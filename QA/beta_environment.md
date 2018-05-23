# Using the Beta environment for display Ads

In order to use our Beta environment you should only redirect the AdLib request **from** the global Appnexus CDN **to** the Ad Solutions development server.

From `https://acdn.adnxs.com/as/1h/pages/*` 

--> to `https://adtechnology.axelspringer.com/beta/1h/pages/*`

## How to redirect the requests?

We recommend to use the Chrome browser Plugin [Redirector](https://chrome.google.com/webstore/detail/redirector/ocgpenflpmgnfapjedencafcfakcekcd)

### Settings for Redirector:

![Settings for Redirector](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/redirector.png?raw=true)

**You can also use Charles Proxy as alternative.**