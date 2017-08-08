# sportbild.de

In this documentation you find the placement details for your Website.  Please find an test-site on the following link:    [Appnexus test site](https://adtechnology.mediaimpact.de/test-appnexus/)

## AdLib

Please use the following JS for the adLib: ```https://acdn.adnxs.com/as/1h/pages/sportbild.js```


## Placements

 Desktop

# Standard Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Superbanner|3648|superbanner|
|Sky|3650|sky|
|Sky 2|3650|sky_btf|
|Billboard|5419|billboard|
|Medium Rectangle|4459|mrec|
|Medium Rectangle 2|4460|mrec_btf|
|Richmedia / Outstream|3651 / 18913|inpage|

# Special Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|contentbar01|3937|billboard_btf|
|contentbar02|8443|billboard_btf_2|
|regteaser01|3938|teaser|

# Special Sport Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|wettpartner_ergebnisModul|22150|wettpartner_ergebnisModul|
|wettpartner_livekalender_ankuendigung|33910|wettpartner_livekalender_ankuendigung|
|wettpartner_scoreboard|22149|wettpartner_scoreboard|
|wettpartner_textlink|22148|wettpartner_textlink|


 Mobile

# Standard Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Reminder|12815 (3648)|banner|
|Content Ad|5720 (5419)|mrec|
|Medium Rectangle|4459|mrec_btf|
|Footer Ad|5721 (3650)|mrec_btf_2|
|Richmedia / Outstream|6419 (3651) / 29606 (18913)|inpage|

# Special Sport Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|wettpartner_ergebnisModul|22150|wettpartner_ergebnisModul|
|wettpartner_livekalender_ankuendigung_mobil|33911|wettpartner_livekalender_ankuendigung|
|wettpartner_scoreboard_mobil|33908|wettpartner_scoreboard|
|wettpartner_textlink_mobil|33913|wettpartner_textlink|


## Standard Integration Sample

 [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

# Desktop:

`	adPlacements: ["superbanner","sky","sky_btf","billboard","mrec","mrec_btf","inpage"],`

# Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","mrec_btf_2","inpage"],`

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
			"sizes": [[320,50],[320,75],[320,160]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
		}],

		"mrec_btf_2": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,50],[320,75],[320,160],[300,300]]
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
  
