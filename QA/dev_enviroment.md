# Using the Beta environment for display Ads

In order to use our Dev environment you should only redirect the AdLib request **from** the global Xandr CDN **to** the Ad Solutions development server.

From `https://acdn.adnxs.com/as/*` / `https://www.asadcdn.com/adlib/*`

--> to `https://adtechnology.axelspringer.com/dev/$1`

## How to redirect the requests?

We recommend to use the Chrome browser Plugin [Redirector](https://chrome.google.com/webstore/detail/redirector/ocgpenflpmgnfapjedencafcfakcekcd)

### Settings for Redirector:

![Settings for Redirector](https://github.com/spring-media/adsolutions-implementationReference/blob/master/assets/dev_redirector.png?raw=true)

**You can also use Charles Proxy, Wireshark or whatever you like most as alternative.**



If you have some question don't hesitate to contact us:


__Ad Technology Team__
  adtechnology@axelspringer.de
  
