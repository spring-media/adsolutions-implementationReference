# rund-ums-baby.de

In this documentation you find the placement details for your Website.  Please find an test-site on the following link:    [Appnexus test site](https://adtechnology.mediaimpact.de/test-appnexus/)

## Placements

 Desktop

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Sky|3650|sky|
|Medium Rectangle|4459|mrec|

 Mobile


| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Content Ad|5720 (5419)|banner|
|Medium Rectangle|4459|mrec|

 [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["sky","mrec"],`

# Mobile:

`	adPlacements: ["banner","mrec"],`
 [Placement Sizes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)

# Desktop:

```
	adSlotSizes: {
		"sky": [{
			"minWidth": 1,
			"sizes": [[160,600],[120,600]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250]]
		}],

	},
```

# Mobile:

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
     
	},
```

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
  
