# finanzen.net_App

In this documentation you find the placement details for webview in your apps.
The integration itself will be almost the same that is used by your mew pages.
For regular tagging question please consult [Integration doc](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md).

## adSSetup

The following adSSetup has been taken from your mobile homepage and extended to fit your InApp Webview.
Please feel free to adjust placements and sizes to your needs.
Please keep in mind, that like in regular websites some of them are normally filled dynamically.
Since we only will be implemented in the news webview "pageName", isArticle and so on can be hard coded.

On the other side we do have two properties (appid and aaid) unique to apps we would asked you to fill properly.

```
adSSetup = {
    'view': 'm',
    'appid': '',
    'aaid': '',
    'partners': true,
    'adPlacements': ["banner", "mrec", "inpage", "mrec_btf", "mrec_btf_2", "mrec_btf_3"],
    'adSlotSizes': {
        "banner": [{"minWidth": 1, "sizes": [[320, 160], [320, 50], [320, 75], [320, 80]]}],
        "mrec": [{"minWidth": 1, "sizes": [[300, 250], [320, 50], [320, 75], [320, 160], [300, 300]]}],
        "inpage": [{"minWidth": 1, "sizes": [[1, 1], [640, 360]]}],
        "mrec_btf": [{
            "minWidth": 1,
            "sizes": [[300, 250], [320, 50], [320, 75], [320, 160], [300, 300], [320, 480], [300, 600], [1000, 300]]
        }]
    },
    'colorBg': false,
    'bgClick': false,
    'stickySky': false,
    'isArticle': true,
    'pageName': 'news_story',
    'target': fin_keywords
};
```

## AdLib

Please use the following JS for the adLib: ```https://www.asadcdn.com/adlib/pages/finanzenApp.js```


## Help

If you have some question don't hesitate to contact us:


__Gertrud Kolb__
 
  Head of AdSolutions
  Corporate Digital Platforms

  Tel: +49 30 2591 72504
  gertrud.kolb@spring-media.de


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  
