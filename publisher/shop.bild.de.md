# shop.bild.de

# shop.bild.de - AdSSetup

In this documentation you find the placement details for your website.

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

`	adPlacements: ["superbanner", "billboard", "sky", "mrec", "mrec_btf"],`

### Notes

If you have infinite scrolling on a site, you can repeat _btf placements as much as you want. Keep in mind that an initial _btf placement needs to be defined like a normal placement in `AdPlacements` and `adSlotSizes`. In addition the initial _btf placement needs to exist in the ad server, too. Each incremented element is (if itself is not defined in adSSetup) a copy of the original _btf placement. Please use the following schema:
Example for 3 Medium Rectangle btf
- mrec_btf
- mrec_btf_2
- mrec_btf_3
For a deeper explanation please take a look into this documentation about our [onDemandAd-Integration](https://github.com/spring-media/adsolutions-implementationReference/blob/master/peculiar/onDemandAd-integration.md).

More info on [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement) and [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

## 4. Define the sizes for every ad placement:

### Sizes for your channel

```
	adSlotSizes: {
		"superbanner": [{
			"minWidth": 1,
			"sizes": [[728,90],[800,250],[970,250]]
		}],
		"billboard": [{
			"minWidth": 1,
			"sizes": [[800,250],[970,250]]
		}],
		"sky": [{
			"minWidth": 1,
			"sizes": [[160,600],[120,600],[300,600]]
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
```

## 5. CLS Placeholder

Please include the following placeholder object in your adSSetup. This will preload adslot containers to prevent a content layout shift which will be a new SEO metric from Google. You can take a look into [our documentation about the cumulative layout shift](https://github.com/spring-media/adsolutions-implementationReference/blob/master/cumulative-layout-shift.md) (CLS) to get a deeper explanation on the topic.

You need to declare the default object to get working placeholders on your site. You can set valid css attributes to customize all your placeholders at once and in case you need to style some placeholders differently, you can do so by adding these slots after the default object. Its css attributes will overwrite the default values.

```
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
	},
```


## 6. Page Configuration

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

# 7. AdLib

`<script type="text/javascript" src="https://www.asadcdn.com/adlib/pages/bildshop.js"></script>`

This `js` contains the whole Ad Library. Please include it in the header of your site and do not load it asynchronously.
Our adlib is heavily optimized and will initially only load a small set of functions that are absolutely necessary from the beginning. The remaining functions are loaded on demand.

## Help

If you have some question don't hesitate to contact us:

__Ad Technology Team__
  adtechnology@axelspringer.de
