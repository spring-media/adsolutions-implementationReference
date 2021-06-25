# Suggestion for responsive AdSSetup

If you have a responsive site and you're wondering how to best combine the ad integration with responsiveness, we'd like to show you one possibility and maybe give you some food for thought.
**Important**: These are just general ideas and are not necessarily the most efficient solution.



## Possible AdSSetup
The AdSSetup is the configuration for our Adlib. Here you control (_besides general settings like the [CLS placeholder](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md)_) which ads and formats are ordered from the adserver.

### Preconfiguration
The idea is that the page width is checked with Javascript before the adSSetup is defined and a choice is made between different presets for mobile / tablet / desktop.

The code could look something like this:

```
var windowWidth = window.innerWidth || window.document.documentElement.clientWidth || window.document.body.clientWidth;
var view = "m";

if (windowWidth > 900) {
  view = "d";
} else {
  view = "m";
}
```


The Mrec is included on desktop as well as mobile. Since the possible sizes may differ here, we can predefine them as follows if needed:


```
var AdSizes = {
      mrec: {
        m: [{
          "minWidth": 1,
          "sizes": [[9,9],[300,250],[320,50],[320,75],[320,160],[300,300]]
        }],
        d: [{
          "minWidth": 1,
          "sizes": [[9,9],[300,250],[320,160],[300,300]]
        }]
      }
}
```



Then we define adPlacements and adSlotSizes for the different views:

```
var Ads = {

    m: {
        adPlacements: ["banner","mrec","mrec_btf","mrec_btf_2","inpage"],
        adSlotSizes: {
            "mrec": AdSizes.mrec.m,
            "mrec_btf": AdSizes.mrec.m,
            "mrec_btf_2": AdSizes.mrec.m,
            "banner": [{
                "minWidth": 1,
                "sizes": [[9,9],[320,50],[320,75],[320,80]]
            }],
            "inpage": [{
                "minWidth": 1,
                "sizes": [[1,1],[640,360]]
            }],
        }
    },

    d: {
        adPlacements: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","inpage"],   
        adSlotSizes: {
            "mrec": AdSizes.mrec.n,
            "mrec_btf": AdSizes.mrec.d,
            "mrec_btf_2": AdSizes.mrec.d,
            "superbanner": [{
                "minWidth": 1,
                "sizes": [[9,9],[728,90],[728,600],[1000,600]]
            }],
            "sky": [{
                "minWidth": 1,
                "sizes": [[9,9],[160,600],[120,600],[300,600]]
            }],
            "billboard": [{
                "minWidth": 1,
                "sizes": [[9,9],[800,250]]
            }],
            "inpage": [{
                "minWidth": 1,
                "sizes": [[1,1],[640,360],[1000,300]]
            }],
        }
    },
}
```


### Putting the AdSetup together
Here we now use our prepared configuration to put together the AdSSetup based on the page width.


```
adSSetup = {

  adPlacements: Ads[view].adPlacements,
  adSlotSizes: Ads[view].adSlotSizes,

  view: view,
  partners: true,
  colorBg: false,
  bgClick: true,
  hasVideoPlayer: true,
  isArticle: false,
  pageName: "home_index",
  target: "value1;value2;value3;key1=value1",
  iabTax: "IAB2,IAB2-1,1,32",

  placeholder: {
       disablePlaceholders: false,
       default: {
          "border-color": "rgba(0,0,0,0)",
          "background-color": "#eee",
          "admarkPosition": "bottom right",
          "color": "#999",
          "font-size": "12px",
          "font-family": "Tahoma"
       }
   }
}
```



### MinWidth - reacting to different page dimensions
With the "minWidth" attribute you can place an order depending on the page width. Using the billboard example - if the page is wider than 969px, the second array is used. If it is less wide, the first array will be used.

```
var billboardSizes = [{
    "minWidth": 1,
    "sizes": [[9,9],[800,250]]
},{
    "minWidth": 969,
    "sizes": [[9,9],[800,250],[970,250]]
}];
```




# Important Notes
- All adSSetup configurations are needed in the header of the page, before the adlib is loaded. 
- The adlib needs also to be loaded in the header of the page
- **Important**: Please do not load the adlib async!
- For more informations about the adSSetup and its settings, please have a look into our [general documentation](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md).
