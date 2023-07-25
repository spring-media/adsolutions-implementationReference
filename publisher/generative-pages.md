
# Generative Pages - Ad Integration Guide

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

 - [Strategy](#strategy)
 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
        - [AdSSetup.adSlotSizes - Desktop](#adssetupadslotsizes---desktop) 
        - [AdSSetup.adSlotSizes - Mobile](#adssetupadslotsizes---mobile) 
    - [3. Provide Ad Slots](#3-provide-ad-slots)
 - [QA and testing](#qa-and-testing)
    - [Testads](#testads)
    - [Human detection](#human-detection)
 - [Help](#help)
   

<br>


-----


# Strategy

To make the ad integration on these pages as easy as possible, we will only implement the adslots Superbanner & Sky (on desktop viewport) and the first Mrec after the first teaser image (on mobile viewport).
The following ad slots in the content will be delivered via Gaia. Gaia is our solution to place adslots dynamically in the content based on some predefined rules.
Gaia will handle everything from placing the additional adslots in the content as well as the ad requests and rendering.



# Basic setup


Basically there are only three important steps to implement a basic ad integration:

<br>


## 1. Include the AdLib

> Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.
> During the onboarding process we provide you a tailor-made version for your page that takes many different settings and special requirements of the site into account.

<br>


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/adtechnology.axelspringer.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

**Important**: It is very important, that you **do not** load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 

<br>


#### 🚧 Work in progress 🚧 


> We will use our **adtechnology.axelspringer.js** for now until we now the final domains and create a specified adlib for every page.
> As soon as we can inspect the html structure of the pages, we will look for some specific selectors which are important for placing our ads on the page. While we are working with the **adtechnology.axelspringer.js**, it can happen that rendered ads are not proberly centered, since these specific selectors are missing in the setup.


<br>


## 2. AdSSetup - provide the config for the ad delivery

> Think of this part like a shopping cart - in the AdSSetup object, you define various settings. For example, you have to 'order' the type of Ads, you want to see on your page, like Mrecs, Billboards and Superbanners.
> But there are also some features, you can control via the AdSSetup object, like the appearance of the placeholders. 


```diff

<html>
    <head>
        <title>Your great website</title>
        
+        <script type="text/javascript">
+            adSSetup = {
+                view: "d",
+                partners: true,
+                adPlacements: ["superbanner", "sky"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/adtechnology.axelspringer.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

You can find a detailed overview with explanation of all parameters for the adSSetup [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

<br>

**Important**: 

 - Make sure, that the adSSetup Object is ready, when the adlib is loaded, so that we can use your configuration to make the call to the ad server.
 - Be sure that you only order placements in the adSSetup.adPlacements, for which you know that you have a matching ad slot on your page, where the delivered ad can be rendered in.


<br>



### AdSSetup.adSlotSizes - Desktop

Please use these sizes for your ad integration on desktop viewports for now:

```javascript

adSSetup = {
    ...
    "adPlacements": ["superbanner", "sky"],
    "adSlotSizes": { 
        "superbanner": [{
            "minWidth": 1,
            "sizes": [[728, 90], [728, 600], [1000, 600]]
        }], 
        "sky": [{
            "minWidth": 1,
            "sizes": [[160, 600], [120, 600], [300, 600], [500, 1000], [1000, 1000]]
        }]
    },
    ...
}

```


<br>



### AdSSetup.adSlotSizes - Mobile

Please use these sizes for your ad integration on mobile viewports for now:

```javascript

adSSetup = {
    ...
    "adPlacements": ["mrec"],
    "adSlotSizes": { 
        "mrec": [{
            "minWidth": 1,
            "sizes": [[320,160], [320,75], [320,50], [300,300], [300,250]]
        }]
    }
    ...
}

```


<br>



## 3. Provide Ad Slots

> You as publisher need to provide us a container for each ad, that you ordered via the adSSetup object. The delivered ads will be rendered in these Ad Slots, so it is very important that there is a container for each ad on the page. The Ad Slots will need the ad type as id and have to be completely unstyled.
> If you need styling around the ad, you can set a wrapper around the Ad Slot and style this wrapper instead.


```diff

<html>
    <head>
        <title>Your great website</title>
        
        <script type="text/javascript">
            adSSetup = {
                view: "d",
                partners: true,
                adPlacements: ["superbanner", "sky"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/adtechnology.axelspringer.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      
+     <div id="superbannerWrapper">
+         <div id="superbanner"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```


And just like that, you already have a basic working ad integration on your page. If you would like to test the ad delivery, [here you can set a cookie](https://reports.asadcdn.com/testads.html) to receive some test ads via a test segment.

_If you no longer want to receive the test ads, you can always remove the cookie via the 'Remove Testads' button on the same page._


<br>



# QA and testing

**Important**: Please don't try to test ads on Localhost. Ads will be not delivered on localhost.



## Testads

If you would like to test the ad delivery, you can set a special cookie here: https://reports.asadcdn.com/testads.html to receive some test ads via a test segment.
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



