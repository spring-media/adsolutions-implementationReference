## Bookmark Tool/JS-Code to submit aderrors

This small javascript is meant to be saved as bookmark so you can run it by click.
It will check the placements on the page and sum them up in a small box to th top left corner.

The code is written in plain javascript so each browser  on each device will accept it,
and theirfore it also works on mobile devices or tablets.

```

javascript:!function(){if(window.ASCDP){var e="Liebes%20ADS-Team,%250A%20%250Aleider%20gab%20es%20folgenden%20Fehler:%250A%250AWerbeelement:%20__XXX__%20%250AURL:%20"+encodeURIComponent(location.href)+"%250AUser-Agent:%20"+encodeURIComponent(navigator.userAgent)+"%250A%250AFehlerbeschreibung%20(wenn%20möglich%20mit%20Screenshot):%250A%250A...%250A%250AFolgende%20Insertions%20waren%20aktiv:%250A",n="<h5 style='text-decoration: underline; margin: 0; color: #000'>AxelSpringer Digital - Loaded Ads</h5><br/><ul style='list-style-type: none; padding: 0;'>";for(var t in ASCDP.adS.adElts)if(ASCDP.adS.adElts.hasOwnProperty(t)){var i=ASCDP.adS.adElts[t].contId,d=document.createElement("div");d.style.cssText="position: absolute;top: 0;background: red;font: bold 16px black;padding: 5px; font-family: 'Segoe UI', sans-serif;",d.innerHTML="Placement: "+i+" - "+(ASCDP.adS.adElts[t].insertionId||"N/A");var o=document.getElementById(i);o&&(o.appendChild(d),o.style.cssText+="position:relative;min-height: 30px;"),n+="<li><span style='display:inline-block; min-width:120px;'>"+ASCDP.adS.adElts[t].contId+": </span><span style='display:inline-block; width:100px;'>"+(ASCDP.adS.adElts[t].hasAd?ASCDP.adS.adElts[t].insertionId||"InsertionId missing":"noad")+"</span></li>",e+="%250A"+i+":%20"+(ASCDP.adS.adElts[t].insertionId||"InsertionId missing")}ASCDP.mailbody="mailto:ads@axelspringer.de?Subject=Fehlerhaftes%20Ad&body="+e+"%250A%250AMit%20freundlichen%20Grüßen%250A",n+='</ul><br/><a style="color:blue" href="'+ASCDP.mailbody+'">ads@axelspringer.de</a><span id="cancelSlider" style="position:absolute;width: 24px;height: 24px;top: 0;right: 0;cursor:pointer;z-index: 999999;background: url(\'https://www.smartadserver.com/diff/templates/images/buttons.png\');background-position: -53px 0;" onclick="javascript:document.body.removeChild(document.getElementById(\'miBox\'));"></span>';var a=document.createElement("div");a.id="miBox",a.style.cssText="z-index: 999999999; padding: 5px; position:fixed; top: 0; left: 0; width: 250px; background: #DF0029; font: bold 14px black; font-family: 'Segoe UI', sans-serif;",a.innerHTML=n,document.body.appendChild(a)}}(document);

```

Please don't modify this code and use it "as is".

To add a bookmark please see Google - for Chrome e.g. please visit this site:
https://support.google.com/chrome/answer/188842?co=GENIE.Platform%3DDesktop&hl=en
