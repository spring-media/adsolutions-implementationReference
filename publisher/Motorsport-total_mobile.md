# motorsport-total.com - mobile Ad AdsSetup

In this documentation you find the placement details for your Website.  

## AdLib

Please use the following JS for the adLib: ```https://www.asadcdn.com/adlib/pages/motorsporttotal.js```



## Ad Integration

 Elements in the `<head>` of the website:

`<script type="text/javascript">`


## 1. Set the viewport of the website

`adSSetup = {view: "m",`


## 2. Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only to max out the revenue

`	partners: true,`


## 3. Define Placements for your site

Please make sure that you only include placements you will add an adslot (div#adPlacementID) for the url the user has called
Also please ensure you add the elements mainly in order they will appear in the website, 
because the adserver will fill the first elements of each size with the must valueable campaigns.


`	adPlacements: ["banner","banner2","mrec","mrec_btf","inpage"],`


__You can repeat the _btf placements as much as you want. Please use the following schema:__

Example for 3 Medium Rectangle btf

- mrec_btf
- mrec_btf_2
- mrec_btf_3

More info on [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) and [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)


## 4. Define the sizes for every ad placement:

### IMPORTANT
Please add the size `9x9` to every placement where programmatic should be able to run. 
Please contact the Programmatic Team if you have questions about the Programmatic Size.

```
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80],[320,160],[300,75],[9,9]]
		}],
    
		"banner2": [{
			"minWidth": 1,
			"sizes": [[4,4]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,75],[300,150],[1000,300],[9,9]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300],[300,75],[300,150],[1000,300],[9,9]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[5,5]]
		}],
     
	},
```


## 5. Page Configuration


```
  colorBg: true, // enable/disable coloring of the page-background
	bgClick: true, // enable/disable click on page-background
	hasVideoPlayer: true, // enable/disable partnerscripts like headerbiding for video
	isArticle: true, // it shows us if the page is an article
	pageName: "demo_story", // channel/article name from CMS, may not contain slashes (/)
	target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
	iabTax: "IAB2,IAB2-1,1,32"
}

```

### Notes

- With the 'iabTax' values, you can classify your content 
  - More infos on [IAB Taxonomy](https://www.iab.com/guidelines/taxonomy/) 

- the 'target' attribute will contain every editorial keyword
  - you can use standalone keywords with semicolon `;` separately
  - key/values are also supported. `key=value1,value2;`
  - please ensure to end the line with a semicolon



## Help

If you have some question don't hesitate to contact us:


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Spring
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
