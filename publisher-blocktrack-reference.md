# Please integrate the following HTML-Tag at the end of the page 

make sure you place it after you defined adSSetup


```html
<!-- Start Blocktrack-Integration -->
<script type='text/javascript'>
(function(){
    var f = (adSSetup.view === 'd') ? 's' : 'm';
    var p = document.createElement('script');
    p.style.display = 'none';
    p.onerror = function() {
        var x = document.createElement('img').src = 'https://bt.mediaimpact.de/' + f + '.png?b=1';
    };
    p.onreadystatechange = p.onload = function() {
        if (!this.readyState || this.readyState === 'loaded' || this.readyState === 'complete'){ 
            var x = document.createElement('img').src = 'https://bt.mediaimpact.de/' + f + '.png?b=0'; p.onload = p.onreadystatechange = null;
        }
    };
    p.src = '//ec-ns.sascdn.com/diff/251/verify.js';
    document.head.appendChild(p);
})();
</script>
<noscript><img style='display:none;' src='https://bt.mediaimpact.de/s.php?b=2' /></noscript>
<!-- End Blocktrack-Integration -->
```
