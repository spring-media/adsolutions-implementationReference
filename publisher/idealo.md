
# Idealo - Ad Integration Guide

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

 - [Strategy](#strategy)
    - [Pagename Structure](#pagename-structure)
    - [Programmatic Advertising](#programmatic-advertising)
 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
        - [AdSSetup.adSlotSizes - Desktop](#adssetupadslotsizes---desktop) 
        - [AdSSetup.adSlotSizes - Mobile](#adssetupadslotsizes---mobile) 
    - [3. Provide Ad Slots](#3-provide-ad-slots)
 - [QA and testing](#qa-and-testing)
    - [Testing on localhost](#testing-on-localhost)
    - [Testads](#testads)
    - [Human detection](#human-detection)
 - [Help](#help)
   

<br>


-----


# Strategy


## Pagename Structure

The pagename is part of the adSSetup object and defines where the user currently is on your website. That can be an article page or a category page.
Each pagename has to exist in the ad server as placement group.

We learned in the kickoff meeting, that the category names that we would suggest to be used as pagename can change over time and that only their IDs remain unique.
It would be possible the create placement groups based on the IDs. While it is technically fine, it might be a bit more difficult when reporting data from the ad server since you need to know which ID maps to which category.

<br>

## Programmatic Advertising

Since it is currently not planned to start with programmatic ads & headerbidding, you just have to set the `partners` flag in the adSSetup to `false`.

When we create the placements and placement group objects in the ad server, we will set all related settings.

<br>


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
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/idealo.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

**Important**: It is very important, that you **do not** load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 

There is a way to load a part of the adlib asynchronically. In this case, only the most important scripts are loaded directly, to handle tasks like creating placeholders.
Other modules are then loaded on demand. If you plan to integrate the adlib with this scenario, please contact us at adtechnology@axelspringer.com to talk about the needed changes.


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
+                partners: false,
+                adPlacements: ["superbanner", "sky", "mrec"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/idealo.js"></script>
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
    "adPlacements": ["superbanner", "sky", "mrec", "mrec_btf"],
    "adSlotSizes": { 
        "superbanner": [{
            "minWidth": 1,
            "sizes": [[728, 90], [728, 600]]
        }], 
        "sky": [{
            "minWidth": 1,
            "sizes": [[160, 600], [120, 600], [300, 600]]
        }],
        "mrec": [{
            "minWidth": 1,
            "sizes": [[300,250]]
        }],
        "mrec_btf": [{
            "minWidth": 1,
            "sizes": [[300,250]]
        }],
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
    "adPlacements": ["mrec", "mrec_btf"],
    "adSlotSizes": { 
        "mrec": [{
            "minWidth": 1,
            "sizes": [[320,160], [300,300], [300,250]]
        }],
        "mrec_btf": [{
            "minWidth": 1,
            "sizes": [[320,160], [300,300], [300,250]]
        }],
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
                partners: false,
                adPlacements: ["superbanner", "sky", "mrec", "mrec_btf"],
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
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/idealo.js"></script>
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


## Testing on localhost

**Important**: Please don't try to test ads on Localhost. Ads will be not delivered on localhost without updates on your environment.

If you have no other choice but to test on localhost, you have to change your hosts file and map localhost with any domain _(for example "www.test.com")_, so that ad requests have a valid domain. 
Ad requests coming from localhost are always blocked.

<br>



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


