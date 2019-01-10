---
layout: post
title: Umbraco - Get prevalues from dropdown list
tags:
  - umbraco
  - umbraco 7.12.4
comments: true
---

![_config.yml]({{ site.baseurl }}/images/umbraco.png)
I recently helped my client adding some features in his existing umbraco solution. 

I decide to use umbraco dropdown list data type to store pre-defined values for some properties and display as dropdown list on the frontend. It took me a bit time to figure out how to pull out the pre-defined values from umbraco for the dropdown list and I would like to take this opportunity to share my implementation.  



```c#
    using Umbraco.Core;
    using Umbraco.Core.Models;

    public class UmbracoContentServiceExtensions
    {
        /// <summary>
        /// Getting prevalues for dropdown lists in Umbraco. 
        /// </summary>
        /// <param name="dataTypeDefinitionName">Data type definition name 
        /// (You can get the data type name from the backoffice under developer -> datatypes)</param>
        /// <returns>A collection of <see cref="IEnumerable{PreValue}"/></returns>
        public static IEnumerable<PreValue> GetDropDropListPrevalues(string dataTypeDefinitionName)
        {
            if (string.IsNullOrWhiteSpace(dataTypeDefinitionName))
                throw new ArgumentNullException(nameof(dataTypeDefinitionName));

            List<PreValue> preValueslst = new List<PreValue>();

            IDataTypeDefinition datatype = ApplicationContext.Current.Services
                                .DataTypeService.GetDataTypeDefinitionByName(dataTypeDefinitionName);

            if (datatype == null)
                return preValueslst.AsEnumerable();

            var preValues = ApplicationContext.Current.Services
                                .DataTypeService.GetPreValuesCollectionByDataTypeId(datatype.Id);

            if (preValues == null)
                return preValueslst.AsEnumerable();

            return preValues.PreValuesAsDictionary.Select(x => x.Value).Where(x => x.Value != "0");
        }
    }

```




Happy Coding! 😇