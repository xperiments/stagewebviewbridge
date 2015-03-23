# How to use with Flex #

To use StageWebViewBridge class inside your projects you must ( at least ), create a container class that extends UIComponent and assign focusEnabled to it.



By example:

```

package es.xperiments.media
{
	import mx.core.UIComponent;

	public class SWVBUIComponent extends UIComponent
	{
		public function SWVBUIComponent()
		{
			super();
			focusEnabled = false;
		}
	}
}



```

Then i MXML code:
```
<?xml version="1.0" encoding="utf-8"?>
<s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
		xmlns:s="library://ns.adobe.com/flex/spark"
		title="HomeView"
		addedToStage="view1_addedToStageHandler(event)" xmlns:mx="library://ns.adobe.com/flex/mx" xmlns:local="*" xmlns:media="es.xperiments.media.*">
	
	<fx:Script>
		<![CDATA[
			import es.xperiments.media.StageWebViewBridge;
			import es.xperiments.media.StageWebViewBridgeEvent;
			import es.xperiments.media.StageWebViewDisk;
			import es.xperiments.media.StageWebviewDiskEvent;
			
			import flash.media.StageWebView;
			
			import spark.events.ViewNavigatorEvent;
			
			protected var webView:StageWebViewBridge;
			
			protected function view1_addedToStageHandler(event:Event):void
			{
				// OPTIONAL BEFORE INIT OPTIONS SETTING
				StageWebViewDisk.setDebugMode( true );
				// if we need debug mode assign it before initializaton
				// StageWebViewDisk Events. First time app launches it proceses the filesystem
				// As it can take some time, depending of the filesize of the included files
				// we provide 2 events to know when process start/finish
				
				StageWebViewDisk.addEventListener(StageWebviewDiskEvent.START_DISK_PARSING, onDiskCacheStart);
				StageWebViewDisk.addEventListener(StageWebviewDiskEvent.END_DISK_PARSING, onDiskCacheEnd);
				StageWebViewDisk.initialize( this.stage );
			}
			
			protected function onDiskCacheStart(e:StageWebviewDiskEvent):void
			{
				trace("SWVD parsing started");
			}
			
			protected function onDiskCacheEnd(e:StageWebviewDiskEvent):void {
				trace("SWVD parsing ended");
				webView = new StageWebViewBridge(0, 50, 400, 450);
				webView.addEventListener(Event.ADDED_TO_STAGE, onAddedToStage);
				SWVB.addChild(webView);
			}
			
			protected function onAddedToStage(e:Event):void
			{
				webView.loadURL("http://www.google.com");
				//webView.loadLocalURL("applink:/index.html");
			}
		]]>
	</fx:Script>
	<media:SWVBUIComponent id="SWVB" width="400" height="450"/>
</s:View>
```