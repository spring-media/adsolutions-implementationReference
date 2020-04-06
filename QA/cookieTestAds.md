## Option to forceCreativeId by cookie

The adlib is build to read cookies if possible and can use it to enforce a specific ad for an adslot as ast_override_div does.
Since it is a cookie it will be persistent per domain so you will have to remove it manually at the moment.

1. visit the domain you want to use the preview using the device and browser the cookie has to be used.
2. open console and type 
``` 
    document.cookie = "mrec=234567890; path=/;"; 
```
3. go on testing

To remove the cookie also go to console and type:

```
    document.cookie = "mrec=234567890; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```
