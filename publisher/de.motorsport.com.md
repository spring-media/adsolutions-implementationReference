# de.motorsport.com

In this documentation you find the placement details for your Website.  Please find an test-site on the following link:    [Appnexus test site](https://adtechnology.mediaimpact.de/test-appnexus/)

## AdLib

Please use the following JS for the adLib: ```https://acdn.adnxs.com/as/1h/pages/motorsport.js```


## Placements

 Desktop

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Superbanner|3648|superbanner|
|Sky|3650|sky|
|Sky|4454|sky_btf|
|Billboard|5419|billboard|
|Billboard_btf|23743|billboard_btf|
|Medium Rectangle|4459|mrec|
|Medium Rectangle|4460|mrec_btf|
|Richmedia / Outstream|3651 / 18913|inpage|
|regteaser01|3938|teaser|
|regteaser02|3939|teaser_2|

 Mobile


| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Reminder|12815 (3648)|banner|
|Content Ad|5720 (5419)|mrec|
|Rectangle_Mobil/Rectangle01|19619/4459|mrec_btf|
|Richmedia / Outstream|6419 (3651) / 29606 (18913)|inpage|
|regteaser01|21530|teaser|
|regteaser02|21532|teaser_2|


 [Placement Codes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Display

### Desktop - Index:

`	adPlacements: ["superbanner","sky","sky_btf","billboard","billboard_btf","mrec","mrec_btf","inpage","teaser","teaser_2"],`

### Desktop - Story:

`	adPlacements: ["superbanner","sky","sky_btf","billboard_btf","mrec","mrec_btf","inpage","teaser","teaser_2"],`

### Desktop - Bildergalerien:

`	adPlacements: ["superbanner","mrec"],`

### Desktop - Statistiken:

`	adPlacements: ["superbanner","sky","sky_btf","billboard_btf","mrec","mrec_btf","inpage","teaser","teaser_2"],`

### Desktop - Liveticker:

`	adPlacements: ["superbanner","sky","sky_btf","billboard_btf","mrec","mrec_btf","inpage","teaser","teaser_2"],`

### Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","inpage","teaser"],`

### AMP:

`	adPlacements: ["banner_sticky","mrec"],`




# Video

### Desktop - Video:

`	adPlacements: ["preroll","midroll"],`

### Mobile - Video:

`	adPlacements: ["preroll","midroll"],`

### AMP - Video:

`	adPlacements: ["preroll","midroll"],`




[Placement Sizes](https://github.com/spring-media/adsolutions-implementationReference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)


# Desktop:

```
	adSlotSizes: {
		"superbanner": [{
			"minWidth": 1023,
			"sizes": [[728,90],[728,600],[1000,600],[800,250],[970,250]]
		}],
     
		"sky": [{
			"minWidth": 1,
			"sizes": [[160,600],[120,600],[300,600],[500,1000],[1000,1000]]
		}],
    
    		"sky_btf": [{
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
    
    		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],
    
    		"teaser": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],

		"teaser_2": [{
			"minWidth": 1,
			"sizes": [[300,150]]
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
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],
				
		"teaser": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],

		"teaser_2": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],		
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
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
  Spring

  Tel: +49 30 2591 78009
  Mobile: +49 151 22334646 
  timo.nolte@axelspringer.de


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Spring
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
  
