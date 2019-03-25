# meinprospekt.de

In this documentation you find the placement details for your Website.  

## AdLib

Please use the following JS for the adLib: ```https://www.asadcdn.com/adlib/pages/meinprospekt.js```


## Placements

 Desktop

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Sky|3650|sky|
|Superbanner|3648|superbanner|
|Billboard|5419|billboard|
|Billboard_btf|5419|billboard_btf|
|Medium Rectangle|4459|mrec|
|Medium Rectangle|4459|mrec_btf|
|Medium Rectangle|4459|mrec_btf_2|
|Medium Rectangle|4459|mrec_btf_3|

 Mobile


| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Reminder|12815 (3648)|banner|
|Medium Rectangle|4459|mrec_btf|
|Medium Rectangle|4459|mrec_btf_2|
|Medium Rectangle|4459|mrec_btf_3|
|Medium Rectangle|4459|mrec_btf_4|


 [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["sky","billboard","billboard_btf","mrec","mrec_btf","mrec_btf_2","mrec_btf_3"],`

# Mobile:

`	adPlacements: ["banner","mrec_btf","mrec_btf_2","mrec_btf_3","mrec_btf_4"],`

 [Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)

# Desktop:

```
	adSlotSizes: {
		"superbanner": [{
			"minWidth": 1023,
			"sizes": [[728,90],[728,600],[1000,600]]
		}],
     
		"sky": [{
			"minWidth": 1,
			"sizes": [[160,600],[120,600],[300,600],[500,1000],[1000,1000]]
		}],
     
		"billboard": [{
			"minWidth": 799,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		},{
			"minWidth": 767,
			"sizes": [[728,90]]			
		}],
    
    		"billboard_btf": [{
			"minWidth": 799,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		},{
			"minWidth": 767,
			"sizes": [[728,90]]			
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
		
	},
```

# Mobile:

```
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80]]
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
		
    		"mrec_btf_4": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],    
		
    
	},
```

## Important notes

- For Intext Outstream and for Richmedia we just need one placement with Appnexus.
- __IMPORTANT__ Please palace the "inpage" placement in the required position for InText. Take care that we need the whole website wide for it.

## Help

If you have some question don't hesitate to contact us:


__Gertrud Kolb__
 
  Head of AdSolutions
  Corporate Digital Platforms

  Tel: +49 30 2591 72504
  gertrud.kolb@spring-media.de


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  
