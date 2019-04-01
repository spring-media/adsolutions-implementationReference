# adcall propagation service for adlib pageSet integration

This script is meant to be integrated in third party iframes to get adcalls by pageInfo like pageName, target, view and so on given by the parent frame.
It is written threeway integrational so it can be used for popups, friendly iframes (fif) and cross-origin frames.

```
<script type="text/javascript">
var displaySizes = [[300,250],[320,50]]; // please refer to briefing what sizes to set
var partnerName = ""; // e.g. "bild.de", please refer to briefing - maybe optional
var pageName = ""; // e.g. "spiele.partner1", please refer to briefing - maybe optional
var slot = "mrec"; // containerId for display ad - please refer to briefing
var vwidth = ""; // optional, the static width of the videoplayer used for videoadcall
var vheight = ""; // optional, the static height of the videoplayer used for videoadcall

var propagateAdUrls = function(msg) {
	console.log(msg.datail);
    // you can add your render method or a call to it here and remove the rest
    // or add a div#${slot} to your html and call:
    renderAdFrame(msg.detail.display);
};

// if you do not support IE <= 9 you may use the second line only
(window.addEventListener) ? 
	window.addEventListener("adInfo", function(msg){propagateAdUrls(msg);}, false) 
	: window.attachEvent("onadInfo", function(msg){propagateAdUrls(msg);});
</script>
<script type="text/javascript" src="https://www.asadcdn.com/adlib/extensions/corsFrameAdCalls.js"></script>
```

## Contact

__Team AdTechnology__
  [adtechnology@axelspringer.de](mailto:adtechnology@axelspringer.de)

