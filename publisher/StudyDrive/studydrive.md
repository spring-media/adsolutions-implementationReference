
# StudyDrive Ad Integration Guide

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [3. Provide Ad Slots](#3-provide-ad-slots)
 - [Publisher-specific integration](#publisher-specific-integration)
    - [The adSSetup - parameters and what to keep in mind](#the-adssetup---parameters-and-what-to-keep-in-mind)
    - [Pagename Structure](#pagename-structure)
    - [Delivering Course Teaser (native)](#delivering-course-teaser)
    - [Request ads on demand](#request-ads-on-demand)
    - [Connection to Power BI](#connection-to-power-bi)
 - [InApp Ad Integration](#inapp-ad-integration)
 - [QA and testing](#qa-and-testing)
    - [Testads](#testads)
    - [Ad Alert](#adalert)
    - [Forced Ad Formats](#forced-ad-formats)
    - [Human detection](#human-detection)
   

<br>


-----

# Basic setup


Basically there are only three important steps to implement a basic ad integration:

<br>


## 1. Include the AdLib

> Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.
> During the onboarding process we provide you a tailor-made version for your page that takes many different settings and special requirements of the site into account.


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/studydrive.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      <div class="your-content">...</div>
      
    </body>
</html>
```

**Important**: It is very important, that you **do not** load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lot, which will cost your page real money in unrealised profits. 


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


<br>


-----


# Publisher-specific integration

> The content above describes a sample integration, but every integration is different and has its own challenges.<br>
> Below we will learn what particular challenges we have in this project and how we will solve them.

<br>


## The adSSetup - parameters and what to keep in mind

You can find a detailed overview with explanation of all parameters for the adSSetup [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

<br>

**Important**: Be sure that you only order placements in the adSSetup.adPlacements, for which you know that you have a matching ad slot on your page, where the delivered ad can be rendered in.

<br>

**BlockTrack Tag Integration**

Please include the BlockTrack Tag at the end of the page and make sure it gets loaded after adSSetup is defined.
You can find the code to inlcude [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-blocktrack-reference.md).

<br>


## Pagename structure

You can have a look into [this document](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/pagename-structure.md), to get a basic understanding on how pagenames & keyword targetings work.

Currently, the discussed pagenames are as following:

 - newsfeed
 - groups
 - course
 - documents_index
 - documents_page
 - flashcards_index
 - flashcards_page
 - company_profile
 - user_profile
 - user_profile_edit
 - notifications

<br>

For an overview of our recommended placements and associated sizes, please have a look into [this document](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/StudyDrive/channel-structure.md).

<br>



## Delivering Course Teaser (native)

The course teasers will be delivered using a native JSON feed with the special size `427x23`. How this works, is described [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/peculiar/nativeTrigger.md).<br>
Basically, we deliver a JSON feed for these native ads for the specific `427,23` size. When these ads are implemented on your page, you need to set an EventListener on our **adInfo** event and react to the hasAd property for this specific contId.

We strongly recommend using a fallback, in case some users are visiting your pages with an adblocker.

<br>



## Request ads on demand

If you have sections on your page with very long content, your can use a dynamic set of btf _(= "below the fold")_ placements.
When you see that the user is scrolling near the next possible adSlot, you can create a new ad slot in your page e.g. "mrec_btf_2" and then request a new ad for this new included placement.<br><br>

The "btf" placements in the Browser are loaded with lazy loading.<br>
Those ads will be rendered only when the placement is 100px under the viewport.
<br>

You can read our guide for [on-demand-ads](https://github.com/spring-media/adsolutions-implementationReference/blob/master/peculiar/onDemandAd-integration.md) for more in-depth info about the required actions.

<br>



## Connection to Power BI

Currently we're not aware of a plugin-type direct connection between Xandr reports and Power BI. However, since Xandr has a powerful API, you can build this connection on your own and therefore meet all requirements you have in your specific use cases.<br>
You can find the documentation of the Xandr API here: https://docs.xandr.com/bundle/xandr-api/page/welcome.html


<br>



-----


# InApp Ad Integration

For an in-depth documentation, please have a look into our [standard Xandr InApp Ad Integration Guide](https://github.com/spring-media/adsolutions-implementationReference/blob/master/InApp%20Ad%20Integration/standard-xandr-inapp-integration.md). 

<br>
Please use the publisherID  "<code>2064676</code>"  for your inApp ad calls.<br>
The memberId for your Xandr seat is "<code>13513</code>"<br>
<br>

For an overview of our recommended placements and associated sizes, please have a look into [this table](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/StudyDrive/channel-structure.md#android--ios-apps).

<br>


-----



# QA and testing

**Important**: Please don't try to test ads on Localhost. Ads will be not delivered on localhost.



## Testads

If you would like to test the ad delivery, you can set a special cookie here: https://reports.asadcdn.com/testads.html to receive some test ads via a test segment.
<br>

> _If you no longer want to receive the test ads, you can always remove the cookie via the 'Remove Testads' button on the same page._

<br>


## AdAlert

By writing "adalert" into the page where the adlib is integrated, you can trigger a debugging feature, that shows you additional information regarding page related settings (such as CMP settings, keywords, pagename, etc.) and delivered ads (creative id's, ...).
Please make sure, that the page content is in focus (a simple click in the page's background helps, if its not working on the first time) while writing "adalert".

You can find more information on the adalert here: <br>
https://github.com/spring-media/adsolutions-implementationReference/blob/master/QA/adalert.md

<br>

## Forced Ad Formats

If you like to test pages with one specific forced ad format, please contact us - we can create special preview urls for certain ads, which do exactly that.

<br>


## Human detection

It can happen, that the adserver does not deliver ads, when the user emulates devices in the browser.

In general the detection tries to find non human or potential malicious requests (e.g. making adcalls from localhost, making many requests within the same second, uncommon request headers, ...).

<br>


