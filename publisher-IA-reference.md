# Facebook InstantArticles

The following URI has to be implemented once per adslot. The parameters variies per slot and defines the adrequest to AppNexus:

```html
https://ib.adnxs.com/tt?member=7823&inv_code=bild.de-IA-ros-mrec&size=300x250&cb=[timestamp]&pt0=[siteId]&pt1=[pageName]
```

## Param glossary
Param    | Value                                  | Explanation
--- | --- | --- 
member   | 7823                                   | given by adSolutions
inv_code | ${domainName}-IA-${pageName}-${slotId} | dynamic e.g. "bild.de-IA-ros-mrec" 
size     | 300x250                                | sizes allowed for adslot 
cb       | [timestamp]                            | please make sure to replace [timestamp] with a random number per page impression
pt0      | [siteId]                               | given by adSolutions
pt1      | [pageName]                             | defines the marketing sector
