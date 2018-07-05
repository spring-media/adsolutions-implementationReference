# Verticalmedia

In this documentation you find the placement details for your Websites.  


## Pagenames


### Gründerszene
- homepage
- automotive
- food
- gsconnect
- karriere
- artikel
- events
- gallery
- datenbank
- jobboard
- lexikon
- suche
- themenspezial

### ngins
- homepage
- artikel
- jobs


## AdLib

Please use the following JSs for the adLib: 

- www.gruenderszene.de ```https://acdn.adnxs.com/as/1h/pages/gruenderszene.js```
- www.ngin-food.com ```https://acdn.adnxs.com/as/1h/pages/ngin-food.js```
- www.ngin-mobility.com ```https://acdn.adnxs.com/as/1h/pages/ngin-mobility.js```


## Placements

 Desktop

| Placement Name|Sizes|Placement Name|
| ------------- |:-------------:| -----:|
|Superbanner|[728,90],[728,600],[1000,600]|superbanner|
|Sky|[160,600],[120,600],[300,600],[500,1000],[1000,1000]|sky|
|Billboard|[960,250],[800,250]|billboard|
|Medium Rectangle|[300,250],[300,600],[1000,300]|mrec|
|Medium Rectangle 2|[300,250]|mrec2|
|Medium Rectangle 3|[300,250]|mrec3|
|Medium Rectangle 4|[300,250]|mrec4|
|Richmedia|[1,1],[640,360]|inpage|

 Mobile


| Placement Name|Sizes|PLacement Name|
| ------------- |:-------------:| -----:|
|Banner|[300,150]|banner|
|Medium Rectangle|[300,250],[300,600],[1000,300]|mrec|
|Medium Rectangle 2|[300,250]|mrec2|
|Medium Rectangle 3|[300,250]|mrec3|
|Medium Rectangle 4|[300,250]|mrec4|
|Richmedia|[1,1],[640,360]|inpage|

 [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

# Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`
 [Placement Sizes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)

# Desktop:

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
			"sizes": [[960,250],[800,250]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600],[1000,300]]
		}],
     
		"mrec2": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec3": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec4": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360]]
		}],
     
	},
```

# Mobile:

```
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600],[1000,300]]
		}],
     
		"mrec2": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec3": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec4": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360]]
		}],
     
	},
```

## AMP

### ngin Mobility

```html
<amp-ad width=300 height=250
        type="appnexus"
        data-member="7823"
        data-code="ngin-mobility-amp-ros-mrec"
></amp-ad>
```

### ngin Food

```html
<amp-ad width=300 height=250
        type="appnexus"
        data-member="7823"
        data-code="ngin-food-amp-ros-mrec"
></amp-ad>
```


## Important notes



## Help

If you have some question don't hesitate to contact us:


__Timo Nolte__
 
  Head of AdSolutions
  Corporate Digital Platforms

  Tel: +49 30 2591 78009
  Mobile: +49 151 22334646 
  timo.nolte@axelspringer.de


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  
