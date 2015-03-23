**Before continue be sure to read how CacheFileSystem works**

# StageWebViewDisk initialization #

StageWebViewDisk is the responsable of all disk transactions with StageWebViewBridge.

**It is required to initialize the StageWebViewDisk class before we can use a StageWebViewBridge instance.**

There are 2 events that gets dispatched from this class.

**We must listen to the StageWebviewDiskEvent.END\_DISK\_PARSING before create any StageWebViewBridge instance**


**Events**
```
// Dispatched at disk parsing start
StageWebviewDiskEvent.START_DISK_PARSING;
// Dispatched at disk parsing end
StageWebviewDiskEvent.END_DISK_PARSING; 
```

**Example initialization code**

```

// OPTIONAL BEFORE INIT OPTIONS SETTING
StageWebViewDisk.setDebugMode( true ); // if we need debug mode assign it before initializaton

// StageWebViewDisk Events. First time app launches it proceses the filesystem
// As it can take some time, depending of the filesize of the included files
// we provide 2 events to know when process start/finish
			
StageWebViewDisk.addEventListener(StageWebviewDiskEvent.START_DISK_PARSING, onDiskCacheStart);
StageWebViewDisk.addEventListener(StageWebviewDiskEvent.END_DISK_PARSING, onDiskCacheEnd);
StageWebViewDisk.initialize( stage /*Stage instance. Required*/ );	

var bridge:StageWebViewBridge;

function onDiskCacheStart( e:StageWebviewDiskEvent ):void{ /* Do something at process start */ }
function onDiskCacheEnd( e:StageWebviewDiskEvent ):void
{
    //Now is safe to init our StageWebViewBridge class
    bridge = new StageWebViewBridge( 0, 150, 320, 280 );
    .... 
}
```

**TIP**
```
If we are targeting only Mobile we can less the debug mode true all the time, as it din't affect on Mobile
```

---

# StageWebViewBridge extends Bitmap #





As StageWebViewBridge extends bitmapdata, you can do:
```

/**
* StageWebViewBridge Class
* @param xpos Indicates the initial x pos
* @param ypos Indicates the initial y pos
* @param w Indicates the initial width
* @param h Indicates the initial height
* @param autoVisibleUpdate Boolean. Control visibility testing of his parents.
*	  TRUE by Default. Disable it to save some CPU ( as it uses an EXIT_FRAME event listener to work )
*	  then control yourself his visibility. 
*
* @example
*  var testBridge:StageWebViewBridge = new StageWebViewBridge( );
* 
*/

// create StageWebViewBridge instance
var view:StageWebViewBridge = new StageWebViewBridge( 0, 150, 320, 280 );

// add it to the display list
addChild( view );

// move it
view.x = 100;
view.y = 100;

// get a SnapShot for use as the Bitmap's bitmapdata
view.getSnapShot();

// toggle the visibility of the SnapShot  
view.snapShotVisible = true;

// rotate, scale, change alpha ( only when snapShotVisible = true )
view.alpha = .5;
view.rotation = 45;
view.scaleX = .5;
```


---


# Creating a new StageWebViewBridge instance #


**AS3 Code**
```
// create StageWebViewBridge instance
// new StageWebViewBridge( x,y,width,height )
var view:StageWebViewBridge = new StageWebViewBridge( 0, 150, 320, 280 );

// add listener for when page becomes loaded
view.addEventListener( Event.COMPLETE, onViewLoadComplete );

// enable javascript to call function helloWorldFromJS
view.addCallback('helloWorldFromJS', helloWorldFromJS );

// load content to the view
view.loadLocalURL('appfile:/index.html');

// as StageWebViewBridge extends Bitmap
// we can now add it to the displaylist
addChild( view );


// event listener that gets called on page load complete
function onViewLoadComplete( e:Event ):void
{
	trace('view loaded');
	// call a javascript function after the page loads
	// that will do an alert with the date passed from as3
	view.call('helloWorldFromAS3', null, new Date().toString() );
}

// function to be called from JS
function helloWorldFromJS( at:String ):void
{
	trace('helloWorldFromJS called from JavaScript at '+ at );
}

```

**index.html**

```
<html>
<head></head>
<body style="margin:0px; padding:0px">  
<script>
	function helloWorldFromAS3( at )
	{
		alert('helloWorldFromAS3 called from AS3 at '+ at ); 
	}
</script>
<button onclick="StageWebViewBridge.call('helloWorldFromJS',null,new Date().toString() )">Call Actionscript helloWorldFromJS function</button>   
 
</body>
</html>   
```


# Working with SnapShots #

You can get an SnapShot of the view by calling the **getSnapShot** method.

GetSnapShot method works asynchronously, you can listen for the StageWebViewBridgeEvent.ON\_GET\_SNAPSHOT event to know when the bitmapdata is generated

```
view.addEventListener( StageWebViewBridgeEvent.ON_GET_SNAPSHOT, onGetSnapShot );
view.getSnapShot();

function onGetSnapShot( e:StageWebViewBridgeEvent ):void
{
	// remove listener
	view.removeEventListener( StageWebViewBridgeEvent.ON_GET_SNAPSHOT, onGetSnapShot );
	// set the bitmapdata visible, hides de stagewebview
	view.snapShotVisible = true;
}

```