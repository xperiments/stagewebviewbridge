# StageWebViewBridge Class #

## Propierties ##
```
/**
 * Enables / Disables the visibility of the SnapShotBitmap
 * @param mode	Boolean.
 */
public function set snapShotVisible( mode : Boolean ) : void


```


## Methods ##

```
/**
 * @param xpos Indicates the initial x pos
 * @param ypos Indicates the initial y pos
 * @param w Indicates the initial width
 * @param h Indicates the initial height
 */
public function StageWebViewBridge( xpos : uint = 0, ypos : uint = 0, w : uint = 400, h : uint = 400 )

/**
 * Loads a local htmlFile into the webview.
 * 
 * To link files in html use the "applink:/" protocol:
 * <a href="applink:/index.html">index</a>
 * 
 * For images,css,scripts... etc, use the "appfile:/" protocol:
 * <img src="appfile:/image.png">
 * 
 * @param url	The url file with applink:/ protocol
 * 				
 * 				Usage: stageWebViewBridge.loadLocalURL('applink:/index.html');
 */
public function loadLocalURL( url : String ) : void

/**
 * Enhaced loadString
 * Loads a string and inject the javascript comunication code into it. 
 */
public function loadString( text : String, mimeType : String = "text/html" ) : void

/**
 * Creates and loads a temporally file with the provided contents.
 * This way we can access local files with the appfile:/ protocol
 * @params String content
 */
public function loadLocalString( content : String ) : void

/**
 * Sets the size of the StageWebView Instance
 * @param w The width in pixels of StageWebView
 * @param h The heigth in pixels of StageWebView
 */
public function setSize( w : uint, h : uint ) : void

/**
 * draws a snapshot of StageWebView to the Bitmap
 */
public function getSnapShot() : void

/**
 * Makes a call to a javascript function
 * @param functionName Name of the function to call
 * @param callback The callback function to execute when javascript call is processed
 * @param arguments Coma separated arguments to pass to Javascript function
 */
public function call( functionName : String, callback : Function = null, ... arguments ) : void

/**
 * Add a callback function to the current list of avaliable callbacks
 * @param name the name of the callback function in this format : [SWVMethod]( name )
 * @param callback The callback function 
 */
public function addCallback( name : String, callback : Function ) : void

```

## Events ( StageWebViewBridgeEvent ) ##
```
// dispatched on stagewebview image capture get generated
public static const ON_GET_SNAPSHOT : String = "ON_GET_SNAPSHOT";
```
