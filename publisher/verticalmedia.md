# Verticalmedia

In this documentation you find the placement details for your Website.  

## Pagenames

-homepage
-automotive
-food
-gsconnect
-karriere
-artikel
-events
-gallery
-datenbank
-jobboard
-lexikon
-suche
-themenspezial


## AdLib

Please use the following JSs for the adLib: 

www.gruenderszene.de ```https://acdn.adnxs.com/as/1h/pages/gruenderszene.js```
www.ngin-food.com ```https://acdn.adnxs.com/as/1h/pages/ngin-food.js```
www.ngin-mobility.com ```https://acdn.adnxs.com/as/1h/pages/ngin-mobility.js```


## Placements

 Desktop

| Placement Name|Sizes|PLacement Name|
| ------------- |:-------------:| -----:|
|Superbanner|[728,90],[728,600],[1000,600]|superbanner|
|Sky|[160,600],[120,600],[300,600],[500,1000],[1000,1000]|sky|
|Billboard|[960,250],[800,250]|billboard|
|Medium Rectangle|[300,250],[300,600],[640,360],[1000,300]|mrec|
|Medium Rectangle 2|[300,250]|mrec_btf|
|Medium Rectangle 3|[300,250]|mrec_btf_2|
|Medium Rectangle 4|[300,250]|mrec_btf_3|
|Richmedia|[1,1]|inpage|

 Mobile


| Placement Name|Sizes|PLacement Name|
| ------------- |:-------------:| -----:|
|Medium Rectangle|[300,250],[300,600],[640,360],[1000,300]|mrec|
|Medium Rectangle 2|[300,250]|mrec_btf|
|Medium Rectangle 3|[300,250]|mrec_btf_2|
|Medium Rectangle 4|[300,250]|mrec_btf_3|
|Richmedia|[1,1]|inpage|

 [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["superbanner","sky","billboard","mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`

# Mobile:

`	adPlacements: ["mrec","mrec_btf","mrec_btf_2","mrec_btf_3","inpage"],`
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
			"sizes": [[300,250],[300,600],[640,360],[1000,300]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec_btf_2": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec_btf_3": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1]]
		}],
     
	},
```

# Mobile:

```
	adSlotSizes: {
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600],[640,360],[1000,300]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec_btf_2": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

		"mrec_btf_3": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1]]
		}],
     
	},
```

## Important notes

- For Intext Outstream and for Richmedia we just need one placement with Appnexus.
- __IMPORTANT__ Please palace the "inpage" placement in the required position for InText. Take care that we need the whole website wide for it.

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
  
