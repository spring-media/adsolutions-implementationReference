# Ad Integration for play.bild.de


Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [3. Provide Ad Slots](#3-provide-ad-slots)
    - [4. Video Setup](#4-video-setup)
    - [5. Ads on Demand / Infinite Scrolling](#5-request-ads-on-demand--infinite-scrolling)
      - [Requesting multiple mrec_btf placements](#requesting-multiple-mrec_btf-placements)
      - [Check if ad sizes are defined](#check-if-ad-sizes-are-defined)
      - [Register the adInfo event](#register-an-event-listener-to-receive-information-from-ad-lib-per-ad-slot)
      - [Add an ad slot to receive the adserver response](#add-an-ad-slot-to-receive-the-adserver-response)
      - [Request an ad](#request-an-ad)
      - [Decide what to do with the ad Info](#decide-what-to-do-with-the-ad-info)
 - [QA and testing](#qa-and-testing)
    - [Testads](#testads)
    - [Human detection](#human-detection)
 - [Help](#help)
   

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
+       <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/play.bild.js"></script>
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
+                view: "m",
+                partners: true,
+                adPlacements: ["mrec", "mrec_btf", "mrec_btf_2", "mrec_btf_3"],
+                adSlotSizes: { ... },
+                placeholder: { ... },
+                colorBg: false,
+                bgClick: false,
+                hasVideoPlayer: true,
+                isArticle: true,
+                pageName: "demo_story",
+                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
+                iabTax: "IAB2,IAB2-1,1,32"
+            }
+        </script>
        
        <script type="text/javascript" src="cdn/pages/play.bild.js"></script>
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
                view: "m",
                partners: true,
                adPlacements: ["mrec", "mrec_btf", "mrec_btf_2", "mrec_btf_3"],
                adSlotSizes: { ... },
                placeholder: { ... },
                colorBg: false,
                bgClick: false,
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
      
+     <div id="mrecWrapper">
+         <div id="mrec"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```


And just like that, you already have a basic working ad integration on your page. If you would like to test the ad delivery, [here you can set a cookie](https://reports.asadcdn.com/testads.html) to receive some test ads via a test segment.

_If you no longer want to receive the test ads, you can always remove the cookie via the 'Remove Testads' button on the same page._


<br>




## 4. Video Setup

🚧 This section is still under construction 🚧

This section explains the parameters for Xandr Video Requests.
The video ad call starts with a static url part which is always the same: 
 
`https://ib.adnxs.com/ptv?member=7823&size=1x1&publisher=1000494`
 
 
## Parameters

| Parameter        | Value           | Note  |
| ------------- |:-------------| :-----|
|    &inv_code=    |    [insert placement name here]      |    *list of placements provided by MI;  for now use static value bild.de-mew-play_video-preroll only*      |
|    &vplaybackmethod=    |     3     |     *fixed value; 3=Click-to-play*     |
|    &kw_vidBildAdlevel=    |     [so-called adlevel]     |     *you should get value from Bild feed, e.g. unterhaltung or politik*     |
|    &kw_misc=    |     [so-called taxonomie]     |     *you should get values from Bild feed, e.g. fischer_helene,schlager,tournee*     |
|    &vwidth=    |    [player width in px]      |     *leave empty if value can't be passed; don't pass zero*     |
|    &vheight=    |    [player height in px]      |     *leave empty if value can't be passed; don't pass zero*     |
|    &kw_vduration=    |     [duration content video in seconds]     |     *you should get values from Bild feed; leave empty if you don't have value*     |
|    &referrer=    |     [encoded URL where the ad will be rendered]     |  *e.g. https%3A%2F%2Fplay.bild.de%2F*        |


## GDPR Consent Parameters

| Parameter        | Value           | Note  |
| ------------- |:-------------| :-----|
|    &gdpr=     |    1     |   *1 = yes = GDPR applies*     |
|    &gdpr_consent=     |    [GDPR Consent String]      |        |


## Example
[https://ib.adnxs.com/ptv?member=7823&inv_code=bild.de-desktop-regio_video-preroll&vplaybackmethod=3&kw_vidContentId=70136844&kw_misc=Hannover_regional,Coronavirus,Neuwagen&vwidth=993&vheight=1117&kw_vduration=74&referrer=https%3A%2F%2Fwww.bild.de%2Fvideo%2Fclip%2Fhannover-regional%2Fneuwagen-dicht-an-dicht-keine-fahrzeugauslieferung-wegen-corona-70136844.bild.html](https://ib.adnxs.com/ptv?member=7823&size=1x1&publisher=1000494&inv_code=bild.de-mew-play_video-preroll&&vplaybackmethod=3&kw_vidBildAdlevel=unterhaltung&kw_misc=fischer_helene,schlager,tournee&vwidth=1024&vheight=576&kw_vduration=132&referrer=https%3A%2F%2Fplay.bild.de%2F&gdpr=1&gdpr_consent=CPpzHMAPpzHMAFZABCENC-CgAP_AAAAAAAYgIcpZ_D7VbWFC-f59aPsgOYxXVMCSAuQCCACAA2ABgAKQcDwCkmAaNESgBgACGQAAoRJBIAIEDAEECUAAYAAEAAGgAAAEhAAIIABAgBEAAAIYAAoCAAAAAACIwAAREAAAmRgYA8LmGEBAxAAQIAAQgAABAAAAAgMAAAAIAAIAAAAAAAgAAAAAAAIAAAEgkCoABYAFQAMgAcAA8ACAAGQANAAeQBDAEUAJgATwAqgBvADmAH4AQgAhgBEACWAFKALcAYYA9oB-AH6ARwAkwBKQC5gGKANwAcQBIgCdgFDgKRAXmAwYBk4DggHjgQ5CAC4AHAAeABsAEgAPwCDgE0AOqAlYBTYDIQG0BoBYAXABDAD8AIKASYA6oCRAE7AKRAZOAzwMACAOoApsRAIAEMAPwAkwB1QEiAJ2AUiAycQABABIKgDABDACYAFwAjgC8wGeCgAQBBQDqjIAoAQwAmAEcAXmAzwYACALEAdUdAzAAWABUADIAHAAQAAyABoADwAH0AQwBFACYAE8AKsAXABdADEAG8AOYAfgBDACIAEsAKMAUoAsQBbgDDAGiAPaAfgB-gEWgI4AjoBJgCUgFiALmAYoA3ABxADqAIvASIAnYBQ4C8wF9AMGAZOAywBqoDxwIcjgC0ADgAPAAuACQAHIAPwAoADNAILAQcBCACIgE0AL0AYEA14B0gDqgJWAU2ArsBkIDJgG0EICgACwAMgBDACYAFUALgAYgA3gClAFiARwAlIBcwDFAHUASIAycBngDVQHjkAAgAzQCCgFiAOqSgNAALAAyABwAHgARAAmABVAC4AGIAQwAiABRgClAFuAPwAjgBcwDFAG4AOoAi8BIgC8wGTgMsAZ4SADgAXAByAM0Ag4BrwDqgJWKQKAAFgAVAAyABwAEAAMgAaAA8gCGAIoATAAngBSACqAGIAOYAfgBDACIAFGAKUAWIAtwBowD8AP0Ai0BHAEdAJSAXMAxQBuAEXgJEATsAocBeYC-gGTgMsAZ4A8coAPAAuACQAHIAPwA2gDNAIOAWIAuoBrwDqgKbAV2AyYBwQA.YAAAAAAAAAAA)

<br>
<br>


## 5. Request Ads on demand / Infinite Scrolling

> This section shows you how to call ads on demand for infinite scrolling.

<br>


### Requesting multiple mrec_btf placements

Per default our \_btf placements are always copies of the initial \_btf placement in the adSSetup. <br>
_(if needed, you can specify for example mrec_btf_8 in the adSSetup with other sizes if you need to use different sizes on one specific \_btf placement)_
<br><br>
You can repeat the btf placements as much as you want. Please use the following schema:

**Example for 3 Medium Rectangle btf**

 - mrec_btf
 - mrec_btf_2
 - mrec_btf_3


<br>

### Check if ad sizes are defined

The ad-lib respects the sizes defined in the adSSetup until the ad-calls are called. In order to ensure that sizes for the actual ad-request are properly set, you may redefine them whenever necessary.<br>
For instance, in the following example, we'll check if all sizes have already been included and add any missing dimensions:


```html
<script>
    if (adSSetup.adSlotSizes["mrec_btf_2"]) {
        adSSetup.adSlotSizes["mrec_btf_2"][0].sizes = adSSetup.adSlotSizes["mrec_btf_2"][0].sizes.concat([
            [300, 250], 
            [300, 300], 
            [320, 480], 
            [300, 600]
        ]);
    } else {
        adSSetup.adSlotSizes["mrec_btf_2"] = [{
            minWidth: 1,
            sizes: [
                [300, 250], 
                [300, 300], 
                [320, 480], 
                [300, 600]
            ]
        }]
    }
</script>
```

<br>

### Register an Event Listener to Receive Information from Ad-lib per Ad Slot

The adlib enables you to retrieve useful information for each ad slot via the "adInfo" event listener. This event may provide some data points that you can then react to, or in some cases explicitly not react to.

You can set the event listener like in the following example:

```html
<script>
window.addEventListener("adInfo", function(adSlot) {
    console.log(adSlot);
});
</script>
```

<br>

### Add an ad slot to receive the adserver response
The adservers framework works with the HTML attribute id to render its codes,
so we need a node for each adplacement to process.
This example shows a node for direct integration into the HTML, but you may also append it by javascript.
It uses a wrapper node element that may be styled (your space), please not use CSS directly on the adslot itself (our space):

```html
<div id="mrec_btf_2_wrapper" class="mrec_btf_Wrapper" style="float:right">
    <div id="mrec_btf_2"></div>
</div>
```

For further information on this feature please have a look into our [adInfo reference](../publisher-loadHandler-reference.md).


<br>


### Request an ad
Since we now have set all preparations we will order an ad one per adslot.
This example shows an cross-browser solution to do so for the adslot div#betad_2:

```html
<script>
    var ev;
    try {
        ev = new CustomEvent('renderAd', {'detail': 'mrec_btf_2'});
    }catch(err){
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('renderAd', true, true, {'detail': 'mrec_btf_2'});
    }
    document.dispatchEvent(ev);
</script>
```


<br>

### Decide what to do with the ad Info
The adlib will now start an ad-request and after it finished, every listener will be informed.
If needed, you can now act on the info of the adResponse. This might be interesting for handling ad-markers. _(Some mobile templates bring an own ad marker with the ad response)_ 

```html
<script>
window.addEventListener("adInfo", function(adSlot) {
    var adResponse = adSlot.detail;
    if (adResponse.hasMarker == true) {
        // the ad comes with its own ad marker -
        // you can now hide the publisher ad marker
    }
});
</script>
```


<br>

-----



# QA and testing

**Important**: Please don't try to test ads on localhost. Ads will be not delivered on localhost.



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



