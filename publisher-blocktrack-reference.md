# BlockTrack HTML-Tag

Please integrate the following HTML-Tag at the end of the page and
make sure it gets loaded after adSSetup is defined


```html
<!-- Start Blocktrack-Integration -->
<script type='text/javascript'>
(function(){
    var f = (adSSetup.view === 'd') ? 's' : 'm';
    var p = document.createElement('img');
    p.style.display = 'none';
    p.onerror = function() {
        var x = document.createElement('img').src = 'https://bt.mediaimpact.de/' + f + '.png?b=1';
    };
    p.onreadystatechange = p.onload = function() {
        if (!this.readyState || this.readyState === 'loaded' || this.readyState === 'complete'){ 
            var x = document.createElement('img').src = 'https://bt.mediaimpact.de/' + f + '.png?b=0'; p.onload = p.onreadystatechange = null;
        }
    };
    p.src = 'https://acdn.adnxs.com/ast/static/bar.jpg';
    document.body.appendChild(p);
})();
</script>
<noscript><img style='display:none;' src='https://bt.mediaimpact.de/s.png?b=2' /></noscript>
<!-- End Blocktrack-Integration -->
```
