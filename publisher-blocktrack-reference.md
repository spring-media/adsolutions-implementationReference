# BlockTrack HTML-Tag

Please integrate the following HTML-Tag at the end of the page and
make sure it gets loaded after adSSetup is defined


```html
<!-- Start Blocktrack-Integration -->
<script type='text/javascript'>
(function(){
    var view = window.adSSetup ? adSSetup.view : ((location.host.match(/^m\.|^wap\.|^mobil.*\./i) || (window.screen && screen.availWidth && (screen.availWidth <= 800))) ? 'm' : 'd');
    var f = (view === 'd') ? 's' : 'm';
    var x, p = document.createElement('img');
    p.style.cssText = 'display:none;visibility:hidden;position:absolute;left:-99999px;top:-99999px;width:0;height:0;';
    p.onerror = function() {
        x = document.createElement('img').src = 'https://www.asadcdn.com/bt/' + f + '.png?b=1';
    };
    p.onreadystatechange = p.onload = function() {
        if (!this.readyState || this.readyState === 'loaded' || this.readyState === 'complete'){ 
            x = document.createElement('img').src = 'https://www.asadcdn.com/bt/' + f + '.png?b=0'; p.onload = p.onreadystatechange = null;
        }
    };
    p.src = 'https://acdn.adnxs.com/ast/static/bar.jpg';
    document.body.appendChild(p);
})();
</script>
<noscript><img style='display:none;' src='https://www.asadcdn.com/bt/s.png?b=2' /></noscript>
<!-- End Blocktrack-Integration -->
```
