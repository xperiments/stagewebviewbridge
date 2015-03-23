# StageWebViewDisk Class #

## Properties ##

```
public static const isIPHONE	: Boolean;
public static const isANDROID	: Boolean;
public static const isMOBILE	: Boolean; 
public static const isLINUX	: Boolean;  
public static const isMAC	: Boolean;    
public static const isWINDOWS	: Boolean;
public static const isDESKTOP	: Boolean;
```


## Static Methods ##
```

/**
 * Main init function
 */
public static function initialize() : void

/**
 * Enables / Disables DEBUG MODE
 */
public static function setDebugMode( mode : Boolean = true ) : void

/**
 * Sets the file extensions that must be preparsed into cache 
 * @param extensions Array of extensions ex.:["html","htm","css","js"]
 * 
 */
public static function setExtensionsToProcess( extensions : Array ) : void

/**
 * Creates and parses a new file with the provided contents.
 * @param fileName the full filename in this format: "appfile:/exampledir/examplefile.html"
 * @param contents Contents of the file.
 * @param isHtml Boolean indicatin if file is an htmlFile ( used to inject js code in the html files );
 */
public static function createFile( fileName : String, contents : String, isHtml : Boolean = true ) : File

/**
 * Returns the native path for the fileName
 * @param fileName Name of the file
 */
public static function getFilePath( fileName : String ) : String

/**
 * Returns the path to the www root filesystem
 */
public static function getRootPath( ) : String

```


## Events ( StageWebviewDiskEvent ) ##
```
public static const START_DISK_PARSING : String;
public static const END_DISK_PARSING : String;
```