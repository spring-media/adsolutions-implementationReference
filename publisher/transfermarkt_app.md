# Transfermarkt.de - App


### Table of contents


1. [Changelog](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#1-changelog)
1. [Introduction](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#2-introduction)
1. [General](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#3-general)
1. [Additional informations for the following adSSetup](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#4-additional-informations-for-the-following-adssetup-object)
1. [Desktop Integration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#5-mobile-integration)
   1. 5.1 [Placements](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#51-placements)
   1. 5.2 [Home](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#52-home)
   1. 5.3 [Artikel](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#53-artikel)
   1. 5.4 [Profile | Live | MeinVerein | Navi-Start](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#54-profile--live--meinverein--navi-start)
   1. 5.5 [Statistiken / Suche](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#55-statistiken--suche)
   1. 5.6 [MeinVerein](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#56-meinverein)
1. [Important Notes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#6-important-notes)
1. [Help](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher/transfermarkt_app.md#7-help)



### 1. Changelog

Date | Change
------------ | -------------
*27.02.2019* | *initial commit with adSSetup object for mobile and desktop*



--------


### 2. Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Xandr.


### 3. General

Please include the following script in the `<head>` of the website:  ```https://acdn.adnxs.com/as/1h/pages/newPublisher.js```.

**Test Ads** - [Here](https://adtechnology.axelspringer.com/testads.html) do you get an Xandr segment for test ads - so you can test you integration. On the same site you can disable the segment to see 'normal' ads.
Please be sure that your browsers accepts 3th party cookies.
   
**General Display Reference** - [Here](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website) do you find a general overview for the whole ad integration process.
   
________________________________
   
   
### 4. Additional informations for the following adSSetup object
   
* "Pagename" schema
	* Home Site --> "home_index"
	* Channel, e.g. sport --> "sport_index"
	* Sub-Channel e.g. soccer --> "sport.soccer_index"
	* Article e.g. soccer article --> "sport.soccer_story"

* "Target": every editorial keyword or custom target
	* you can use stand alone keywords with semicolon ; separately
	* key/values are also supported. key=value1,value2;
	* please ensure to end the line with a semicolon





# 5. Mobile Integration


### 5.1 Placements

| Placement Name|Xandr|
| ------------- | ----- |
|Banner|banner|
|Medium Rectangle|mrec|
|Medium Rectangle|mrec_btf|
|Richmedia / Outstream|inpage|


You can repeat the btf placements as much as you want. Please use the following schema:

*Example for 3 Medium Rectangle btf*

* mrec_btf
* mrec_btf_2
* mrec_btf_3
   
   
   
Take a look on [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website) and [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) for more information.




## 5.2 Home


Include the following object in your <head>-Tag.

```javascript
<script type="text/javascript">
adSSetup = {
	view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
	partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
	adPlacements: ["banner","mrec_btf","mrec_btf_2","mrec_btf_3","mrec_btf_4","inpage"], // Every Ad (mrec_btf_2 - n / billboard_btf_2 - n / sky_btf_2 - n) on the page must be listed here
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,150]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,150],[300,600],[1000,300],[320,480]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[1000,300]]
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


## 5.3 Artikel 


Include the following object in your <head>-Tag.

```javascript
<script type="text/javascript">
adSSetup = {
	view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
	partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
	adPlacements: ["banner","mrec_btf","mrec_btf_2","inpage"], // Every Ad (mrec_btf_2 - n / billboard_btf_2 - n / sky_btf_2 - n) on the page must be listed here
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,150]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,150],[300,600],[1000,300],[320,480]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360]]
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


## 5.4 Profile | Live | MeinVerein | Navi-Start


Include the following object in your <head>-Tag.

```javascript
<script type="text/javascript">
adSSetup = {
	view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
	partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
	adPlacements: ["banner","mrec_btf","mrec_btf_2","inpage"], // Every Ad (mrec_btf_2 - n / billboard_btf_2 - n / sky_btf_2 - n) on the page must be listed here
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,150]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,150],[300,600],[1000,300],[320,480]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
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


## 5.5 Statistiken / Suche


Include the following object in your <head>-Tag.

```javascript
<script type="text/javascript">
adSSetup = {
	view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
	partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
	adPlacements: ["banner","mrec_btf","inpage"], // Every Ad (mrec_btf_2 - n / billboard_btf_2 - n / sky_btf_2 - n) on the page must be listed here
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,150]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,150],[300,600],[1000,300],[320,480]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
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

## 5.6 MeinVerein


Include the following object in your <head>-Tag.

```javascript
<script type="text/javascript">
adSSetup = {
	view: "m", // has to fit the design of the page, please use 'm' for mobile and 'd' for desktop
	partners: true, //Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue
	adPlacements: ["banner","mrec_btf","mrec_btf_2"], // Every Ad (mrec_btf_2 - n / billboard_btf_2 - n / sky_btf_2 - n) on the page must be listed here
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,150]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,150],[300,600],[1000,300],[320,480]]
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


   
### 6. Important Notes

- For Intext Outstream and for Richmedia we just need one placement with Xandr.
- __IMPORTANT__ Please place the "inpage" placement in the required position for InText. Take care that we need the whole website wide for it.



### 7. Help

If you have some question don't hesitate to contact us:


__Carlos Bracho__
 
  Head of AdTechnology
  Spring
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de



