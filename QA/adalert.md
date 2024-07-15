## Bookmark Tool/JS-Code to submit ad errors

This small javascript is meant to be saved as bookmark so you can run it by click.  
It will load a javascript file that checks the placements on the page and sum them up in a small box to the top left corner.  

The code is written in plain javascript so each browser on each device will accept it,  
and therefore it also works on mobile devices or tablets.

##### Please don't modify this code and use it "as is".

```
javascript:!function(){var s=document.createElement("script");s.src="https://www.asadcdn.com/adlib/extensions/adalert.js",document.getElementsByTagName("head")[0].appendChild(s);}();void(0);
```

You can copy the code and insert it in your browser as the url for a new bookmark.  
If you want to use the AdAlert with a smartphone, you can open your browsers bookmark menu and add a new bookmark by inserting the url you just copied.

To trigger the AdAlert on your smartphone, you just have to open the bookmark while you are on the page you want to make the alert about.
In the Alert you can also add screenshots of the issue you are experiencing. Screenshots and a clear description of the experienced issue are always invaluable, as they enable us to accurately reproduce and address the problem, or identify the specific ads responsible for the issue.

<br />

#### Definitions

Color | stands for | means
--- | --- | ---
green | delivered | ad should be visible
orange | mediation noBid | there was no higher programmatic bid
light grey | not rendered now | either slot is missing or it will be rendered on scroll
dark grey | blocker | a creative blocker
rose | foreignId | an ID passed by the partners redirect

_The number after the creative id shows the member the ad belongs to the Xandr seat_


