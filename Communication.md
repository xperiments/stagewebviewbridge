## Creating a new instance ##

```
var webView:StageWebViewBridge = new StageWebViewBridge( 0,0,400,400 );
addChild( webView );
```

## Calling Javascript from Actionscript ##
```
// call javascript method
webView.call('someFunctionToCall');

// call javascript method width parameters
webView.call('someFunctionToCall', null, ...arguments );

// call javascript with callack function
webView.call('someFunctionToCall', callBackFunction, ...arguments );
```

## Enabling actionscript functions to be called from javascript ##
```
webView.addCallback("functionToCall", as3FunctionHandler );
```


## Calling Actionscript from Javascript ##
```

// call actionscript method
StageWebViewBridge.call('someFunctionToCall');

// call actionscript method width parameters
StageWebViewBridge.call('someFunctionToCall', null, ...arguments );

// call actionscript with callback function
StageWebViewBridge.call('someFunctionToCall', callBackFunction, ...arguments );
```