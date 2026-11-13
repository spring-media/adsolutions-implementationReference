## 🚧 Work in Progress 🚧

# Almashhad - Ad Integration Guide

<br>

## Table of contents

- [Ad unit overview](#ad-unit-overview)
- [Basic setup](#basic-setup)
  - [1. Include the AdLib](#1-include-the-adlib)
  - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [AdSSetup.adPlacements](#adssetupadplacements)
    - [AdSSetup.adSlotSizes](#adssetupadslotsizes)
  - [3. Provide Ad Slots](#3-provide-ad-slots)
    - [General](#general)
    - [Custom adslot ids](#custom-adslot-ids)
    - [Example](#example)
- [Strategy](#strategy)
  - [Option 1: Full dynamic ad units in AdSSetup](#option-1-full-dynamic-ad-units-in-adssetup)
  - [Option 2: Full ad unit names as data attributes](#option-2-full-ad-unit-names-as-data-attributes)
- [Help](#help)
   

<br>


-----


# Ad unit overview

From the first look on almashhad.com we found the following adunits:

```javascript
[
    "/22879256770/AlMashhad-Ad2",
    "/22879256770/almashhad-ad4"
]
```


# Basic setup


Basically there are only three important steps to implement a basic ad integration:

<br>


## 1. Include the AdLib

Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.<br>
During the onboarding process we provide you a tailor-made version ofthe adlib for your page that takes many different settings and special requirements of the site into account.

<br>


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/almashhad.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

> 🚧 Work in Progress 🚧
> We will prepare an adlib instance for you to test with.

<br>

**Important**: 
 - It is very important, that you **do not** load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 
 - Please make sure that the adlib is loaded **after** the CMP stub.


<br>


## 2. AdSSetup - provide the config for the ad delivery

Think of this part like a shopping cart - in the AdSSetup object, you define various settings. For example, you have to 'order' the type of Ads, you want to see on your page, like in our case Mrecs, Billboards and Superbanners. <br>
The names will be different in your setup since you have different naming conventions.
We will add a suggestion for how to create the adSSetup object for your pages at the end of this documentation.

<br>


```diff

<html>
    <head>
        <title>Your great website</title>
        
+        <script type="text/javascript">
+            adSSetup = {
+                view: "d",
+                partners: true,
+                adPlacements: ["AlMashhad-Ad2", "almashhad-ad4"],
+                adSlotSizes: { ... },
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: false,
+                isArticle: true,
+                pageName: "news_story",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/almashhad.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

There are also some features, you can control via the AdSSetup object, like the appearance of the placeholders. 
You can find a detailed overview with explanation of all parameters for the adSSetup [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

<br>

**Important**: 

 - Make sure, that the adSSetup Object is ready, when the adlib is loaded, so that we can use your configuration to make the call to the ad server.
 - Be sure that you only order placements in the adSSetup.adPlacements, for which you know that you have a matching ad slot on your page, where the delivered ad can be rendered in.


<br>


### AdSSetup.adPlacements

In this array, you include all ad slots you have on the page that should be included in ad requests.

```javascript

adSSetup = {
    ...
    "adPlacements": ["AlMashhad-Ad2", "almashhad-ad4"],
    ...
}

```



<br>


### AdSSetup.adSlotSizes

Going on with our example adSSetup object, we continue with the ad formats we request via sizes.
Here we want to request ads for a desktop page, so we set the `"view"` attribute to `"d"`.

Additionally, we define the ad slots that are on this desktop page and decide with the size attributes which ad formats are allowed in these ad slots.



```javascript

adSSetup = {
    ...
    "view": "d",
    "adSlotSizes": {
        "AlMashhad-Ad2": [{
            "minWidth": 1,
            "sizes": [[300, 100], [468, 60], [728, 90]]
        }], 
        "almashhad-ad4": [{
            "minWidth": 1,
            "sizes": [[300, 250]]
        }]},
    },

    ...
}

```

<br>


## 3. Provide Ad Slots

### General

You as publisher need to provide us a container for each ad, that you ordered via the adSSetup object. The delivered ads will be rendered in these Ad Slots, so it is very important that there is a container for each ad on the page. The Ad Slots will need the ad type as id and have to be completely unstyled.
If you need styling around the ad, you can set a wrapper around the Ad Slot and style this wrapper instead.

<br>

### Custom adslot ids

We would suggest that you set the div ids of the ad slots like this:

```javascript
unit.replace("/22879256770/", '')
```

So the ad unit "/13259764/SNA_LDR//BB1_Ad" would become the ad slot id "LDR--BB1_Ad". Replacing the `/` characters would make it easier to interact with the html for us. The ad slots you order in the adSSetup object and the full ad units we generate from the infos from the adSSetup object would still result in `/13259764/SNA_LDR//BB1_Ad`.

<br>

### Example


```diff

<html>
    <head>
        <title>Your great website</title>
        
        <script type="text/javascript">
            adSSetup = {
                view: "d",
                partners: true,
                adPlacements: ["AlMashhad-Ad2", "almashhad-ad4"],
                adSlotSizes: { ... },
                placeholder: { ... },
                colorBg: true,
                bgClick: true,
                hasVideoPlayer: false,
                isArticle: true,
                pageName: "news_story",
                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
                iabTax: "IAB2,IAB2-1,1,32"
            }
        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/almashhad.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      
+     <div id="AlMashhad-Ad2-wrapper">
+         <div id="AlMashhad-Ad2"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```

<br>


# Strategy

We evaluated two possible strategies for a clean ad integration on your sites.

1. Use a fully dynamic adSSetup with standardized ad unit structure, or
2. Use a smaller adSSetup configuration and set the full ad unit name as data attribute on the ad slot elements you provide on the page.


As mentioned earlier, we crawled a part of skynewsarabia and from that it looks like there are less variable ad units - we only found the ad units mentioned in the section [Ad unit overview](#ad-unit-overview). 

So if these are the only ad units you currently use, we could go with the first strategy.

<br>

## Option 1: Full dynamic ad units in AdSSetup

Usually we have a naming structure like {publisher}-{platform}-{pagename}-{adslot}, for example "bild.de-desktop-news_story-mrec". Therefore we use part of the adSSetup to build this dynamic structure for ad requests.

If your ad units always only consist of "/{publisher_id}/{adslot}", you can let the `adSSetup.pagename` value empty.
Otherwise, if you plan to have a more granular, standardized naming convention for your ad units, you can use the `adSSetup.pagename` attribute for that. If you want to make it even more granular and have different ad units based on viewport, we can do that, too.

<br>

```diff
<html>
    <head>
        <title>Your great website</title>
        
+        <script type="text/javascript">
+            adSSetup = {
+                view: "d",
+                partners: true,
+                adPlacements: ["AlMashhad-Ad2", "almashhad-ad4"],
+                adSlotSizes: {
+                   "AlMashhad-Ad2": [{
+                      "minWidth": 1,
+                      "sizes": [[300, 100], [468, 60], [728, 90]]
+                   }], 
+                   "almashhad-ad4": [{
+                      "minWidth": 1,
+                      "sizes": [[300, 250]]
+                   }]},
+                },
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: false,
+                isArticle: true,
+                pageName: "news_story",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/almashhad.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
+     <div id="AlMashhad-Ad2-wrapper">
+         <div id="AlMashhad-Ad2" data-adunit="/22879256770/AlMashhad-Ad2"></div>
+     </div>
      <div class="your-content">...</div>
+     <div id="almashhad-ad4-wrapper">
+         <div id="almashhad-ad4" data-adunit="/22879256770/almashhad-ad4"></div>
+     </div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

<br>

## Option 2: Full ad unit names as data attributes

If you have a lot of static ad unit names that do not follow one standard naming convention, than you can still go with the second option and set the full ad unit name as data attribute on the adslot:

<br>

```diff
<html>
    <head>
        <title>Your great website</title>
        
+        <script type="text/javascript">
+            adSSetup = {
+                view: "d",
+                partners: true,
+                adPlacements: ["AlMashhad-Ad2", "almashhad-ad4"],
+                adSlotSizes: {
+                   "AlMashhad-Ad2": [{
+                      "minWidth": 1,
+                      "sizes": [[300, 100], [468, 60], [728, 90]]
+                   }], 
+                   "almashhad-ad4": [{
+                      "minWidth": 1,
+                      "sizes": [[300, 250]]
+                   }]},
+                },
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: false,
+                isArticle: true,
+                pageName: "",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/skynewsarabia.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
+     <div id="AlMashhad-Ad2" data-adunit="/22879256770/AlMashhad-Ad2"></div>
      <div class="your-content">...</div>
+     <div id="almashhad-ad4" data-adunit="/22879256770/almashhad-ad4"></div>
      <div class="your-content">...</div>
      
    </body>
</html>
```



-----


# Help

If something is unclear or you have any questions, you can contact us via email:


__Ad Technology Team__
adtechnology@axelspringer.de
