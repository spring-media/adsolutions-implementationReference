# Welcome to our implementation reference!

The goal of these documentations is to give you an idea on how the ad integration works and what you as a developer need to keep in mind.



## Table of contents

 - [Basic setup](#basic-setup)
    - [1. Include the AdLib](#1-include-the-adlib)
    - [2. AdSSetup - provide the config for the ad delivery](#2-adssetup---provide-the-config-for-the-ad-delivery)
    - [3. Provide Ad Slots](#3-provide-ad-slots)
 - [The AdSSetup - in detail](#the-adssetup---in-detail)
   



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

**Important**: It is very important, that you do not load the adlib asynchronically! Otherwise this will lead to [cumulative layout shifts](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) and delay the headerbidding a lotf, which will cost your page real money in unrealised profits. 


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


# The AdSSetup - in detail

Since the AdSSetup is a very important part of the ad integration on your page, it should be clear, what informations are included and what they mean.



<table>
<thead>
  <tr>
    <th>Attribute</th>
    <th>Explanation</th>
    <th>Sample Value</th>
    <th>Required</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>view</td>
    <td>Decides if the current page is on mobile (m) or desktop (d) viewport</td>
<td>

`"d" | "m"`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>partners</td>
    <td>Enable programmatic demand</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>adPlacements</td>
<td>

List every ad that you order from the ad server. You can find a visual illustration for the adPlacements [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-placements-overview).

**Important**: Please make sure, that you provide an adSlot for each placement, that you define here.


</td>
<td>

_mobile_
```javascript
[
    "banner",
    "mrec",
    "mrec_btf",
    "mrec_btf_2",
    "mrec_btf_3",
    "inpage"
]
```

_desktop_
```javascript
[
    "superbanner",
    "sky",
    "billboard",
    "mrec",
    "mrec_btf",
    "mrec_btf_2",
    "mrec_btf_3",
    "inpage"
]
```

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>adSlotSizes</td>
    <td>Specify the formats you like to have for each ad that you ordered in the 

`adSSetup.adPlacements`


 <br>

Read more about sizes [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#creative-sizes-reference).

</td>
<td>

```javascript

adSlotSizes: {

    "billboard": [{
        "minWidth": 799,
        "sizes": [[800, 250]]
    }, {
        "minWidth": 969,
        "sizes": [[970, 250], [800, 250]]
    }],

    "mrec": [{
        "minWidth": 1,
        "sizes": [[300, 250], [300, 600]]
    }],

    "mrec_btf": [{
        "minWidth": 1,
        "sizes": [[300, 250], [300, 600]]
    }]
}

```

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>placeholders</td>
<td>

Our answer on Google's CLS. Learn more about that topic and the setup possibilities for the placeholder object [here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md).

</td>
<td>

```javascript
placeholder: {
    disablePlaceholders: false,
    default: {	
        "border-color": "#EEEDE8",
        "background-color": "#F9F9F7",
        "admarkPosition": "bottom right",
        "color": "#BCBCBC",
        "font-size": "12px",
        "font-family": "Tahoma"
    },
    mrec: { 
        "background-color": "#FCBFFF"
    }
}
```

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>colorBg</td>
    <td>Allow or deny a change of the background color of your page by the ads</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
    
  <tr>
    <td>bgClick</td>
    <td>Allow or deny the clickability of the background of the page controled by the ads</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>hasVideoPlayer</td>
    <td>enable or disable partnerscripts like headerbiding for video</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>isArticle</td>
    <td>it shows us if the page is an article</td>
<td>

`true | false`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>pagename</td>
    <td>channel / article name from CMS - there has to be an existing pendant as 'Placement Group' in the ad server.</td>
<td>

`news_index` for channel pages and
`news_story` for article pages

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>target</td>
    <td>a list of key/values which are used for targeting</td>
<td>

`"value1;value2;key1=value1,value2;key2=value1,value2;"`

</td>
    <td>yes</td>
  </tr>
  <tr>
    <td>iabTax</td>
    <td>explanation</td>
    <td>sample</td>
    <td>no</td>
  </tr>
</tbody>
</table>

