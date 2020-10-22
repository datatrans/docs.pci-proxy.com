# White label PCI Proxy

The White label PCI Proxy functionality allows you to use your very own domain name or subdomain instead of our PCI Proxy URL, while still being out of PCI DSS scope. 

For instance, if you have an API endpoint shared with partners and you don’t want them to change it. There is no need to give up the administrative rights of your domain, just create a CNAME record to map your domain or subdomain to a PCI Proxy domain.

## Activate the white label domain

To provide you with the CNAME value, please send an email to [support@pci-proxy.com](mailto:support@pci-proxy.com) with the following information:

* your white label domain name
* the PCI Proxy URL – which is available after the integration was installed
* the target URL - where will be your HTTP request forwarded.

Once we will have all the above information, we will order the SSL certificate for you from our partner [Digicert](https://www.digicert.com/) and you will have to demonstrate ownership over the domain. You will be assisted by one of our system engineers to validate the domain name by email or by a DNS TXT record and for the whole remaining process.

After the certificate is issued, we will provide you with the CNAME value, we will activate our server configuration and then we will verify together that everything works as expected.

{% hint style="info" %}
We can start the white labeling process after the contract is signed and the production environment is activated from our side. 
{% endhint %}

## Renewal

Given the fact that starting from the end of August 2020, trusted SSL certificates are no longer available for validity periods longer than 1 year, we will renew the certificates issued by Digicert and you will be in contact with our system engineers for this process.

