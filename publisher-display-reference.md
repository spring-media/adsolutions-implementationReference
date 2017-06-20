# Integration - Online Desktop & Mobile Advertisement

## Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaigns and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Appnexus.

### Overview

In the following you will find an overview of the necessary components which must be implemented to deliver and display the advertising media.

#### Elements in the `<head>` of the website:

`<script type="text/javascript">`

##### 1. Set the viewport of the website. Use for desktop "d" and for mobile "m"

`adSSetup = {view: "[View]", // has to fit the design of the page, please use m for mobile and d for desktop`

##### 2. Switch for the 3th party scripts. We strictly recommend to set it as "true"

`	partners: false,`

##### 3. Define the ad placements for the website

`	adSlots: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

#### For Desktop:
##### Mandatory:
- superbanner
- sky
- billboard
- mrec
- inpage
#### Optional
- billboard_btf
- mrec_btf
- sky_btf

#### For Mobile:
##### Mandatory:
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
			"sizes": [[970,250],[850,250]]
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
			"sizes": [[1x1],[640,360],[1000,300]]
		},
     
	},
```

#### Ad Sizes for every placement:
##### For Desktop:
Placement | Size 1 | Size 2 | Size 3 | Size 4  | Size 5 
--- | --- | --- | --- | --- | ---
*superbanner* | `[728,90]` | `[728,600]` | `[1000,600]` |  | 
*sky* | `[160,600]` | `[120,600]` | `[300,600]` | `[500,1000]` | `[1000,1000]`
*billboard* | `[970,250]` | `[850,250]` |  |  | 
*mrec* | `[300,250]` | `[300,600]` |  |  | 
*inpage* | `[1,1]` | `[640,360]` | `[1000,300]` |  | 

##### For Mobile:
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

##### colorBG: enable/disable coloring of the page-background
##### bgClick: enable/disable click on page-background
##### stickySky: enable/disable stickiness for skyscraper
##### pageName: it is the name of the channel or article in CMS
__We recommend the following schema__
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

`<body>`
