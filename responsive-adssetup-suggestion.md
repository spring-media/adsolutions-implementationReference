# Suggestion for responsive AdSSetup

If you have a responsive site and you're wondering how to best combine the ad integration with responsiveness, we'd like to show you one possibility and maybe give you some food for thought.
**Important**: These are only general ideas and suggestions. Since each site is different, these are not necessarily the most efficient solutions.



#### Table of Contents 
- [1. Possible AdSSetup](#1-possible-adssetup)
   - [1.1 Preconfiguration](#11-preconfiguration)
   - [1.2 Putting the AdSetup together](#12-putting-the-adsetup-together)
   - [1.3 MinWidth - reacting to different page dimensions](#13-minwidth---reacting-to-different-page-dimensions)
- [2. Dealing with dynamic adslots](#2-dealing-with-dynamic-adslots)
   - [2.1 Changing adSlot id's directly in the markup](#21-changing-adslot-ids-directly-in-the-markup)
   - [2.2 Do not change adSlots asynchronously](#22-do-not-change-adslots-asynchronously)
- [3. Important Notes](#3-important-notes)


---


# 1. Possible AdSSetup
The AdSSetup is the configuration for our Adlib. Here you control (_besides general settings like the [CLS placeholder](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md)_) which ads and formats are ordered from the adserver.

## 1.1 Preconfiguration
The idea is that the page width is checked with Javascript before the adSSetup is defined and a choice is made between different presets for mobile / tablet / desktop.

The code could look something like this:

```javascript
var windowWidth = window.innerWidth || window.document.documentElement.clientWidth || window.document.body.clientWidth;
var view = "m";

if (windowWidth > 900) {
  view = "d";
} else {
  view = "m";
}
```


The Mrec is included on desktop as well as mobile. Since the possible sizes may differ here, we can predefine them as follows if needed:


```javascript
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

```javascript
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
            "mrec": AdSizes.mrec.d,
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


## 1.2 Putting the AdSetup together
Here we now use our prepared configuration to put together the AdSSetup based on the page width.


```javascript
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



## 1.3 MinWidth - reacting to different page dimensions
With the "minWidth" attribute you can place an order depending on the page width. Using the billboard example - if the page is wider than 969px, the second array is used. If it is less wide, the first array will be used.

```javascript
var billboardSizes = [{
    "minWidth": 1,
    "sizes": [[9,9],[800,250]]
},{
    "minWidth": 969,
    "sizes": [[9,9],[800,250],[970,250]]
}];
```


---


# 2. Dealing with dynamic adslots
While handling HTML containers depending on variables is relatively easy with frameworks like Angular or React compared to vanilla JavaScript.
Nonetheless, there are some ways to set the markup dynamically even with vanilla javascript. 

At this point, we would like to present one possible solution.  


## 2.1 Changing adSlot id's directly in the markup

A possible solution would be to first give the AdSlots a placeholder id and rewrite it after the viewport has been detected.

```html
<div id="adSlot0"></div>
<div id="adSlot1"></div>
<div id="adSlot2"></div>
```

This way you would define another object in the header of the page that contains all AdSlots that should be rendered on the page depending on the viewport.

```html
<script>
    var slotIds = {
        d: ["superbanner", "sky", "billboard", "mrec", "inpage"],
        m: ["banner", "", "mrec", "mrec_btf", "inpage"]
    };
    var slotIdIndex = 0;
</script>
```

However, this object would be different from the previously defined `Ads[view].adPlacements` in this approach, because this time we would also define empty AdSlots that don't get an id depending on the viewport.

This table should help to illustrate the idea:


| placeholder id  | AdSlot on view = d  | AdSlot on view = m  |
| ------------- |:-------------| :-----|
|    adSlot0     |    superbanner     |    banner    |
|    adSlot1     |    sky     |    _none*_    |
|    adSlot2     |    billboard     |    mrec    |
|    adSlot3     |    mrec     |    mrec_btf    |
|    adSlot4     |    inpage     |    inpage    |

_As you can see, the Sky in this example does not get a mobile counterpart because the AdSlot for the mobile viewport does not have a suitable position._


Now we would add a script tag after each placeholder AdSlot container to set the id depending on the viewport.

```html
<div id="adSlot0"></div>

<script>
    document.getElementById("adSlot" + slotIdIndex).id = slotIds[adSSetup.view][slotIdIndex];
    slotIdIndex++;
</script>
```


## 2.2 Do not change adSlots asynchronously 

Please make sure that adSlots are not reloaded from third party modules or changed asynchronously. 
Otherwise this can lead not only to [CLS](https://web.dev/cls/) but also to ad delivery problems.


---


# 3. Important Notes
- All adSSetup configurations are needed in the header of the page, before the adlib is loaded. 
- The adlib needs also to be loaded in the header of the page
- **Important**: Please do not load the adlib async!
- For more informations about the adSSetup and its settings, please have a look into our [general documentation](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md).


## Help
If you have any questions or problem don't hesitate to contact us:

__Ad Technology Team__
  adtechnology@axelspringer.de

