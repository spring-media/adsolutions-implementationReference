# manual for dynamically use adplacements

### Part 1 - make sure sizes are defined
The adlib will respect the sizes that are set by the adSSetup right to the time the adcalls are invoked.
So to ensure the sizes for the actual adrequest are set you may redefine it at all time.
In the example we will check if there are sizes already and add those we miss:

```
<script>
    if (adSSetup.adSlotSizes["mrec_btf_2"]) {
        adSSetup.adSlotSizes["mrec_btf_2"][0].sizes.concat([
            [300, 250],
            [427, 23]
        ]);
    } else {
        adSSetup.adSlotSizes["mrec_btf_2"] = [{
            minWidth: 1
            sizes: [
                [300, 250],
                [427, 23]
            ]
        }]
    }
</script>
```

### Part 2 - register an listener to receive info from adlib per adslot
The adlib will provide info per adslot to everybody who listens to "adInfo" events.
The event will have many information to react or also explicitly not react, you may see by yourself,
using the code from the following example
```
<script>
window.addEventListener("adInfo", function(adSlot) {
    console.log(adSlot);
});
</script>
```
For further information on this feature please see its [reference](../publisher-loadHandler-reference.md)

### Part 3 - add an adslot to receive adserver response
The adservers framework works with the HTML attribute id to render its codes,
so we need a node for each adplacement to process.
This example shows a node for direct integration into the HTML, but you may also append it by javascript.
It uses a wrapper node element that may be styled (your space), please not use CSS directly on the adslot itself (our space):
```
<div id="mrec_btf_2_wrapper" class="mrec_btf_Wrapper" style="float:right">
    <div id="mrec_btf_2></div>
</div>
```

### Part 4 - request an ad
Since we now have set all preparations we will order an ad one per adslot.
This example shows an cross-browser solution to do so for the adslot div#mrec_btf_2:
```
<script>
    var ev;
    try {
        ev = new CustomEvent('renderAd', {'detail': 'mrec_btf_2'});
    }catch(err){
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('renderAd', true, true, {'detail': 'mrec_btf_2'});
    }
    window.dispatchEvent(ev);
</script>
```

### Part 5 - decide what to do with the adInfo
The adlib will now start an adrequest and after it finished every listener from Part 2 will be informed.
In the following example we will check if the property tempName is one of we're interested in
and if it is we will invoke an own method to handle the response:
```
<script>
window.addEventListener("adInfo", function(adSlot) {
    var adResponse = event.detail;
    if (adResponse.tempName === "heimspiel") {
        // start rendering quotes for advertiser to div with id matching adSlot.contId
        _hs.renderQuotes(adResponse.advertiserName, adSlot.contId);
    }
});
</script>
```