# AdLib Message Service

After receiving the response from the adserver our adlib analyses the result and communicates it through an event.
To receive this information you just setup an eventListener to listen to "adInfo".

```
window.addEventListener("adInfo", function(adSlot) {
    console.log(adSlot);
});
```
In the given argument you will receive all information gathered to the actual adslot, best way to see what you receive is to inspect it via console.log().

The most important information though will be this:

Property | Type | used for
--- | --- | --- 
adSlot.id | *string* | the adSlot container id e.g. superbanner, billboard_btf ...
adSlot.hasAd | *boolean* | let's you know if there is an ad.
adSlot.hasMarker | *boolean* | let's you know if the ad brings an own marker.
adSlot.placementSize | *string* | the size of the adplacement the winning bid is booked to
adSlot.tempName | *string* | identifies the adformat, e.g. videowall, fireplace, oneTag etc.
adSlot.crea1.height | *string* | the real base-height of the first creative of the adformat
adSlot.crea1.width | *string* | the real base-width of the first creative of the adformat

Given this you can do things like this:

```
window.addEventListener("adInfo", function(adSlot) {
	if (!adSlot.hasAd) {
        document.getElementById(adSlot.id).style.display='none';
	}
});
```


