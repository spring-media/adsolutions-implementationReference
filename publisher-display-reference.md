# Integration - Online Desktop & Mobile Advertisement

## Introduction

This document describes the necessary steps for integrating online advertisements on desktop and mobile websites for Axel Springer. 
The delivery of ads utilizes a "One Call" function, which have to be included in the `<head>` part of the websites. This will receive the booked campaings and will let them in the background for lately rendering. The Ad Placements are `<div>`'s which have to be placed in the wished position for the ad. All Advertisements can be managed via Appnexus.

### Overview

In the following you will find an overview of the necessary components which must be implemented to deliver and display the advertising media.

#### Elements in the `<head>` of the website:

`<script type="text/javascript">`

##### 1. Set the viewport of the website. Use for desktop "d" and for mobile "m"

`adSSetup = {
		view: "[View]", // has to fit the design of the page, please use m for mobile and d for desktop`

##### 2. Switch for the 3th party scripts. We estrictly recommend to set it as "true"

`partners: false,`

##### 3. Define the ad placements for the website

`adSlots: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

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

You can repeat the _btf placements as much as you want. Please use the following schema:

Example for 3 Medium Rectangle btf

- mrec_btf
- mrec_btf_2
- mrec_btf_3

#### 4. Define the sizes for every ad placement:


`adSlotSizes: {`

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
      
		},`


