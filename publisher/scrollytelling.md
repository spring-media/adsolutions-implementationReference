# Scrollytelling - Ad Integration Guide

Welcome to your Ad Integration documentation! 
In this document you will learn how to implement our adlib in your site to deliver ads with it.

<br>


## Table of contents

 - [Ad Integration Steps for Scrollytelling](#ad-integration-steps-for-scrollytelling)
    - [Use our widget integration script](#use-our-widget-integration-script)
    - [Provide Ad Slots](#provide-ad-slots)
 - [Advertisement Labeling](#advertisement-labeling)
 - [Next Steps](#next-steps)
 - [QA and testing](#qa-and-testing)
    - [Testads](#testads)
    - [Human detection](#human-detection)
 - [Help](#help)
   

<br>


-----



# Ad Integration Steps for Scrollytelling

## Use our widget integration script

> As Scrollytelling is a special case with two scenarios (standalone and embed), we prepared a script that will load the adlib and create the adSSetup for you - matching both scenarios:


```html
<script>
    (() => {
        const slots = ["widget", "widget_2"], pageName = "scrollytelling_story", targets = "",
            framed = globalThis === window.top,
            windowWidth = document.documentElement?.clientWidth || document.body?.clientWidth || window.innerWidth;
        let adlibWindow = null, frame = globalThis, view;

        const loadAdLibrary = () => {
            const adlib = document.createElement("script");
            adlib.src = "https://www.asadcdn.com/adlib/pages/bild.js";
            document.head.appendChild(adlib);
        }

        const setSize = () => {
            window.adSSetup.adSlotSizes.widget = [{
                "minWidth": 1,
                "sizes": [[300, 600], [320, 480], [320, 460], [300, 300], [300, 250]]
            }, {
                "minWidth": 727,
                "sizes": [[728, 90], [970, 250], [800, 250]]
            }];
        }

        if (windowWidth >= 728) {
            view = "d";
        } else {
            view = "m";
        }

        while (frame) {
            try {
                if (frame.frames["__asadlibLocator"]) {
                    adlibWindow = frame;
                    break;
                }
            } catch {
            }
            if (frame === window.top) {
                break;
            }
            frame = frame.parent;
        }

        if (adlibWindow === globalThis) {
            setSize();
            slots.forEach(slot => {
                globalThis.adSSetup.adPlacements.push(slot);
                document.dispatchEvent(new CustomEvent('renderAd', {
                    'detail': slot
                }));
            });
        } else if (adlibWindow && framed) {
            window.addEventListener("message", (msg) => {
                if (msg?.data?.message === "pageSet") {
                    window.adSSetup = msg.data.data;
                    window.adSSetup.adPlacements = slots;
                    setSize();
                    loadAdLibrary();
                }
            }, false);
            window.top.postMessage('sendPageSet:;:' + window.name, '*');
        } else {
            globalThis.adSSetup = {
                view: view,
                partners: true,
                adPlacements: slots,
                adSlotSizes: {},
                placeholder: {},
                bgClick: true,
                hasVideoPlayer: false,
                isArticle: true,
                pageName: pageName,
                target: targets
            }

            setSize();
            loadAdLibrary();
        }
    })();
</script>
```

<br>
<br>

Most important for you is the first line in the above script

```javascript
const slots = ["widget", "widget_2"], pageName = "scrollytelling_story", targets = "",
```

<br>

**slots**
<br>

In `slots`, you define the adSlots you have on the page. If your article is longer and has more adSlots, you have to list them here, so that they will be "ordered" with the ad request.
Since we use only `widget`and `widget_btf`, we only define the sizes (which decide the available ad formats) for the `widget` - every `widget_{n}` slot will be a clone of the first `widget` slot and will have the same size definitions.

<br>

**pagename**
<br>

Another important part is the `pagename`. This attribute indicates the environment - if you are running standalone, you will use "scrollytelling_story" - if you're running as embed, you will use the pagename of the parent page.<br>
**The script handles this for you.**

<br>
<br>

The script does all the heavy lifting for you, including:
 - loading the adlib
 - detecting the viewport and setting allowed ad formats (sizes) accordingly
 - detecting the environment (standalone vs. embed)
 - getting all relevant adSSetup settings from parent, when running as embed

<br>
<br>

This is what the script will build for you. 

<br>


```diff

<html>
    <head>
        <title>Scrollytelling Widget</title>
        
+        <script type="text/javascript">
+            adSSetup = {
+                view: "d",
+                partners: true,
+                adPlacements: ["widget", "widget_2"],
+                adSlotSizes: { ... },
+                placeholder: { ... },
+                colorBg: true,
+                bgClick: true,
+                hasVideoPlayer: false,
+                isArticle: true,
+                pageName: "scrollytelling_story",
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

If you want to learn more about the adSSetup object, you can find a detailed overview with explanation of all parameters [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/general/adSSetup-in-detail.md).

<br>

**Important**: 

 - Make sure, that the adSSetup Object is ready, when the adlib is loaded, so that we can use your configuration to make the call to the ad server.
 - Be sure that you only order placements in the adSSetup.adPlacements, for which you know that you have a matching ad slot on your page, where the delivered ad can be rendered in.
 - In the adPlacements array, you defined which adslots you have on your page - for example "widget", "widget_2", "widget_3" (you can continue like this, depending on how long your content is).
 - In the adSlotSizes object you defined the sizes for the "widget" adslot. Since we only have "widget" and "widget_{n}" slots on the page, we use the sizes of the first slot to clone the others.


<br>
<br>



## Provide Ad Slots

> You as publisher need to provide us a container for each ad, that you ordered via the adSSetup object. The delivered ads will be rendered in these Ad Slots, so it is very important that there is a container for each ad on the page. The Ad Slots will need the ad type as id and have to be completely unstyled.
> If you need styling around the ad, you can set a wrapper around the Ad Slot and style this wrapper instead.


```diff

<html>
    <head>
        <title>Scrollytelling</title>
        
        <script type="text/javascript">
            adSSetup = {
                view: "d",
                partners: true,
                adPlacements: ["widget", "widget_2"],
                adSlotSizes: { ... },
                placeholder: { ... },
                colorBg: true,
                bgClick: true,
                hasVideoPlayer: false,
                isArticle: true,
                pageName: "scrollytelling_story",
                target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
            }
        </script>
        
        <script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/bild.js"></script>
    </head>
    <body>

      <div class="your-content">...</div>
      
+     <div id="widgetWrapper">
+         <div id="widget"></div>
+     </div>

      <div class="your-content">...</div>

+     <div id="widget_2Wrapper">
+         <div id="widget_2"></div>
+     </div>

      <div class="your-content">...</div>
      
    </body>
</html>
```


<br>



# Advertisement Labeling

As a wish from the Media Impact Product team - it would be great if you could implement a proper advertisement labeling before and after each adslot to make a clear switch between the content and ads.
For example:

Werbung <br>
[AdSlot] <br>
Jetzt gehts weiter mit dem Artikel

<br>

If you have questions regarding the advertisement labeling, please reach out to Jakob Stoltmann.



<br>

# Next steps

 - Check for PUR status - if PUR is active, we are not allowed to load the adlib.
 - Before loading the adlib, wait for CMP. Make sure that the CMP is loaded as early as possible.
 - Load the provided script after the CMP and as early as possible, too. Make sure that the adlib is **never** loaded asynchronously.
 - If scrollytelling is used as an embed on the page, check if you are loaded in an iFrame or directly on the page. If you're directly on the page, you should be able to get all the relevant ad values from the parent pages' adSSetup object. Thats what the provided script will do for you.


<br>



# QA and testing

**Important**: Please don't try to test ads on Localhost. Ads will not be delivered on localhost.



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



