# Integration - Online Desktop & Mobile Advertisement


**Table of Contents**  

- [Introduction](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#introduction)
- [Overview](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#overview)
- [Ad Integration](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#ad-integration)
	- [`<head>` elements](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#elements-in-the-head-of-the-website)
		- [1. Viewport](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#1-set-the-viewport-of-the-website-use-for-desktop-d-and-for-mobile-m)
		- [2. 3th party scripts.](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#2-switch-for-the-3th-party-scripts-we-strictly-recommend-to-set-it-as-false-only-on-pages-for-directsales-campaign-only-the-max-out-the-revenue)
		- [3. Placements](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)
			- [Desktop](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop)
				- [Mandatory](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mandatory)
				- [Optional](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#optional)
			- [Mobile](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-mobile)
				- [Mandatory](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mandatory-1)
				- [Optional](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#optional-1)
		- [4. Placement Sizes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)
			- [Placement's Sizes Reference](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#ad-sizes-for-every-placement)
				- [For Desktop](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1)
				- [For Mobile](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-mobile-1)
		- [5. Page configuration](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#5-page-configuration)
			- [colorBG](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#colorbg-enabledisable-coloring-of-the-page-background)
			- [bgClick](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#bgclick-enabledisable-click-on-page-background)
			- [stickySky](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#stickysky-enabledisable-stickiness-for-skyscraper)
			- [pageName](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#pagename-it-is-the-name-of-the-channel-or-article-in-cms)
			- [target](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#target-every-editorial-keyword-or-custom-target)
		- [6. AdLib](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#6-adlib)
- [Ad Placements in the `<body>`](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#ad-placements-in-the-body-of-the-website)
		- [Example](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#example)
	- [Ad Placements Overview](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#ad-placements-overview)
		- [Display](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#display)
			- [superbanner](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#superbanner)
			- [sky](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#sky)
			- [billboard](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#billboard)
			- [mrec](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mrec)
			- [inpage](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#inpage)
		- [Mobile](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mobile)
			- [banner](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#banner)
			- [mrec](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mrec-1)
			- [inpage](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#inpage-1)
			- [mrec_btf](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#mrec_btf)

## Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Appnexus.

## Overview

In the following you will find an overview of the necessary components which must be implemented to deliver and display the advertising media.

## Ad Integration

### Elements in the `<head>` of the website:

`<script type="text/javascript">`

#### 1. Set the viewport of the website. Use for desktop "d" and for mobile "m"

`adSSetup = {view: "[View]", // has to fit the design of the page, please use m for mobile and d for desktop`

#### 2. Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only the max out the revenue

`	partners: true,`

#### 3. Define the ad placements for the website

`	adPlacements: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

### For Desktop:
#### Mandatory:
- superbanner
- sky
- billboard
- mrec
- inpage
#### Optional
- billboard_btf
- mrec_btf
- sky_btf

### For Mobile:
#### Mandatory:
- banner
- mrec
- inpage
- mrec_btf

#### Optional
- banner_sticky

__You can repeat the _btf placements as much as you want. Please use the following schema:__

Example for 3 Medium Rectangle btf

- mrec_btf
- mrec_btf_2
- mrec_btf_3

#### 4. Define the sizes for every ad placement:

```
	adSlotSizes: {
		"superbanner": {
			"minWidth": 1,
			"sizes": [[728,90],[728,600],[1000,600]]
		},
     
		"sky": {
			"minWidth": 1,
			"sizes": [[160,600],[120,600],[300,600],[500,1000],[1000,1000]]
		},
     
		"billboard": {
			"minWidth": 1,
			"sizes": [[970,250],[800,250]]
		},
     
		"mrec": {
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		},
     
		"mrec_btf": {
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		},
     
		"mrec_btf_2": {
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		},
     
		"mrec_btf_3": {
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		},
     
		"inpage": {
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		},
     
	},
```

### Ad Sizes for every placement:
#### For Desktop:
Placement | Size 1 | Size 2 | Size 3 | Size 4  | Size 5 
--- | --- | --- | --- | --- | ---
*superbanner* | `[728,90]` | `[728,600]` | `[1000,600]` |  | 
*sky* | `[160,600]` | `[120,600]` | `[300,600]` | `[500,1000]` | `[1000,1000]`
*billboard* | `[970,250]` | `[800,250]` |  |  | 
*mrec* | `[300,250]` | `[300,600]` |  |  | 
*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` |  | 

#### For Mobile:
Placement | Size 1 | Size 2 | Size 3 | Size 4  | Size 5  |  Size 6
--- | --- | --- | --- | --- | --- | ---
*banner* | `[320,50]` | `[320,75]` | `[320,80]` |  |  |  
*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`
*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` |  |  | 

#### 5. Page configuration

```
	colorBg: true, // enable/disable coloring of the page-background
	bgClick: true, // enable/disable click on page-background
	stickySky: true, // enable/disable stickiness for skyscraper
	pageName: "demo_story", // channel/article name from CMS
       	target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;"
}
```

#### colorBG: enable/disable coloring of the page-background
#### bgClick: enable/disable click on page-background
#### stickySky: enable/disable stickiness for skyscraper
#### pageName: it is the name of the channel or article in CMS
**_We recommend the following schema:_**
- Home Site --> "home_index"
- Channel, e.g. sport --> "sport_index"
- Sub-Channel e.g. soccer --> "sport.soccer_index"
- Article e.g. soccer article --> "sport.soccer_story"
#### target: Every editorial keyword or custom target
- you can use stand alone keywords with semicolon `;` separately
- key/values are also supported. `;key=value1,value2;`

`</script>`

#### 6. AdLib

`<script type="text/javascript" src="https://www.example-cdn.com/assets/js/mywebsite.js"></script>`

This `js` contains the whole Ad Library. Every website will get its own `js` from Axel Springer.

`</head>`


### Ad Placements in the `<body>` of the website:

```
<div id="${adPlacement}"></div>
```

The `div id` must be the name of the placement. [See from line 24 of this document](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website). 

#### Example

__Superbanner__

`<div id="superbanner"></div>`

`</body>`

## Ad Placements Overview

## Display

### superbanner

`<div id="superbanner"></div>`

![superbanner](https://bracho.xyz/adtech/img/superbanner.png "superbanner")

This placement should be positioned at the top of the web page. Wallpapers and fireplaces are also delivered via this placement. [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*superbanner* | `[728,90]` | `[728,600]` | `[1000,600]`

### sky

`<div id="sky"></div>`

![sky](https://bracho.xyz/adtech/img/sky.png "sky")

This placement is to be positioned on the left side of the website content. Sitebars, dynamic sitebars, and double-dinamic sitebars are also delivered via this placement. [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*sky* | `[160,600]` | `[120,600]` | `[300,600]` | `[500,1000]` | `[1000,1000]`

### billboard

`<div id="billboard"></div>`

![billboard](https://bracho.xyz/adtech/img/billboard.png "billboard")

This placement is to be placed directly under the navigation or under the first teaser of the website. [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*billboard* | `[970,250]` | `[800,250]` 

### mrec

`<div id="mrec"></div>`

![mrec](https://bracho.xyz/adtech/img/mrec.png "mrec")

We recommend to place the first Mrec above the fold (ATF). [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[300,600]`  

### inpage

`<div id="inpage"></div>`

![inpage](https://bracho.xyz/adtech/img/inpage.png "inpage")

Interstitials, Understitials, and InText-Outstream Advertising Materials are delivered through the inpage Placement. This placement is to be placed in the position requested by the publisher for InText- Outstream ads. [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` 

## Mobile

### banner

`<div id="banner"></div>`

![banner](https://bracho.xyz/adtech/img/mobil_banner.png "banner")

This placement should be positioned at the top of the web page.  [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*banner* | `[320,50]` | `[320,75]` | `[320,80]`

### mrec

`<div id="mrec"></div>`

![mrec](https://bracho.xyz/adtech/img/mobil_mrec.png "mrec")

We recommend to place the first Mrec above the fold (ATF). [These sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`

### inpage

`<div id="inpage"></div>`

![inpage](https://bracho.xyz/adtech/img/mobil_inpage.png "inpage")

Interstitials, Understitials, and InText-Outstream Advertising Materials are delivered through the inpage Placement. This placement is to be placed in the position requested by the publisher for InText- Outstream ads. [This sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` 

### mrec_btf

`<div id="mrec"></div>`

![mrec_btf](https://bracho.xyz/adtech/img/mobil_mrec-btf.png "mrec_btf")

This placement can be placed multiple times on a page. We stron recommend to place one mrec_btf after 3 blocks of text. 
**_Please use the following schema_**
- mrec_btf
- mrec_btf_2
- mrec_btf_3

[This sizes must be used](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#for-desktop-1).

*mrec* | `[300,250]` | `[320,50]` | `[320,75]` | `[320,80]` | `[320,160]` | `[300,300]`

## Creative Sizes Reference

Each Size belongs to a certain creative. For standard creatives we use the IAB standards.


## Display

Size | Creative | IAB | Preview
--- | --- | --- | ---
*728,90* | Superbanner/Leaderboard | [YES](https://www.iab.com/guidelines/universal-ad-package/) | ![superbanner](https://www.mediaimpact.de/img/259938729_8679ac04a5.png) 
 
