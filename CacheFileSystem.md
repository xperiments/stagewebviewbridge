# Cache FileSystem ( Updated 1.0 Beta ) #

Working with localfiles is tedious. You must provide paths with a native path.

To overcome this situation we have provide StageWebViewBridge with new ways of referencing resources as we have explained in [ContentLoading](ContentLoading.md)

# How Cache system works #


## Begin the scenes ##

But, what happends begin the scenes?

StageWebViewBridge will assume that the "root" dir of your web files is the "www" directory inside your File.applicationDirectory.

### Explanation of directories ###
```
app:/www................This is your working directory.
			Put inside it all your html project files.
			Make only changes in files of this directory.!!! 

app:/wwwSource..........Contains parsed sources and files.

```

## Debug Mode ON/OFF ##

Every time you compile your projects, depending of the debug and current plattform StageWebViewBridge will do:

**StageWebViewDisk.setDebugMode( true )**

> #### DESKTOP ####
```
wwwSource dir will be generated in the applicationDirectory dir and used as the www root folder
```
> #### iOS ####
```
 www dir will be used as the www root folder
```
> #### ANDROID ####
```
 wwwSource dir will be generated in the applicationStorageDirectory dir and used as the www root folder
```

**StageWebViewDisk.setDebugMode( false )**

> #### DESKTOP ####
> <font color='#FF0000'>ATTENTION <b>BE SURE TO BACKUP YOUR WWW DIR BEFORE DO THIS, AS THE FILES WILL BE OVERWRITTEN</b></font>
```
 www dir will be used as the www root folder
```

> #### iOS ####
```
 www dir will be used as the www root folder
```
> #### ANDROID ####
```
 wwwSource dir will be generated in the applicationStorageDirectory dir and used as the www root folder
```


## Public Methods ##

**.setDebugMode**
```
/**
 * Enables / Disables DEBUG MODE
 */
public static function setDebugMode( mode : Boolean = true ) : void
```

**.setExtensionsToProcess**
```
/**
 * Sets the file extensions that must be preparsed into cache 
 * @param extensions Array of extensions ex.:["html","htm","css","js"]
 * 
 */
public static function setExtensionsToProcess( extensions : Array ) : void
```

**.createFile**
```
/**
 * Creates and parses a new file with the provided contents.
 * @param fileName the full filename in this format: "appfile:/exampledir/examplefile.html"
 * @param contents Contents of the file.
 * @param isHtml Boolean indicatin if file is an htmlFile ( used to inject js code in the html files );
 */
public static function createFile( fileName : String, contents : String, isHtml : Boolean = true ) : File
```

**.getFilePath**
```
/**
 * Returns the native path for the fileName
 * @param fileName Name of the file
 */
public static function getFilePath( url : String ) : String
```

**.getRootPath**
```
/**
 * Returns the Main path to the www root filesystem
 */
public static function getRootPath() : String
```

**.getSourceRootPath**
```
/**
 * Return the path of the cached files dir ( DESKTOP/ANDROID == getRootPath | iOS = "app:/www" as this uses less cache files )
 */
public static function getSourceRootPath() : String
{
	return _applicationSourcesDirectory;
}
```