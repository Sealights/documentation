# Check the connectivity to the Sealights server from my machine

Some network security policies may prevent agents from reaching the SeaLights platform. This is normally caused due to security policies related to Firewalls, or other networking-related security configurations that prevent access to the SeaLights API.

To verify this is the case, try running a cURL command to your dashboard URL:

{% tabs %}
{% tab title="Linux" %}
```bash
curl -I https://<YourCustomDNSName>.sealights.co
```
{% endtab %}

{% tab title="Powershell" %}
```powershell
Invoke-WebRequest -Uri https://<YourCustomDNSName>.sealights.co -UseBasicParsing | Select-Object StatusCode,StatusDescription
```
{% endtab %}
{% endtabs %}

If you don't have the URL of your dedicated Sealights account or if you need a generic Sealights endpoint, you can use `https://connect.sealights.co` in the above command.

{% hint style="success" %}
`HTTP/2 200` code should be returned. If this code is received, you can access the SeaLights API and there is no need for this document.
{% endhint %}

If using a proxy, you should add the relevant parameter to the command

{% tabs %}
{% tab title="Linux" %}
```bash
curl -vI https://<YourCustomDNSName>.sealights.co --proxy http://myproxy.mycompany.int
```
{% endtab %}

{% tab title="Powershell" %}
```powershell
Invoke-WebRequest -Proxy <MyProxyUri> -Uri https://<YourCustomDNSName>.sealights.co -UseBasicParsing | Select-Object StatusCode,StatusDescription
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In case this command fails, it is important to understand why. Looking at the detailed output (given by the `-vI` flags) can point us in the right direction.

For Windows, more details can be found on [Microsoft’s Official documentation](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest) page.
{% endhint %}

{% hint style="info" %}
Important note: We have seen cases in which different machines/containers had different permissions with regard to an outbound connection to Sealights. Please consider repeating this connectivity test from your CI machines and the machines that run your tests and your system under test.
{% endhint %}

## How to resolve connectivity issues&#x20;

In case a firewall is present, it needs to **allow network traffic to reach the SeaLights platform,** and depending on your organization’s policy, you can use one of the following solutions.

### Allowing outbound traffic to Sealights' domain <a href="#allow-outbound-traffic-to-sealights-domain" id="allow-outbound-traffic-to-sealights-domain"></a>

The Firewall should **allow** outbound connections on port 443 (TLS v1.2) to **our domain** `https://*.sealights.co`.\
For a more restrictive rule, you can open the connections to your Sealights dashboard URL only.

### Allowing outbound traffic to Sealights' range of IP addresses <a href="#allow-outbound-traffic-to-sealights-range-of-ip-addresses" id="allow-outbound-traffic-to-sealights-range-of-ip-addresses"></a>

As SeaLights' networking is managed in AWS, the full list of subnets pointing to our platform can be found in the [ip-ranges.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file supplied by AWS.

Be sure to follow the next steps to understand which IP addresses need to be added to your exceptions list:

1. Download the provided `ip-ranges.json` file from AWS.
2. From the file, filter out the entries related to CloudFront (using `jq` tool for example): \
   `cat ip-ranges.json | jq '.prefixes[] | select(.service=="CLOUDFRONT")'`
3. **Add the subnets** output from the previous stage **to your Firewall exception** list for outbound connections on port 443 (TLS v1.2)

{% hint style="info" %}
Some customers may have their servers managed via F5 Volterra, therefore the IP Ranges should be configured based on the following information [![](https://docs.cloud.f5.com/docs/favicon-32x32.png)Firewall or Proxy Reference for Network Cloud | F5 Distributed Cloud Tech Docs](https://docs.cloud.f5.com/docs/reference/network-cloud-ref)
{% endhint %}
