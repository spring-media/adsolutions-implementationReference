# AdLib Message Service

After receiving the response from the adserver our adlib analyses the result and communicates it through an event.
To receive this information you just setup an eventListener to listen to `adInfo` Event.

```
window.addEventListener("adInfo", function(adSlot) {
    console.log(adSlot);
});
```
In the given argument you will receive all information gathered to the actual adslot, best way to see what you receive is to inspect it via `console.log()`.

The most important information though will be this:

Property | Type | Always available? | Used for
--- | --- | --- |--- 
adSlot.detail.id | *string* | yes | the adSlot container id e.g. `superbanner`, `billboard_btf` ...
adSlot.detail.hasAd | *boolean* | yes | let's you know if there is an ad.
adSlot.detail.hasMarker | *boolean* | no | let's you know if the ad brings its own marker.
adSlot.detail.placementSize | *string* | no | the size of the adplacement the winning bid is booked to
adSlot.detail.tempName | *string* | empty when `hasAd` is false | identifies the adformat, e.g. videowall, fireplace, oneTag etc.
adSlot.detail.crea1.height | *string* | no | the real base-height of the first creative of the adformat
adSlot.detail.crea1.width | *string* | no | the real base-width of the first creative of the adformat

## Usage

```javascript
window.addEventListener("adInfo", function(adSlot) {
	if (! adSlot.detail.hasAd) {
        document.getElementById(adSlot.detail.id).style.display = 'none';
	}
});
```


