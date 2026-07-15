# IMI - Ad Integration Guide


> 🚧 Work in progress 🚧
>
> **Important:** Please do not reference to this documentation yet, as this is still working in progress in its early phase.

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

- [Strategy](#strategy)
  - [Option 1: Full dynamic ad units in AdSSetup](#option-1-full-dynamic-ad-units-in-adssetup)
  - [Option 2: Full ad unit names as data attributes](#option-2-full-ad-unit-names-as-data-attributes)
- [Basic setup](#basic-setup)
  - [1. Include the AdLib](#1-include-the-adlib)
  - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [AdSSetup.adPlacements](#adssetupadplacements)
    - [AdSSetup.adSlotSizes](#adssetupadslotsizes)
  - [3. Provide Ad Slots](#3-provide-ad-slots)
    - [General](#general)
    - [Custom adslot ids](#custom-adslot-ids)
    - [Example](#example)
- [QA and testing](#qa-and-testing)
  - [Testads](#testads)
  - [Human detection](#human-detection)
- [Help](#help)
   

<br>


-----


From the excel ad unit overview you provided, it seems like a lot of the ad units do not follow a standardized structure, which will be a potential challenge when setting up a full dynamic ad integration that we usually have on the pages we manage.

We crawled a part of skynewsarabia and from that it looks like there are less variable ad units - we only found the following ad units: 

```javascript
[
    "/13259764/Ad unit (all levels)",
    "/13259764/Default",
    "/13259764/Playstream_SkynewsArabia",
    "/13259764/SNA_AMP_MPU_Ad",
    "/13259764/SNA_AMP_MPU_Ad_STG",
    "/13259764/SNA_Article_HM1_Ad",
    "/13259764/SNA_Article_HM1_Ad_STG",
    "/13259764/SNA_Article_HM2_Ad",
    "/13259764/SNA_Article_HM2_Ad_STG",
    "/13259764/SNA_Article_HM_Ad",
    "/13259764/SNA_Article_HM_Ad_STG",
    "/13259764/SNA_Article_LDR/BB1_Ad",
    "/13259764/SNA_Article_LDR/BB1_Ad_STG",
    "/13259764/SNA_Article_LDR/BB2_Ad",
    "/13259764/SNA_Article_LDR/BB2_Ad_STG",
    "/13259764/SNA_Article_Promo_Ad",
    "/13259764/SNA_Article_Promo_Ad2",
    "/13259764/SNA_Article_Promo_Ad2_STG",
    "/13259764/SNA_Article_Promo_Ad_STG",
    "/13259764/SNA_HM1_Ad",
    "/13259764/SNA_HM1_Ad_STG",
    "/13259764/SNA_HM2_Ad",
    "/13259764/SNA_HM2_Ad_STG",
    "/13259764/SNA_HM3_Ad",
    "/13259764/SNA_HM3_Ad_STG",
    "/13259764/SNA_HM4_Ad",
    "/13259764/SNA_HM4_Ad_STG",
    "/13259764/SNA_HM5_Ad",
    "/13259764/SNA_HM5_Ad_STG",
    "/13259764/SNA_Inapp_Insidepage_LMB1_Ad",
    "/13259764/SNA_Inapp_Insidepage_LMB1_Ad_STG",
    "/13259764/SNA_Inapp_Insidepage_MPU1_Ad",
    "/13259764/SNA_Inapp_Insidepage_MPU1_Ad_STG",
    "/13259764/SNA_Inapp_MPU1_Ad",
    "/13259764/SNA_Inapp_MPU1_Ad_STG",
    "/13259764/SNA_Insidepage_HM1_Ad",
    "/13259764/SNA_Insidepage_HM1_Ad_STG",
    "/13259764/SNA_Insidepage_HM2_Ad",
    "/13259764/SNA_Insidepage_HM2_Ad_STG",
    "/13259764/SNA_Insidepage_LDR/BB1_Ad",
    "/13259764/SNA_Insidepage_LDR/BB1_Ad_STG",
    "/13259764/SNA_Insidepage_LDR/BB2_Ad",
    "/13259764/SNA_Insidepage_LDR/BB2_Ad_STG",
    "/13259764/SNA_LDR/BB1_Ad",
    "/13259764/SNA_LDR/BB1_Ad_STG",
    "/13259764/SNA_LDR/BB2_Ad",
    "/13259764/SNA_LDR/BB2_Ad_STG",
    "/13259764/SNA_PreRoll_video",
    "/13259764/SNA_Side_MPU1_Ad",
    "/13259764/SNA_Side_MPU1_Ad_STG",
    "/13259764/SNA_TeadsVideo_Ad",
    "/13259764/SNA_TeadsVideo_Ad_STG"
]
```


# Basic setup


Basically there are only three important steps to implement a basic ad integration:

<br>


## 1. Include the AdLib

Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.<br>
During the onboarding process we provide you a tailor-made version for your page that takes many different settings and special requirements of the site into account.

<br>


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/skynewsarabia.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

We have prepared the following two adlib instances for you:
 - https://www.asadcdn.com/adlib/pages/thenationalnews.js
 - https://www.asadcdn.com/adlib/pages/skynewsarabia.js


**Important**: It is very important, that you **do not** load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 



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
+                adPlacements: ["HM1_Ad", "HM2_Ad"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/skynewsarabia.js"></script>
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
    "adPlacements": ["HM1_Ad", "HM2_Ad"],
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
        "HM1_Ad": [{
            "minWidth": 1,
            "sizes": [[300, 600]]
        }], 
        "LDR--BB1_Ad": [{
            "minWidth": 1,
            "sizes": [[728, 90], [970, 90]]
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
unit.replace("/13259764/SNA_", '').replaceAll("/", "-")
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
                adPlacements: ["HM1_Ad", "HM2_Ad"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/skynewsarabia.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      
+     <div id="HM1_Ad-wrapper">
+         <div id="HM1_Ad"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```

<br>


# Strategy

We evaluated two possible strategies for a clean ad integration on your sites.

1. Use a fully dynamic adSSetup with standardized ad unit structure (see below), or
2. Use a smaller adSSetup configuration and set the full ad unit name as data attribute on the ad slot elements you provide on the page.


From the excel ad unit overview you provided, it seems like a lot of the ad units do not follow a standardized structure, which will be a potential challenge when setting up a full dynamic ad integration that we usually have on the pages we manage.

We crawled a part of skynewsarabia and from that it looks like there are less variable ad units - we only found the following ad units: 

```javascript
[
  "/13259764/SNA_LDR//BB1_Ad",
  "/13259764/SNA_HM1_Ad",
  "/13259764/SNA_HM2_Ad",
  "/13259764/SNA_Side_MPU1_Ad",
  "/13259764/SNA_LDR//BB2_Ad",
  "/13259764/SNA_Article_LDR//BB1_Ad",
  "/13259764/SNA_Article_HM2_Ad",
  "/13259764/SNA_Article_HM1_Ad",
  "/13259764/SNA_Article_Promo_Ad",
  "/13259764/SNA_Article_Promo_Ad2",
  "/13259764/SNA_TeadsVideo_Ad",
  "/13259764/SNA_Article_LDR//BB2_Ad",
  "/13259764/SNA_Insidepage_LDR//BB1_Ad",
  "/13259764/SNA_Insidepage_LDR//BB2_Ad",
  "/13259764/SNA_Insidepage_HM1_Ad",
  "/13259764/SNA_Insidepage_HM2_Ad"
]
```

So if these are the only ad units you currently use, we could go with the first strategy.

<br>

## Option 1: Full dynamic ad units in AdSSetup

Usually we have a naming structure like {publisher}-{platform}-{pagename}-{adslot}, for example "bild.de-desktop-news_article-mrec". Therefore we use part of the adSSetup to build this dynamic structure for ad requests.

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
+                adPlacements: ["SNA_HM1_Ad", "SNA_LDR//BB1_Ad"],
+                adSlotSizes: {
+                    "HM1_Ad": [{
+                        "minWidth": 1,
+                        "sizes": [[300, 600]]
+                    }], 
+                    "LDR--BB1_Ad": [{
+                        "minWidth": 1,
+                        "sizes": [[728, 90], [970, 90]]
+                    }]},
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: false,
+                isArticle: true,
+                pageName: "homepage",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/skynewsarabia.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
+     <div id="HM1_Ad-wrapper">
+         <div id="HM1_Ad" data-adunit="/13259764/SNA_HM1_Ad"></div>
+     </div>
      <div class="your-content">...</div>
+     <div id="LDR--BB1_Ad-wrapper">
+         <div id="LDR--BB1_Ad" data-adunit="/13259764/SNA_LDR//BB1_Ad"></div>
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
+                adPlacements: ["HM1_Ad", "LDR--BB1_Ad"],
+                adSlotSizes: {
+                    "HM1_Ad": [{
+                        "minWidth": 1,
+                        "sizes": [[300, 600]]
+                    }], 
+                    "LDR--BB1_Ad": [{
+                        "minWidth": 1,
+                        "sizes": [[728, 90], [970, 90]]
+                    }]},
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
+     <div id="HM1_Ad" data-adunit="/13259764/SNA_HM1_Ad"></div>
      <div class="your-content">...</div>
+     <div id="LDR--BB1_Ad" data-adunit="/13259764/SNA_LDR//BB1_Ad"></div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

<br>

# QA and testing

**Important**: Please don't try to test ads on Localhost. Ads will be not delivered on localhost.


## Testads

If you would like to test the ad delivery, [here you can set a cookie](https://reports.asadcdn.com/testads.html) to receive some test ads via a test segment.
<br>

> _If you no longer want to receive the test ads, you can always remove the cookie via the 'Remove Testads' button on the same page._

<br>




## Human detection

It can happen, that the adserver does not deliver ads, when the user emulates devices in the browser.

In general the detection tries to find non human or potential malicious requests (e.g. making adcalls from localhost, making many requests within the same second, uncommon request headers, ...).

<br>


-----


# Help

If something is unclear or you have any questions, you can contact us via email:


__Ad Technology Team__
adtechnology@axelspringer.de
