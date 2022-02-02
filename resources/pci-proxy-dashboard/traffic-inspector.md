# Traffic Inspector

The Traffic Inspector enables you to monitor and debug traffic on a specific integration in real-time. It allows you to see the entire stream of a request sent through PCI Proxy. As well, you can access payload data and see exactly what's sent to and returned by a target endpoint. Simply navigate to the `Traffic Inspector` menu on the left-hand side menu bar or access it within the `Developers` menu directly and activate the logging for 15 minutes to help you to introspect the traffic and to adjust your integration or payload accordingly.

Due to the logging of sensitive cardholder data, the Traffic Inspector is currently available on the Sandbox environment only.

### Activate the Traffic Inspector <a href="#activate-the-traffic-inspector" id="activate-the-traffic-inspector"></a>

To activate the record function choose an integration assigned to your account and hit the Start recording button.

![](<../../.gitbook/assets/traffic inspector 1.png>)

### Get an overview of logged requests  <a href="#get-an-overview-about-logged-requests" id="get-an-overview-about-logged-requests"></a>

Once you send data to the PCI Proxy API wait until the record has been loaded into the dashboard to see an overview of the collected request. This overview displays some basic information like target HTTP status code, target URI, timestamp, or the number of conversions done on request or response.

You can have multiple activated sessions (integrations). Choose the sessions you want to view data in the top-right menu by simply clicking on it.

![](<../../.gitbook/assets/traffic inspector 2.png>)

### View detailed request data <a href="#view-detailed-request-data" id="view-detailed-request-data"></a>

To access the entire stream of a request simply click on the record you want to view. Once done you can view all the request-specific data, the headers, and the body of the request and response. From the very beginning of the request until the end you can see all the operations performed including internal PCI Proxy application processing time.

![](<../../.gitbook/assets/traffic inspector 3.png>)

