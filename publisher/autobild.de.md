# autobild.de

In this documentation you find the placement details for your Website.  Please find an test-site on the following link:    [Appnexus test site](https://adtechnology.mediaimpact.de/test-appnexus/)

## Placements

 Desktop

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Superbanner|3648|superbanner|
|Sky|3650|sky|
|Billboard|5419|billboard|
|Billboard 2|23743|billboard_btf|
|Medium Rectangle|4459|mrec|
|Medium Rectangle 2|4460|mrec_btf|
|Contentbar01|3937|billboard_btf_2|
|menuad|23447|menuad|
|multilink|4465|multilink|
|regteaser01|3938|teaser|
|regteaser02|3939|teaser_2|
|regteaser03|3940|teaser_3|
|regteaser04|19237|teaser_4|
|regteaser05|19238|teaser_5|
|regteaser06|19239|teaser_6|
|Richmedia / Outstream|3651 / 18913|inpage|

 Mobile


| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Reminder|12815|banner|
|Content Ad|5720|mrec|
|Rectangle_Mobil|19619|mrec_btf|
|regteaser01|3938|teaser|
|regteaser02|3939|teaser_2|
|Footer Ad|5721|mrec_btf_2|
|Richmedia / Outstream|6419 / 29606|inpage|

 [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["superbanner","sky","billboard","billboard_btf","mrec","mrec_btf","billboard_btf_2","menuad","multilink","teaser","teaser_2","teaser_3","teaser_4","teaser_5","teaser_6","inpage"],`

# Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","teaser","teaser_2","mrec_btf_2","inpage"],`
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
			"minWidth": 799,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		}],
		
		"billboard_btf": [{
			"minWidth": 799,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],

		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
		
		"billboard_btf_2": [{
			"minWidth": 799,
			"sizes": [[800,250]]
		},{
			"minWidth": 969,
			"sizes": [[970,250],[800,250]]
		}],		

		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],

		"menuad": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],

		"multilink": [{
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

		"teaser_3": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],

		"teaser_4": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],

		"teaser_5": [{
			"minWidth": 1,
			"sizes": [[300,150]]
		}],

		"teaser_6": [{
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
		
		"mrec_btf_3": [{
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

- The following formats should be removed because they are no longer used:
	- bigbox_aubi: 4466
	- double_content_ad: 15953
	- fullbanner01: 4158
	- fullbanner02: 4468
	- header_aubi: 4467
	- sponsoring_button_aubi: 4806
	- superflyout_aubi: 15889
	- verticalbanner: 4464
	- mobile_native_ad_branded_news: 24940


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
  
