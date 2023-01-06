# Reload Ads Event



If you need to reload ads on your own, you can use a custom event, which is loaded into the window via the adlib.
By dispatching the event "reloadAds", you will reload all visible ads inside the current viewport of your site.

This is how it could look as an ES5 cross browser example:


## Reload all visible adSlots

With this snippet you will reload all visible adSlots in the current viewport


```html
<script>
    var ev;
    try {
        ev = new CustomEvent('reloadAds', { 'detail': '' });
    } catch (err) {
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('reloadAds', true, true, { 'detail': '' });
    }
    window.dispatchEvent(ev);
</script>
```


## Reload only one specific adSlot

If you only want to reload one specific adSlot, you can specify it in the `'detail'` parameter:

```html
<script>
    var ev;
    try {
        ev = new CustomEvent('renderAd', {'detail': 'mrec_btf_2'});
    }catch(err){
        ev = document.createEvent('CustomEvent');
        ev.initCustomEvent('renderAd', true, true, {'detail': 'mrec_btf_2'});
    }
    document.dispatchEvent(ev);
</script>
```


## Help
If you have any questions or problem don't hesitate to contact us:

__Ad Technology Team__<br>
  adtechnology@axelspringer.de
