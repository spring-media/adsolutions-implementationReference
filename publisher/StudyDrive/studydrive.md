
# :warning: Work in Progress :warning:
This document is still work in progress and not meant to be used yet! 


--------


# StudyDrive Ad Integration Guide

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.



## Table of contents

 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [3. Provide Ad Slots](#3-provide-ad-slots)
 - [Text](#url)
   



# Basic setup


Basically there are only three important steps to implement a basic ad integration:

## 1. Include the AdLib

> Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.
> During the onboarding process we provide you a tailor-made version for your page that takes many different settings and special requirements of the site into account.


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="cdn/pages/website.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

**Important**: It is very important, that you do not load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 


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
+                adPlacements: ["superbanner", "sky", "billboard", "mrec", "mrec_btf", "mrec_btf_2", "mrec_btf_3", "inpage"],
+                adSlotSizes: { ... },
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: true,
+                isArticle: true,
+                pageName: "demo_story",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="cdn/pages/website.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

Make sure, that the adSSetup Object is ready, when the adlib is loaded, so that we can use your configuration to make the call to the ad server.


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
                adPlacements: ["superbanner", "sky", "billboard", "mrec", "mrec_btf", "mrec_btf_2", "mrec_btf_3", "inpage"],
                adSlotSizes: { ... },
                placeholder: { ... },
                colorBg: true,
                bgClick: true,
                hasVideoPlayer: true,
                isArticle: true,
                pageName: "demo_story",
                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
                iabTax: "IAB2,IAB2-1,1,32"
            }
        </script>
        
        <script type="text/javascript" src="cdn/pages/website.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      
+     <div id="billboardWrapper">
+         <div id="billboard"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```


And just like that, you already have a basic working ad integration on your page. If you would like to test the ad delivery, [here you can set a cookie](https://reports.asadcdn.com/testads.html) to receive some test ads via a test segment.

_If you no longer want to receive the test ads, you can always remove the cookie via the 'Remove Testads' button on the same page._


----------





## Publisher-specific integration

> The content above describes a sample integration, but every integration is different and has its own challenges.<br>
> Below we will learn what particular challenges we have in this project and how we will solve them.



### Setting together the adSSetup

You can find an overview with explanation of all parameters for the adSSetup [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).


### Pagename structure

You can have a look into [this document](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/pagename-structure.md), to get a basic understanding on how pagenames & keyword targetings work.





## InApp Ad Integration

`- coming soon -`


