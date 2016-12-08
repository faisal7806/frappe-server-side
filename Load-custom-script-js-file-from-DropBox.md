If you want to load a .js file from DropBox as a custom script, you can use the following code in your custom script file:

```
var script = document.createElement("script");
script.type = "text/javascript";
script.src = "https://www.dropbox.com/s/yeoasv2glsve0za/tut.js?raw=1";
script.onload = function(){
console.log("Agent_Calculator Loaded");
};
 
document.head.appendChild(script);
```
The line `script.src = "https://www.dropbox.com/s/yeoasv2glsve0za/tut.js?raw=1";` needs to be updated with your own file hosted on DropBox.

When you get a share link in DropBox, in this case the file shown above, it will look like:
`https://www.dropbox.com/s/yeoasv2glsve0za/tut.js?dl=0`

You must replace `dl=0` with `raw=1`.  Once you have done that, you can paste it into the script as shown above.  

The file in the example is valid and can be used for testing.