---
layout: post
title: Perform tracking customization
tags:
  - episerver
  - episerver commerce
  - episerver perform
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver.png)
Recently I helped one of the customer to implement profile tracking and perform recommendation for their B2B solution built on Episerver ecommerce platform. I found an issue during the implementation I would like to share in this post.


## Summary

Let's start with a quick summary of the scenarios I have in the solution before we dive into the customization

For the perform integration, I choose the [Server side API integration](https://world.episerver.com/documentation/developer-guides/commerce/personalization/recommendations/server-side-api-integration/) approach as the solution needs to support both web app and native mobile app. The following scenarios are special in this commerce project

1. Using non default cart (The default cart naming convention is `Default-{CustomerID}`, which the `CustomerID` is the unique identifier in the ERP system that stored to the Episerver `Organization` object.)

## Issues

When creates the `TrackingData` object with `TrackingDataFactory` class, the following methods require the `Cart` object, and by default it will load the cart with `Default` cart name.

* CreateCartTrackingData
* CreateCheckoutTrackingData

```c#

    public class TrackingDataFactory
    {
        public virtual CartTrackingData CreateCartTrackingData(HttpContextBase httpContext)
        {
            IOrderGroup currentCart = GetCurrentCart();
            if (currentCart == null)
            {
                return null;
            }
            return new CartTrackingData(GetCartDataItems(currentCart), currentCart.Currency.CurrencyCode, _languageResolver.GetPreferredCulture().Name, GetRequestData(httpContext), GetCommerceUserData(httpContext));
        }

        public virtual CheckoutTrackingData CreateCheckoutTrackingData(HttpContextBase httpContext)
        {
            IOrderGroup currentCart = GetCurrentCart();
            if (currentCart == null)
            {
                return null;
            }
            return new CheckoutTrackingData(GetCartDataItems(currentCart), currentCart.Currency.CurrencyCode, currentCart.GetSubTotal(_orderGroupCalculator).Amount, currentCart.GetShippingSubTotal(_orderGroupCalculator).Amount, currentCart.GetTotal(_orderGroupCalculator).Amount, _languageResolver.GetPreferredCulture().Name, GetRequestData(httpContext), GetCommerceUserData(httpContext));
        }              

        protected virtual IOrderGroup GetCurrentCart()
        {
            return _orderRepository.LoadCart<ICart>(GetContactId(), Cart.DefaultName, _currentMarket);
        }
    }
```

## Solution
In order to load the custom cart, we'll need to replace the default implementation of `GetCurrentCart()` behavior. Luckily, Episerver has already thought about this needs and provided the capability to override `GetCurrentCart()` implementation. To fix the issue, I have to create overloaded methods for both `CheckoutTrackingData` and `CartTrackingData` to be able to receive the `CustomerId` in order to customize the cart name. Finally, in the calling method, use the overloaded methods instead of the default one. 


```c#
    public class CustomTrackingDataFactory : TrackingDataFactory
    {

        public virtual CheckoutTrackingData CreateCheckoutTrackingData(HttpContextBase httpContext, string customerId)
        {
            _customerId = customerId;
            return base.CreateCheckoutTrackingData(httpContext);
        }

        public virtual CartTrackingData CreateCartTrackingData(HttpContextBase httpContext, string customerId)
        {
            _customerId = customerId;
            return base.CreateCartTrackingData(httpContext);
        }

        protected override IOrderGroup GetCurrentCart()
        {
            var cartName = ServiceLocator.Current.GetInstance<ICartService>().GetCustomerCartName(Cart.DefaultCartName, _customerId);
            return _orderRepository.LoadCart<ICart>(GetContactId(), cartName, _currentMarket);
        }
    }
```

## Reference

[Recommendations API overview](https://world.episerver.com/documentation/developer-guides/commerce/personalization/recommendations/an-API-overview/)


Happy Coding! 😇