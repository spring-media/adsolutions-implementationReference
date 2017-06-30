# bild.de

In this documentation you find the placement details for your Website.

## Placements

### Desktop

#### Standard Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Superbanner|3648|superbanner|
|Superbanner 2|3648|superbanner_btf|
|Sky|3650|sky|
|Sky 2|3650|sky_btf|
|Billboard|5419|billboard|
|Medium Rectangle|4459|mrec|
|Medium Rectangle 2|4460|mrec_btf|
|Richmedia / Outstream|3651 / 18913|inpage|

#### Special Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Bild_Home A-Teaser|16669|home a-teaser|
|content_stoerer_1 (NewsBlock)|16267|newsblock|
|content_stoerer_2 (PolitikBlock)|16269|politikblock|
|content_stoerer_3 (Unterhaltung Block)|16270|untelhaltungsblock|
|content_stoerer_4 (Sport)|16271|sportblock|
|content_stoerer_5 (Geld Block)|16272|geldblock|
|content_stoerer_6 (Regional Block)|16273|regionalblock|
|content_stoerer_7 (Video)|16274|videoblock|
|content_stoerer_XXL_1|17376|xxlblock|
|content_stoerer_XXL_2|17377|xxlblock_2|
|contentbar01|3937|billboard_btf|
|contentbar02|8443|billboard_btf_2|
|contentbar03|8444|billboard_btf_3|
|regteaser01|3938|teaser|
|regteaser01|3939|teaser_2|
|regteaser01|3940|teaser_3|

#### Special Sport Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|bild_buli_powerbutton|19708|home a-teaser|
|bild_buli_powerplace|19702|buli_powerplace|
|bild_buli_powerplace_inverted|19703|buli_powerplace_inverted|
|bild_buli_powersky_bottom_left|19706|buli_powersky_bottom_left|
|bild_buli_powersky_bottom_right|19707|buli_powersky_bottom_right|
|bild_buli_powersky_top_left|19704|buli_powersky_top_left|
|bild_buli_powersky_top_right|19705|buli_powersky_top_right|
|wettpartner_ergebnisModul|22150|wettpartner_ergebnisModul|
|wettpartner_livekalender_ankuendigung|33910|wettpartner_livekalender_ankuendigung|
|wettpartner_scoreboard|22149|wettpartner_scoreboard|
|wettpartner_textlink|22148|wettpartner_textlink|
|wettpartner_wettbox_ergebnis_BuLi Home|33906|wettpartner_wettbox_ergebnis_BuLiHome|
|wettpartner_wettbox_ergebnis_Vereinsbuehnen|33980|wettpartner_wettbox_ergebnis_Vereinsbuehnen|
|wettpartner_wettbox_tabelle|33905|wettpartner_wettbox_tabelle|


### Mobile

#### Standard Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|Reminder|12815|banner|
|Content Ad|5720|mrec|
|Medium Rectangle|4459|mrec_btf|
|Medium Rectangle 2|4460|mrec_btf_2|
|Footer Ad|5721|mrec_btf_3|
|Richmedia / Outstream|6419 / 29606|inpage|

#### Special Sport Placements

| Placement Name|Legacy Format ID (Smart)|Appnexus|
| ------------- |:-------------:| -----:|
|wettpartner_ergebnisModul|22150|wettpartner_ergebnisModul|
|wettpartner_livekalender_ankuendigung_mobil|33911|wettpartner_livekalender_ankuendigung|
|wettpartner_scoreboard_mobil|33908|wettpartner_scoreboard|
|wettpartner_textlink_mobil|33913|wettpartner_textlink|
|wettpartner_wettbox_box unter artikel_mobil|33909|wettpartner_textlink|
|wettpartner_wettbox_ergebnis_BuLi Home|33906|wettpartner_wettbox_ergebnis_BuLiHome|
|wettpartner_wettbox_ergebnis_Vereinsbuehnen|33980|wettpartner_wettbox_ergebnis_Vereinsbuehnen|
|wettpartner_wettbox_tabelle|33905|wettpartner_wettbox_tabelle|

## Standard Integration Sample

### [Placement Codes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#3-define-the-ad-placements-for-the-website)

#### Desktop:

`	adPlacements: ["superbanner","superbanner_btf","sky","sky_btf","billboard","mrec","mrec_btf","inpage"],`

#### Mobile:

`	adPlacements: ["banner","mrec","mrec_btf","inpage"],`
### [Placement Sizes](https://github.com/CDPAdSolution/adSolution-Reference/blob/master/publisher-display-reference.md#4-define-the-sizes-for-every-ad-placement)

#### Desktop:

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
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[300,600]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],
     
	},
```

#### Mobile:

```
	adSlotSizes: {
		"banner": [{
			"minWidth": 1,
			"sizes": [[320,50],[320,75],[320,80]]
		}],
     
		"mrec": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,500],[320,75],[320,80],[320,160],[300,300]]
		}],
     
		"mrec_btf": [{
			"minWidth": 1,
			"sizes": [[300,250],[320,500],[320,75],[320,80],[320,160],[300,300]]
		}],
     
		"inpage": [{
			"minWidth": 1,
			"sizes": [[1,1],[640,360],[1000,300]]
		}],
     
	},
```

## Important notes

- A Contentbar is on the website but it is not being used. Please remove it.
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
  
