# Reload Ads Event



If you need to reload ads on your own, you can use a custom event, which is loaded into the window via the adlib.
By dispatching the event "reloadAds", you will reload all visible ads inside the current viewport of your site.

This is how it could look as an ES5 cross browser example:



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



## Help
If you have any questions or problem don't hesitate to contact us:

__Ad Technology Team__
  adtechnology@axelspringer.de
