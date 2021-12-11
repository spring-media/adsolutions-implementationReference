# manual for dynamically use adplacements

### Part 1 - make sure sizes are defined
The adlib will respect the sizes that are set by the adSSetup right to the time the adcalls are invoked.
So to ensure the sizes for the actual adrequest are set you may redefine it at all time.
In the example we will check if there are sizes already and add those we miss:

```html
<script>
    if (adSSetup.adSlotSizes["betad_2"]) {
        adSSetup.adSlotSizes["betad_2"][0].sizes = adSSetup.adSlotSizes["betad_2"][0].sizes.concat([
            [427, 23],
            [300, 150],
            [300, 250]
        ]);
    } else {
        adSSetup.adSlotSizes["betad_2"] = [{
            minWidth: 1,
            sizes: [
                [427, 23],
                [300, 150],
                [300, 250]
            ]
        }]
    }
</script>
```

### Part 2 - register an listener to receive info from adlib per adslot
The adlib will provide info per adslot to everybody who listens to "adInfo" events.
The event will have many information to react or also explicitly not react, you may see by yourself,
using the code from the following example

```html
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

```html
<div id="betad_2_wrapper" class="betad_Wrapper" style="float:right">
    <div id="betad_2" data-target="contest=bundesliga;"></div>
</div>
```

### Part 4 - request an ad
Since we now have set all preparations we will order an ad one per adslot.
This example shows an cross-browser solution to do so for the adslot div#betad_2:

```html
<script>
    var ev;
    try {
        ev = new CustomEvent('renderAd', {'detail': 'betad_2'});
    }catch(err){
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('renderAd', true, true, {'detail': 'betad_2'});
    }
    document.dispatchEvent(ev);
</script>
```

### Part 5 - decide what to do with the adInfo
The adlib will now start an adrequest and after it finished every listener from Part 2 will be informed.
In the following example we will check if the property tempName is one of we're interested in
and if it is we will invoke an own method to handle the response:

```html
<script>
window.addEventListener("adInfo", function(adSlot) {
    var adResponse = adSlot.detail;
    if (adResponse.tempName === "heimspiel") {
        // start rendering quotes for advertiser to div with id matching adResponse.contId
        _hs.renderQuotes(adResponse.advertiserName, adResponse.contId);
    }
});
</script>
```

## Help

If you have some question don't hesitate to contact us:


__Carlos Bracho__
 
  Senior Ad Technology Lead 
  Corporate Digital Platforms
  
  Tel: +49 30 2591 76784
  Mobile: +49 151 44619807 
  carlos.bracho@axelspringer.de

__Ad Technology Team__
  adtechnology@axelspringer.de
