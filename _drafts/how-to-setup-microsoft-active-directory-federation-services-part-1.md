# How to setup Microsoft Active Directory Federation Services [AD FS] - Part 1


![_config.yml]({{ site.baseurl }}/images/adfs_dev_1.png)


1. Windows 2016 Setup
2. Install Active Directory
3. Configurae Active Directory
4. Install IIS
5. Create SSL certificate - Self-sign
6. Install Active Directory Federation Service (AD FS)
7. Configure Active Directory Federation Service (AD FS)

## Create self-sign certificate

The following script will generate 3 years self-sign certificate.  

> Replace **FQDN** with your auzre public DNS name.



```powershell
$todaydt = Get-Date
$3years = $todaydt.AddYears(3)
New-SelfSignedCertificate -dnsname <FQDN> -notafter $3years -friendlyname 'Episerver adfs SelfSigned' -CertStoreLocation cert:\LocalMachine\My
```

Once your run the above script, you will get see `Thumbprint` from the output, make sure you copy this somewhere as this will be used in the next step when you export the certificate.

![_config.yml]({{ site.baseurl }}/images/adfs/Inkedpowershell-New-SelfSignedCertificate_LI.jpg)





## Export certificate

### Generate private key certificate (PFX file)



The following script outputs the private key certificate to a password protected PFX file.

```powershell
$CertPassword = ConvertTo-SecureString -String “Yourpassword” -Force –AsPlainText
Export-PfxCertificate -Cert cert:\LocalMachine\My\C3DEE647F579CBFC86E14D5924D93527F23FD25C -FilePath C:\Users\your name\adfs.pfx -Password $CertPassword
```

### Generate public certificate

The following script outputs the public certificate.


```powershell
Export-Certificate -Cert Cert:\LocalMachine\My\C3DEE647F579CBFC86E14D5924D93527F23FD25C -FilePath C:\Users\your name\adfscert.cer
```



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
> * IdP-Initiaged SSO page endpoint is disabled 
>   
>   By default, if you're using Windows Server 2016, this endpoint is disabled, use the following cmdlet to enable it.
>   
>   ```powershell
>   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
>   ```

## Reference


* [How to create self signed certificate with powershell](http://woshub.com/how-to-create-self-signed-certificate-with-powershell/){:target="_blank"}

* [ADFS Passive Request = “There are no registered protocol handlers”](https://serverfault.com/questions/824303adfs-passive-request-there-are-no-registered-protocol-handlers){:target="_blank"}

* [How to setup Microsoft Active Directory Federation Services [AD FS]](https://www.virtuallyboring.com/how-to-setup-microsoft-active-directory-federation-services-adfs/){:target="_blank"}

* [How to Create a Self-Signed Certificate Using PowerShell](http://woshub.com/how-to-create-self-signed-certificate-with-powershell/){:target="_blank"}






