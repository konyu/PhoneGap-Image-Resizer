# Image Resizer plugin for Phonegap #

The plugin will resize images natively using phonegap's plugin architecture

## Adding the Plugin to your project ##

Using this plugin requires [PhoneGap](http://github.com/phonegap).

1. To install the plugin, copy imageresize.js to your project's www folder and include it in your html file after phonegap.js. The file is compatible with both iOS and Android (was not tested with others).

    &lt;script type="text/javascript" charset="utf-8" src="phonegap.js"&gt;&lt;/script&gt;<br/>
    &lt;script type="text/javascript" charset="utf-8" src="imageresize.js"&gt;&lt;/script&gt;

2. For Android: Create a new package within your project called "com.webXells.ImageResizer" and move ImageResizePlugin.java into it.
3. For iOS : Coming soon, sorry guys :-)

## Using the plugin ##

The plugin creates the object `window.plugins.imageResizer`.  To use, call one of the following, available methods:

<pre>
   window.plugins.imageResizer.resizeImage(successCallBack, failCallBack, imageData, width, height, options);
   window.plugins.imageResizer.getImageSize(successCallBack, failCallBack, imageData, options);
   window.plugins.imageResizer.storeImage(successCallBack, failCallBack, imageData, options);
</pre>

For Example:
<pre>
    window.plugins.imageResizer.resizeImage(

    function(data) { console.log(data.imageData); }, function (error) {
        console.log("Error : \r\n" + error);
    }, imageDataInBase64, 0.5, 0.5, {resizeType:ImageResizer.RESIZE_TYPE_FACTOR ,format:'jpg'});
</pre>

### Android quirks and howto's ###

Write down plugin.xml

 <plugin name="ImageResizer" value="com.webXells.ImageResizer.ImageResizePlugin"/>

The storeImage funtion will always store the image to the device's default external storage, under the given Directory and filename. the photoAlbum property will be ignored.



### iOS quirks and howto's ###

For a full iOS integration, two extra extensions should be used:
1. Base64 Encoder/Decoder using Dave Wimer implementation (http://colloquy.info/project/browser/trunk/NSDataAdditions.h?rev=1576)
2. Image Scaling for UIImage (Using the great howto guide here : http://iphonedevelopertips.com/graphics/how-to-scale-an-image-using-an-objective-c-category.html )
The sources are added to the github.

The storeImage funtion in iOS saves either in the photo album, or in the application's temporary directory. 
In the first case (photo album is set to true), the filename and directory will be completly ignored. A filename will be decided by iOS itself.
In the second case, only filename will be used and directory will be ignored.
	
## JavaScript doc ##
	
### resizeImage Doc ###
<pre>
  param success success callback, will receive the data sent from the native plugin
  param fail error callback, will receive an error string describing what went wrong
  param imageData The image data, either base64 or local url
  param width width factor / width in pixels
  param height height factor / height in pixels
  param options extra options -  
               format : file format to use (ImageResizer.FORMAT_JPG/ImageResizer.FORMAT_PNG) - defaults to JPG
               imageDataType : the data type (IMAGE_DATA_TYPE_BASE64/IMAGE_DATA_TYPE_URL) - defaults to Base64
               resizeType : type of the resize (RESIZE_TYPE_FACTOR/RESIZE_TYPE_PIXEL) - must be given
              quality : INTEGER, compression quality - defaults to 70
  returns JSON Object with the following parameters:
               imageData : Base64 of the resized image
               height : height of the resized image
               width: width of the resized image
</pre> 

### getImageSize Doc ###
Get an image width and height
<pre>
  param success success callback, will receive the data sent from the native plugin
  param fail error callback, will receive an error string describing what went wrong
  param imageData The image data, either base64 or local url
  param options extra options -  
              imageDataType : the data type (IMAGE_DATA_TYPE_BASE64/IMAGE_DATA_TYPE_URL) - defaults to Base64
  returns JSON Object with the following parameters:
               height : height of the image
               width: width of the image
</pre> 

### storeImage ###

Store an image locally
<pre>
  param success success callback, will receive the data sent from the native plugin
  param fail error callback, will receive an error string describing what went wrong
  param imageData The image data, either base64 or local url
  param options extra options -  
              format : file format to use (ImageResizer.FORMAT_JPG/ImageResizer.FORMAT_PNG) - defaults to JPG
              imageDataType : the data type (IMAGE_DATA_TYPE_BASE64/IMAGE_DATA_TYPE_URL) - defaults to Base64
              filename : filename to be stored, with ot without ending (if no ending given, format will be used) - must be given.
              directory : in which directory should the file be stored - must be given
              quality : INTEGER, compression quality - defaults to 100
  returns JSON Object with the following parameters:
              url : URL of the file just stored
</pre>  

## RELEASE NOTES ##

### 6/3/2012 ###
Initial Release, For Now Only Android Plugin was uploaded, iOS coming soon.


### The MIT License

Copyright (c) <2012> Raanan Weber, [webXells GmbH](http://www.webxells.com)

 Permission is hereby granted, free of charge, to any person obtaining a copy
 of this software and associated documentation files (the "Software"), to deal
 in the Software without restriction, including without limitation the rights
 to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 copies of the Software, and to permit persons to whom the Software is
 furnished to do so, subject to the following conditions:

 The above copyright notice and this permission notice shall be included in
 all copies or substantial portions of the Software.

 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
 THE SOFTWARE.
 
