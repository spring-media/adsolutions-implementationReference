# deals.bild.de - desktop AdSSetup

In this documentation you find the placement details for your Website.  



## Ad Integration

 Elements in the `<head>` of the website:

`<script type="text/javascript">`


## 1. Set the viewport of the website

Set view: "m" for mobile or "d" for desktop viewport.

`adSSetup = {view: "d",`


## 2. Switch for the 3th party scripts. We strictly recommend to set it as "false" only on pages for directsales campaign only to max out the revenue

`	partners: true,`


## 3. Define Placements for your site

Please make sure that you only include placements you will add an adslot (div#adPlacementID) for the url the user has called.
Also please ensure you add the elements mainly in order they will appear in the website, 
because the adserver will fill the first elements of each size with the must valueable campaigns.


`	adPlacements: ["a-teaser","mrec","dealsad","inpage"],`


__You can repeat the _btf placements as much as you want. Please use the following schema:__

Example for 3 Medium Rectangle btf

- mrec_btf
- mrec_btf_2
- mrec_btf_3

More info on [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) and [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)


## 4. Define the sizes for every ad placement:


### Sizes for home_index

```
	adSlotSizes: {
		"a-teaser": [{
			"minWidth": 1,
			"sizes": [[2,2]]
		}],
    
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
    
		"dealsad": [{
			"minWidth": 1,
			"sizes": [[728,90]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1]]
		}]
	},
```

### Sizes for channel_index

```
	adSlotSizes: {
		"a-teaser": [{
			"minWidth": 1,
			"sizes": [[2,2]]
		}],
    
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
    
		"dealsad": [{
			"minWidth": 1,
			"sizes": [[728,90]]
		}],
	},
```


### Sizes for shop_index & shop_story

```
	adSlotSizes: {
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
    
		"dealsad": [{
			"minWidth": 1,
			"sizes": [[728,90]]
		}],
	},
```



## 5. Page Configuration


```
        colorBg: true,             // enable/disable coloring of the page-background
	bgClick: true,             // enable/disable click on page-background
	hasVideoPlayer: true,      // enable/disable partnerscripts like headerbiding for video
	isArticle: true,           // it shows us if the page is an article
	pageName: "demo_story",    // channel/article name from CMS, may not contain slashes (/)
	target: "value1;value2;value3;key1=value1,value2;key2=value1,value2;",
	iabTax: "IAB2,IAB2-1,1,32"
}

</script>
```

### Notes

- With the 'iabTax' values, you can classify your content 
  - More infos on [IAB Taxonomy](https://www.iab.com/guidelines/taxonomy/) 

- the 'target' attribute will contain every editorial keyword
  - you can use standalone keywords with semicolon `;` separately
  - key/values are also supported. `key=value1,value2;`
  - please ensure to end the line with a semicolon



# 6. AdLib

`<script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/bilddeals.js"></script>`

This `js` contains the whole Ad Library.




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
