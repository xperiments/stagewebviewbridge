# Content Loading #

**Before continue be sure to read how CacheFileSystem works**

## Introduction ##
To accomplish with the loading of different resources we introduce 3 new protocols.
```
applink:/ --> links between local documents
appfile:/ --> reference to images/scripts/css etc
jsfile:/ --> used in JS to get a file path with StageWebViewBridge.getFilePath('jsfile:/fileinroot.html') 
```

### Linking between pages in html ###
```
<a href="applink:/someDir/someFile.html">Link</a>
```

### Referencing images, scripts, etc in html ###
```
<img src="appfile:/image.png">
<script src="appfile:/myScript.js"></script>
```


---

# Loading content from Online #

<font color='#FF0000'>To load content from online resources we use the standard webView.loadURL( url ) method, <b>but if we LIKE COMM TO GET WORKING, we MUST include the StageWebViewBridge.js inside the online file</b>.</font>


---

# Different load methods #

## .loadURL( url:String ) ##

Standard method of loading content

```
 webView.loadURL( url );
```

## .loadLocalURL( url ) ##

Lets us load content from our www directory.

The benefits of use this method other than loadURL method is that we can refer resources like:
```
appfile:/image.png
```

It also injects the necesary code to establish communication with actionscript.

**Example**
```
// load document.html from www root directory
webView.loadLocalURL("applink:/document.html");
// load index.html that is inside the html directory in www root directory
webView.loadLocalURL("applink:/html/index.html");
```

## .loadString( text : String, mimeType : String = "text/html" ) ##

Same as the standard loadString method, but also injects the necesary code to make bidirectional communication between AS3 and JS.

**Attention:**
```
You must provide a valid html code because the injection finds the <head> tag to inject the script.
```

**Example**
```
var html:String = '<html><head><head><body>Hello World</body></html>';
webView.loadLocalString( html );
```


## .loadLocalString( text : String, mimeType : String = "text/html" ) ##

Creates a temporally file in the filesystem with the text provided.
This lets us reference local files with the diferents protocols provided.

**Attention:**
```
You must provide a valid html code because the injection finds the <head> tag to inject the script.
```

**Example**
```
var html:String = '<html><head><head><body><img src="appfile:/image.jpg"></body></html>';
webView.loadLocalString( html );
```