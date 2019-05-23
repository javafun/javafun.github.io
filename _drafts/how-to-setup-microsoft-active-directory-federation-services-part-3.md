

# How to setup Microsoft Active Directory Federation Services [AD FS] - Part 3



## Troubleshooting

`Encountered error during federation passive request.  Microsoft.IdentityServer.RequestFailedException: MSIS7065: There are no registered protocol handlers on path /adfs/ls to process the incoming request.`

> When you encounter this error, check the AD FS event log to find out more detials. The following scenarios could lead the above errors 
> 
> * Wrong SSO page url 
>   
>   If you want to check ADFS is operational or not, you should access to the following page URL with the aspx extension (**/IdpInitiatedSignon.aspx**) 
>   
>   **https://FQDN/adfs/ls/IdpInitiatedSignon.aspx**
>   
>   
> 
> * IdP-Initiaged SSO page endpoint is disabled 
>   
>   By default, if you're using Windows Server 2016, this endpoint is disabled, use the following cmdlet to enable it.
>   
>   ```powershell
>   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
>   ```









## Reference

* [How to create self signed certificate with powershell]([http://woshub.com/how-to-create-self-signed-certificate-with-powershell/](http://woshub.com/how-to-create-self-signed-certificate-with-powershell/)

* [ADFS Passive Request = “There are no registered protocol handlers”]([https://serverfault.com/questions/824303/adfs-passive-request-there-are-no-registered-protocol-handlers](https://serverfault.com/questions/824303/adfs-passive-request-there-are-no-registered-protocol-handlers))




