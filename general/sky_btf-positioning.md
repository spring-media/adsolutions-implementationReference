## Positioning of Sky_btf placements

> Since the positioning of the sky_btf placement can be a bit tricky to implement and not every publisher has the resources to do so, we want to provide you with a possible solution.

**Important**: *This document is only relevant, if you plan to deliver Sky_btf placements on your page.<br>If you only use the usual Sky placement, you don't need this.*

<br>

### First: the requirements

If you deliver Sky_btf placements on your page, you should be sure, that the page is long enough.<br>
**The Sky_btf has to be placed at 50% page height, but needs at least 2500px to the top.**<br><br>
This is very important - imagine you have paid a big amount of money for an advertising campaign that is only seen for 1000px 
and the rest of the 18.000px height page is blocked by a programmatic sky which costs a lot less.

<br>


### Code sample

Just one way you could implement the positioning is via Javascript.
You can use the following logic to place the slot on the page:

```Javascript

const reposSkyBtf = function () {
    var skyBtf = document.getElementById("${ADD_ID_OF_SKY_BTF_WRAPPER}");
    var newHeight = document.documentElement.scrollHeight / 2;
    if (skyBtf) {
        if (newHeight > 2500) {
            skyBtf.style.top = newHeight / 2 + "px";
        } else {
            skyBtf.style.top = "2500px";
        }
    }
};

```

<br>

Also you maybe would set your wrapper to `display:none` before setting top and when top is set apply `display:block` to be sure it does not get rendered before.


