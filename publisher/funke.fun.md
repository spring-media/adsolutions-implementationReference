# Funke.fun

In this documentation you find the placement details for your Website.  


## AdLib

Please use the following JS for the adLib: ```https://www.asadcdn.com/adlib/pages/funkefun.js```



### Table of contents

1. [Introduction](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#1-introduction)
1. [General](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#2-general)
1. [Additional informations for the following adsSetup](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#3-additional-informations-for-the-following-adssetup-object)
1. [Desktop Integration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#4-desktop-integration)
    1. 4.1 [Placements](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#41-placements)
    1. 4.2 [adsSetup](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#42-adssetup)
        1. 4.2.1 adsSetup for /gewinnspiele
        1. 4.2.2 adsSetup for /gewinnspiele/detail and /gewinnspiele/spiel 
1. [Mobile Integration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#5-mobile-integration)
    1. 5.1 [Placements](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#51-placements)
    1. 5.2 [adsSetup](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#52-adssetup)
        1. 5.2.1 adsSetup for /gewinnspiele
        1. 5.2.2 adsSetup for /gewinnspiele/detail and /gewinnspiele/spiel 
1. [Important Notes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#6-important-notes)
1. [Help](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/funke.fun.md#7-help)



--------

### 1. Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer.
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Appnexus.


### 2. General

Please include the following script in the `<head>` of the website:  ```https://www.asadcdn.com/adlib/pages/funkefun.js```.

**Test Ads** - [Here](https://adtechnology.axelspringer.com/testads.html) do you get an AppNexus segment for test ads - so you can test you integration. On the same site you can disable the segment to see 'normal' ads. Please be sure that your browsers accepts 3th party cookies.

**General Display Reference** - [Here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website) do you find a general overview for the whole ad integration process.

________________________________

### 3. Additional informations for the following adsSetup object

* "Pagename" schema
    * Home Site --> "home_index"
    * Channel, e.g. sport --> "sport_index"
    * Sub-Channel e.g. soccer --> "sport.soccer_index"
    * Article e.g. soccer article --> "sport.soccer_story"

* "Target": every editorial keyword or custom target
    * you can use stand alone keywords with semicolon ; separately
    * key/values are also supported. key=value1,value2;
    * please ensure to end the line with a semicolon



# 4. Desktop Integration


### 4.1 Placements

| Placement Name|Xandr|
| ------------- | ----- |
|Superbanner|superbanner|
|Sky|sky|
|Billboard|billboard|
|Billboard_btf|billboard_btf|
|Medium Rectangle|mrec|
|Medium Rectangle|mrec_btf|
|Richmedia / Outstream|inpage|


You can repeat the btf placements as much as you want. Please use the following schema:

*Example for 3 Medium Rectangle btf*

* mrec_btf
* mrec_btf_2
* mrec_btf_3



Take a look on [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website) and  [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) for more information.


### 4.2 adsSetup

#### 4.2.2 adsSetup for /gewinnspiele

Include the following object in your head-Tag.

```javascript
<script type="text/javascript">
adsSetup = {
    view: "d", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
    partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
    adPlacements: ["billboard", "mrec"],
    adSlotSizes: {
        "billboard": [{
           "minWidth": 1,
           "sizes": [[970,250], [800,250], [3,3], [728,600], [728,90], [1000,600]]
        }],
        "mrec": [{
           "minWidth": 1,
           "sizes": [[300,250]]
        }],
    },

    /* page configuration */
    colorBg: true, // enable/disable coloring of the page-background
    bgClick: true, // enable/disable click on page-background
    stickySky: true, // enable/disable stickiness for skyscraper
    hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding for video
    isArticle: true, // it shows us if the page is an article
    pageName: "demo_story", // channel/article name from CMS
    target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
}


</script>
```


#### 4.2.2 adsSetup for /gewinnspiele/detail and /gewinnspiele/spiel

Include the following object in your head-Tag.

```javascript
<script type="text/javascript">
adsSetup = {
    view: "d", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
    partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
    adPlacements: ["billboard", "mrec", "sky"],
    adSlotSizes: {
        "billboard": [{
           "minWidth": 1,
           "sizes": [[970,250], [800,250], [3,3], [728,600], [728,90], [1000,600]]
        }],
        "mrec": [{
           "minWidth": 1,
           "sizes": [[300,250], [320,150], [320,100], [320,50], [320,75], [320,160], [320,250], [300,300]]
        }],
        "sky": [{
           "minWidth": 1,
           "sizes": [[160,600], [120,600], [300,600], [500,1000], [1000,1000]]
        }]
    },

    /* page configuration */
    colorBg: true, // enable/disable coloring of the page-background
    bgClick: true, // enable/disable click on page-background
    stickySky: true, // enable/disable stickiness for skyscraper
    hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding for video
    isArticle: true, // it shows us if the page is an article
    pageName: "demo_story", // channel/article name from CMS
    target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
}


</script>
```



# 5. Mobile Integration

### 5.1 Placements

| Placement Name|Appnexus|
| ------------- | ----- |
|Reminder|banner|
|Medium Rectangle|mrec|
|Medium Rectangle 2|mrec_btf|
|Medium Rectangle 3|mrec_btf_2|
|Richmedia / Outstream|inpage|



You can repeat the btf placements as much as you want. Please use the following schema:

*Example for 3 Medium Rectangle btf*

* mrec_btf
* mrec_btf_2
* mrec_btf_3



Take a look on [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website) and  [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) for more information.



### 5.2 adsSetup


#### 5.2.1 adsSetup for /gewinnspiele

Include the following object in your head-Tag.

```javascript
<script type="text/javascript">
adsSetup = {
    view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
    partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
    adPlacements: ["banner", "mrec", "mrec_btf"],
    adSlotSizes: {
        "banner": [{
           "minWidth": 1,
           "sizes": [[320,50], [320,75], [320,80], [320,100], [320,250]]
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

    /* page configuration */
    colorBg: true, // enable/disable coloring of the page-background
    bgClick: true, // enable/disable click on page-background
    stickySky: true, // enable/disable stickiness for skyscraper
    hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding for video
    isArticle: true, // it shows us if the page is an article
    pageName: "demo_story", // channel/article name from CMS
    target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
}


</script>
```


#### 5.2.2 adsSetup for /gewinnspiele/detail and /gewinnspiele/spiel



Include the following object in your head-Tag.

```javascript
<script type="text/javascript">
adsSetup = {
    view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
    partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
    adPlacements: ["banner", "mrec", "mrec_btf"],
    adSlotSizes: {
        "banner": [{
           "minWidth": 1,
           "sizes": [[320,50], [320,75], [320,80], [320,100], [320,250]]
        }],

        "mrec": [{
           "minWidth": 1,
           "sizes": [[300,250], [320,150], [320,100], [320,50], [320,75], [320,160], [320,250], [300,300]]
        }]
    },

    /* page configuration */
    colorBg: true, // enable/disable coloring of the page-background
    bgClick: true, // enable/disable click on page-background
    stickySky: true, // enable/disable stickiness for skyscraper
    hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding for video
    isArticle: true, // it shows us if the page is an article
    pageName: "demo_story", // channel/article name from CMS
    target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
}


</script>
```


 

## Important notes

- For Intext Outstream and for Richmedia we just need one placement with Xandr.
- __IMPORTANT__ Please place the "inpage" placement in the required position for InText. Take care that we need the whole website wide for it.

## Help

If you have some question don't hesitate to contact us:


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  
