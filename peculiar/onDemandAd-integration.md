# manual for dynamically use adplacements

Some circumstances may require to use adplacements dynamically, e.g. if you want to use an adplacement after changing or adding content.

To do so you need to make sure you already defined the configuration for the new adplacement.
If you're sure you did so you may just inject the adplacement into the DOM and tell the adlib:

``` html
// the wrapper can be styled as you like to, for floating the ad next to the content or whatever, but please do not style the adSlot directly
<div id="billboard_btf_2_wrapper" class="billboard_Wrapper" style="float:right; width:300px;">
    <div id="billboard_btf_2" data-target="pos=7"></div>
    <script>
        var ev = new CustomEvent('renderAd', {'detail': 'billboard_btf_2'});
        document.dispatchEvent(ev);
    </script>
</div>
```

Otherwise you can follow this guide to setup everything for the adplacement dynamically.
Everything here is written in plain javascript and wrapped into a script tag for demonstration,
but you may also integrate this codes into your codebase at it fits best:

### Part 1 - make sure sizes are defined
The adlib will respect the sizes that are set by the adSSetup right to the time the adcalls are invoked.
So to ensure the sizes for the actual adrequest are set you may redefine it at all time.
In the example we will check if there are sizes already and add those we miss:

```html
<script>
    if (adSSetup.adSlotSizes["billboard_btf_2"]) {
        adSSetup.adSlotSizes["billboard_btf_2"][0].sizes = adSSetup.adSlotSizes["billboard_btf_2"][0].sizes.concat([
            [427, 23],
            [300, 150],
            [300, 250]
        ]);
    } else {
        adSSetup.adSlotSizes["billboard_btf_2"] = [{
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
<div id="billboard_btf_2_wrapper" class="billboard_btf_2_Wrapper" style="float:right">
    <div id="billboard_btf_2" data-target="contest=bundesliga;"></div>
</div>
```

### Part 4 - request an ad
Since we now have set all preparations we will order an ad one per adslot.
This example shows an cross-browser solution to do so for the adslot div#billboard_btf_2:

```html
<script>
    var ev;
    try {
        ev = new CustomEvent('renderAd', {'detail': 'billboard_btf_2'});
    }catch(err){
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('renderAd', true, true, {'detail': 'billboard_btf_2'});
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
    if (adResponse.tempName === "wallpaper") {
        // a wallpaper needs place to the right, so maybe one needs to bound the dimensions of the content
        document.getElementById("content").style.width = "calc(100% - 300px)";
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
