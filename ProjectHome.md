<font color='#FF0000'>22/11/2011 New Version 1.0 Beta 3, Added Basic examples, Adobe Docs, fixed some bugs</font>


# StageWebViewBridge #

StageWebViewBridge is an extended version of flash.media.StageWebView.

  * Extends Bitmap class, you can modify his x,y,alpha,rotation,visible,  etc ( Version 1 Beta )
  * Communicates Actionscript with Javascript.
  * Communicates Javascript with Actionscript.
  * Load local files and resources in a easy way.
  * Extends loadString method with AS3 - JS communication.
  * Extends loadString method to load local resources.
  * Lets you take an SnapShot to use as the bitmapData of the bitmap.


By example you can call javascript from as3
```
// call javascript with callack function
webView.call('someFunctionToCall', callBackFunction, ...arguments );

// reference local resources in a easy way
<img src="appfile:/image.png">
```

## Downloads ##


**Lattest swc** [swc](http://code.google.com/p/stagewebviewbridge/source/browse/#svn%2Ftrunk%2FStageWebViewBridge%2Fdownload)

StageWebViewBridge27.zip is meant to be used with AIR 2.7 or LOWER.

StageWebViewBridge\_svn ... .zip is meant to be used with AIR 3.0 or HIGHER.

**Asdocs**

Download the documentation [here](http://stagewebviewbridge.googlecode.com/svn/trunk/StageWebViewBridge/download/asdocs.zip)

**Examples**

You can download the examples
[here](http://stagewebviewbridge.googlecode.com/svn/trunk/StageWebViewBridge/download/@swvb_examples.zip)


## Avaliable wiki pages ##

Manage local resources and cache: [CacheFileSystem](CacheFileSystem.md)

Usage: [Usage](Usage.md)

Communication between as3 and javascript and vice versa: [Communication](Communication.md)

Load local files and reference resources: [ContentLoading](ContentLoading.md)

The StageWebViewBridge Class: [StageWebViewBridgeClass](StageWebViewBridgeClass.md)

The StageWebViewDisk Class: [StageWebViewDiskClass](StageWebViewDiskClass.md)