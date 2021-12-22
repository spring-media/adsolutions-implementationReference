# Welcome to our implementation reference!

The goal of these documentations is to give you an idea on how the ad integration works and what you as a developer need to keep in mind.


## Basic setup


Basically there are only three important steps to implement a basic ad integration:

### 1. Include the AdLib

> Our AdLib is the heart of the ad delivery. There are many features and processes, that are done by the adlib and of course, you need to include the script on your page to get a working ad delivery.
> During the onboarding process we create a tailor-made version for your page that takes many different settings and special requirements of the site into account.


```diff

<html>
    <head>
        <title>Your great website</title>
+       <script type="text/javascript" src="cdn/pages/website.js"></script>
    </head>
    <body>

      <div class="your-content"></div>
      <div class="your-content"></div>
      
    </body>
</html>
```

**Important**: It is very important, that you do not load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lotf, which will cost your page real money in unrealised profits. 


### 2. AdSSetup - provide the config for the ad delivery

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

      <div class="your-content"></div>
      <div class="your-content"></div>
      
    </body>
</html>
```

Make sure, that the adSSetup Object is ready, when the adlib is loaded, so that we can use your configuration to make the call to the ad server.


### 3. Provide Ad Slots

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

      <div class="your-content"></div>
+     <div id="billboardWrapper">
+         <div id="billboard"></div>
+     </div>
      <div class="your-content"></div>
      
    </body>
</html>
```
