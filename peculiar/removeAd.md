# manual for dynamically removing adplacements

Some circumstances may require to remove adplacements dynamically.

In this case you should inform the adlib by calling an adlib event:

``` html
// the wrapper can be styled as you like to, for floating the ad next to the content or whatever, but please do not style the adSlot directly
<div id="billboard_btf_2_wrapper" class="billboard_Wrapper" style="float:right; width:300px;">...</div>

<script>
    var ev = new CustomEvent('removeAd', {'detail': 'billboard_btf_2'});
    document.dispatchEvent(ev);
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
