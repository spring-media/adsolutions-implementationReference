# Integration - Online Desktop & Mobile Advertisement


**Table of Contents**  

- [Introduction](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#introduction)
- [Overview](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#overview)
- [Ad Integration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-integration)
	- [`<head>` elements](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#elements-in-the-head-of-the-website)
		- [1. Viewport](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#1-set-the-viewport-of-the-website-use-for-desktop-d-and-for-mobile-m)
		- [2. 3th party scripts.](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#2-switch-for-the-3th-party-scripts-we-strictly-recommend-to-set-it-as-false-only-on-pages-for-directsales-campaign-only-the-max-out-the-revenue)
		- [3. Placements](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)
			- [Desktop](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop)
				- [Mandatory](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mandatory)
				- [Optional](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#optional)
			- [Mobile](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-mobile)
				- [Mandatory](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mandatory-1)
				- [Optional](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#optional-1)
		- [4. Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)
				-[Desktop](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#desktop-1)
				-[Mobile](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mobile-1)
			- [Placement's Sizes Reference](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-sizes-for-every-placement)
				- [For Desktop](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1)
				- [For Mobile](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-mobile-1)
		- [5. Page configuration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#5-page-configuration)
			- [colorBG](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#colorbg-enabledisable-coloring-of-the-page-background)
			- [bgClick](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#bgclick-enabledisable-click-on-page-background)
			- [stickySky](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#stickysky-enabledisable-stickiness-for-skyscraper)
			- [pageName](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#pagename-it-is-the-name-of-the-channel-or-article-in-cms)
			- [target](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#target-every-editorial-keyword-or-custom-target)
		- [6. AdLib](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#6-adlib)
- [Ad Placements in the `<body>`](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-placements-in-the-body-of-the-website)
		- [Example](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#example)
	- [Ad Placements Overview](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#ad-placements-overview)
		- [Display](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#display)
			- [superbanner](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#superbanner)
			- [sky](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#sky)
			- [billboard](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#billboard)
			- [mrec](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mrec)
			- [inpage](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#inpage)
		- [Mobile](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mobile)
			- [banner](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#banner)
			- [mrec](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mrec-1)
			- [inpage](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#inpage-1)
			- [mrec_btf](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#mrec_btf)
- [Creative Sizes Reference](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#creative-sizes-reference)
- [QA and Testing](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#qa-and-testing)
- [Special Reports](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#special-features)
			- [Lazy Loading](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#lazy-loading)



## Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Xandr.

## Overview

In the following you will find an overview of the necessary components which must be implemented to deliver and display the advertising media.

## Ad Integration

 Elements in the `<head>` of the website:

`<script type="text/javascript">`

# 1. Set the viewport of the website. Use for desktop "d" and for mobile "m"

`adSSetup = {view: "[View]", // has to fit the design of the page, please use m for mobile and d for desktop`

# 2. Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue

`	partners: true,`

# 3. Define the ad placements for the website
Please make sure that you only include placements you will add an adslot (div#adPlacementID) for the url the user has called
Also please ensure you add the elements mainly in order they will appear in the website, 
because the adserver will fill the first elements of each size with the must valueable campaigns.

## Desktop:

`	adPlacements: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

## Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

 For Desktop:
# Mandatory:
- superbanner
- sky
- billboard
- mrec
- inpage
# Optional
- billboard_btf
- mrec_btf
- sky_btf

 For Mobile:
# Mandatory:
- banner
- mrec
- inpage
- mrec_btf

# Optional
- banner_sticky

__You can repeat the _btf placements as much as you want. Please use the following schema:__

Example for 3 Medium Rectangle btf

- mrec_btf
- mrec_btf_2
- mrec_btf_3

# 4. Define the sizes for every ad placement:

### IMPORTANT
Please add the size `9x9` to every placement cleared for programmatic.

## Desktop:

```
	adSlotSizes: {
		"superbanner": [{
			"minWidth": 1,
			"sizes": [[728,90],[728,600],[1000,600]]
		}],
     
		"sky": [{
			"minWidth": 1,
			"sizes": [[160,600],[120,600],[300,600],[500,1000],[1000,1000]]
		}],
     
		"billboard": [{
			"minWidth": 1,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
     
		"mrec_btf_2": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
     
		"mrec_btf_3": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],
     
	},
```

## Mobile:

```
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],
     
		"mrec_btf_2": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],
     
		"mrec_btf_3": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],
     
	}
}
```


 Ad Sizes for every placement:
# For Desktop:
Placement | Size 1 | Size 2 | Size 3 | Size 4  | Size 5 
--- | --- | --- | --- | --- | ---
*superbanner* | `[728,90]` | `[728,600]` | `[1000,600]` |  | 
*sky* | `[160,600]` | `[120,600]` | `[300,600]` | `[500,1000]` | `[1000,1000]`
*billboard* | `[970,250]` | `[800,250]` |  |  | 
*mrec* | `[300,250]` | `[300,600]` |  |  | 
*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` |  | 

# For Mobile:
Placement | Size 1 | Size 2 | Size 3 | Size 4  | Size 5  |  Size 6
--- | --- | --- | --- | --- | --- | ---
*banner* | `[320,50]` | `[320,75]` | `[320,80]` |  |  |  
*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`
*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` |  |  | 

# 5. placeholder settings

```
	placeholder: {
		disablePlaceholders: false,			// optional, set to true to disable placeholder logic from adlib
		default: {					// define your standards either defaults will be used
			"border-color": "#EEEDE8",
			"background-color": "#F9F9F7",
			"admarkPosition": "bottom right",	// options: "hidden", "top/bottom", "left/center/right" 
			"color": "#BCBCBC",
			"font-size": "12px",
			"font-family": "Tahoma"
		},
		mrec: {						// define default overides for specific adslot 
			"bgColor": "#FCBFFF"
		}
	}
```
# 6. Page configuration

```
	colorBg: true, // enable/disable coloring of the page-background
	bgClick: true, // enable/disable click on page-background
	hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding vor video
	isArticle: true, // it shows us if the page is an article
	pageName: "demo_story", // channel/article name from CMS, may not contain slashes (/)
	target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
	iabTax: "IAB2,IAB2-1,1,32"
}
```



**_If you will be administrated by MediaImpact we recommend the following schema for pageName:_**
- Home Site --> "home_index"
- Channel, e.g. sport --> "sport_index"
- Sub-Channel e.g. soccer --> "sport.soccer_index"
- Article e.g. soccer article --> "sport.soccer_story"
# target: Every editorial keyword or custom target
- you can use stand alone keywords with semicolon `;` separately
- key/values are also supported. `key=value1,value2;`
- please ensure to end the line with a semicolon
- with iabTax you can classify your content - have a look into [this IAB standard](https://iabtechlab.com/standards/content-taxonomy/) for more info

`</script>`

# 7. AdLib

`<script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/mywebsite.js"></script>`

This `js` contains the whole Ad Library. Every website will get its own `js` from Axel Springer.

`</head>`


Ad Placements in the `<body>` of the website:

```
<div id="${adPlacement}"></div>
```

This `div` has to be wrapped in an own container, has to be free of Styles/CSS and the `div id` must be the name of the placement. [See from line 24 of this document](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website). 

### Example

__Superbanner__

```
<div id="superbannerWrapper" class="container">
    <div id="superbanner"></div>
</div>
```


## Ad Placements Overview

## Display

 ### superbanner

`<div id="superbanner"></div>`

![superbanner](assets/superbanner.png "superbanner")

This placement should be positioned at the top of the web page. Wallpapers and fireplaces are also delivered via this placement. [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*superbanner* | `[728,90]` | `[728,600]` | `[1000,600]`

### sky

`<div id="sky"></div>`

![sky](assets/sky.png "sky")

This placement is to be positioned on the left side of the website content. Sitebars, dynamic sitebars, and double-dinamic sitebars are also delivered via this placement. [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*sky* | `[160,600]` | `[120,600]` | `[300,600]` | `[500,1000]` | `[1000,1000]`

### billboard

`<div id="billboard"></div>`

![billboard](assets/billboard.png "billboard")

This placement is to be placed directly under the navigation or under the first teaser of the website. [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*billboard* | `[970,250]` | `[800,250]` 

### mrec

`<div id="mrec"></div>`

![mrec](assets/mrec.png "mrec")

We recommend to place the first Mrec above the fold (ATF). [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[300,600]`  

### inpage

`<div id="inpage"></div>`

![inpage](assets/inpage.png "inpage")

Interstitials, Understitials, and InText-Outstream Advertising Materials are delivered through the inpage Placement. This placement is to be placed in the position requested by the publisher for InText- Outstream ads. [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` 

## Mobile

### banner

`<div id="banner"></div>`

![banner](assets/mobil_banner.png "banner")

This placement should be positioned at the top of the web page.  [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*banner* | `[320,50]` | `[320,75]` | `[320,80]`

### mrec

`<div id="mrec"></div>`

![mrec](assets/mobil_mrec.png "mrec")

We recommend to place the first Mrec above the fold (ATF). [These sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`

### inpage

`<div id="inpage"></div>`

![inpage](assets/mobil_inpage.png "inpage")

Interstitials, Understitials, and InText-Outstream Advertising Materials are delivered through the inpage Placement. This placement is to be placed in the position requested by the publisher for InText- Outstream ads. [This sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` 

### mrec_btf

`<div id="mrec"></div>`

![mrec_btf](assets/mobil_mrec-btf.png "mrec_btf")

This placement can be placed multiple times on a page. We stron recommend to place one mrec_btf after 3 blocks of text. 
**_Please use the following schema_**
- mrec_btf
- mrec_btf_2
- mrec_btf_3

[This sizes must be used](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`

## Creative Sizes Reference

Each Size belongs to a certain creative. For standard creatives we use the IAB standards.


Size | Creative | IAB | Preview
--- | --- | --- | ---
*728,90* | Superbanner/Leaderboard | [YES](https://www.iab.com/guidelines/universal-ad-package/) | ![superbanner](https://www.mediaimpact.de/data/uploads/2018/08/superbanner.png) 
*728,600* | Wallpaper | NO | ![wallpaper](https://www.mediaimpact.de/data/uploads/2018/08/Wallpaper-Desktop-621x350.png)
*1000,600* | Fireplace | NO | ![fireplace](https://www.mediaimpact.de/data/uploads/2018/09/Fireplace-Desktop-621x350.png)
*120,600 / 160,600* | Skyscraper/Wide Skyscraper | [YES](https://www.iab.com/guidelines/universal-ad-package/) | ![sky](https://www.mediaimpact.de/data/uploads/2018/08/skyscraper.png)
*500,1000* | Sitebar / Dynamic Sitebar | NO | ![sitebar](https://www.mediaimpact.de/data/uploads/2018/08/sitebar-1.png) 
*1000,1000* | Double Dynamic Sitebar | NO | ![ddsitebar](https://www.mediaimpact.de/data/uploads/2018/08/double-dynamic-sitebar-300x169.png)
*970,250 / 800,250* | Billboard | [YES](https://www.iab.com/guidelines/display-rising-stars-ad-units/) | ![billboard](https://www.mediaimpact.de/data/uploads/2018/08/billboard-300x169.png)
*320,50* | Mobile Banner 6:1 | [YES](https://www.iab.com/wp-content/uploads/2015/11/IAB_Display_Mobile_Creative_Guidelines_HTML5_2015.pdf) | ![banner](https://www.mediaimpact.de/data/uploads/2018/08/mobile-app-content-ad-thumb-130x100.png)
*320,75 / 320,160* | Mobile Banner 4:1, 2:1 | NO | ![banner](https://www.mediaimpact.de/data/uploads/2018/08/mobile-content-ad-300x169.png)
*300,300* | Premium Content Ad / 1:1 | NO | ![banner](assets/1zu1.png)
*1,1* | Interstitial / Layer | NO | ![layer](https://www.mediaimpact.de/data/uploads/2019/03/mobile_halfpage_ad-621x350.png)
*640,360* | InText Outstream | NO | ![intext](https://www.mediaimpact.de/data/uploads/2022/01/bigstage_teaser-130x100.png)
*1000,300* | Understitial | NO | ![understitial](https://www.mediaimpact.de/data/uploads/2018/08/mobile-understitial-300x169.png)

## QA and Testing

### Please don't try to test ads on Localhost. Ads will be not delivered on localhost.

### Anti - Blacklisting Chrome Plugin
Xandr blocks clients or ip-address that make too many ad requests on a determined placement or in a too short time interval. For it is strongly recommended that before you start testing, to change the browser headers.

#### We recomend to use the browser plugin modheaders:
https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj?hl=de

After installing the plugin please insert the following Request Header: 'X-Is-Test:1'


### Test Ads

#### Test Ads for standard placements
In order to get test advertising please open the [following URL at first](https://adtechnology.axelspringer.com/testads.html), it will turn on the test ads for 30 days. **Please be sure that your browsers accepts 3th party cookies**. 

https://adtechnology.axelspringer.com/testads.html


#### Test Ads for special placements
If your website hast special placement f.e. Teaser, multilinks, etc., please contact adtechnology@axelspringer.de to get the test-instructions.
 
## Special Features
### Lazy Loading
The "btf" placements in the Browser are loaded with lazy loading. Those ads will be rendered only if the placement 100px under the viewport
![Lazyloading](assets/lazyloading.png "Lazy Loading")
