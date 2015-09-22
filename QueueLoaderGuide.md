<a href='http://wiki.github.com/hydrotik/QueueLoader'>QueueLoader has moved and is now most current on GitHub</a> I will still keep a current download of the latest rev in the download section

**Overall Monitoring/Basic Example**
```
// Most Basic Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

var img:Sprite = new Sprite();
img.name = "image_1";
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = .075;
addChild(img);

_oLoader.addItem("../flashassets/images/slideshow/1.jpg", img);

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**Multiple Items and Event Monitoring Example**
```
// Multiple Items and Event Monitoring Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var imageContainer:Sprite = new Sprite();
addChild(imageContainer);
imageContainer.x = imageContainer.y = 25;

var _oLoader:QueueLoader = new QueueLoader();

var startX:int = 0;
var startY:int = 0;

for (var i:int = 0; i < 3; i++) {
	var img:Sprite = new Sprite();
	img.name = "image_"+i;
	img.x = startX;
	img.y = startY;
	img.scaleX = img.scaleY = .075;
	imageContainer.addChild(img);
	_oLoader.addItem("../flashassets/images/slideshow/"+(i+1).toString()+".jpg", img, {title:"Image "+i});
	if (startX > 250) {
		startX = startX + 50;
		startY = startY + 100;
	} else {
		startX = startX + 150;
	}
}

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_START, onQueueStart, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_START, onItemStart, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_PROGRESS, onItemProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_ERROR, onItemError,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

//Listener functions
function onQueueStart(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}

function onItemStart(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
}

function onItemProgress(event:QueueLoaderEvent):void {
	trace("\t\t\t>>onItemProgress: "+event.queuepercentage);
}

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
}

function onItemError(event:QueueLoaderEvent):void {
	trace("\n>>"+event.message+"\n");
}


function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}

```


**Bitmap Smoothing and Cache Killing Example**
```
// Bitmap Smoothing and Cache Killing Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

var img:Sprite = new Sprite();
img.name = "image_1";
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = 1.25;
addChild(img);

_oLoader.addItem("../flashassets/images/slideshow/1.jpg", img, {title:"Image 1", cacheKiller:true, smoothing:true});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**Calling a SWF's Library Class References - Application Domain Example**
```
// Calling a SWF's Library Class References - Application Domain Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;


var addedDefinitions:LoaderContext = new LoaderContext();
addedDefinitions.applicationDomain = ApplicationDomain.currentDomain;

var _oLoader:QueueLoader = new QueueLoader(false, addedDefinitions, true, "testQueue");

_oLoader.addItem("../flashassets/swf/externalsounds.swf", this, {title:"SWF"});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_START, onQueueStart, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

//Listener functions
function onQueueStart(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	var loop:Sound = new (getDefinitionByName("Loop1"))();
	var soundChannel:SoundChannel = loop.play(0,999);
}
```


**Queue Disposing**
```
// Queue Disposing

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

var img:Sprite = new Sprite();
img.name = "image_1";
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = .1;
addChild(img);

_oLoader.addItem("../flashassets/images/slideshow/1.jpg", img, {title:"Image 1"});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	setTimeout(callDipose, 3000);
}

function callDipose():void{
	_oLoader.dispose();
}
```


**Manually Setting File Type/URL Variable Example**
This will let you pass URL variables to a file that is to be loaded. Keep in mind that the example data.php file has no php code in it so that it will run locally. However on a php server you would have the code shown below in the data.php file. This will pass the url variable $user a value of yourname, which you should see as yourname.jpg in the XML output.

**PHP:**
```
<?php echo '<?xml version="1.0" encoding="iso-8859-1"?>
<test
	css="test.css"
	>
	<!--
	Fonts:
		
	-->
	
	<config>
		<audio src="flashassets/swf/externalsounds.swf" />
	</config>
	
	
	<images>
		<img src="flashassets/images/slideshow/' . $user . '.jpg" />
		<img src="flashassets/images/slideshow/2.jpg" />
		<img src="flashassets/images/slideshow/3.jpg" />
	</images>
	
</test>'; ?>
```


**Actionscript:**
```
// Manually Setting File Type/URL Variable Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

var img:Sprite = new Sprite();
img.name = "image_1";
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = .1;
addChild(img);

_oLoader.addItem("../includes/admin/data.php?id=1&user=yourname", null,
		{title:"XML PHP", mimeType:QueueLoader.FILE_XML}
);

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "XML PHP") {
		var output:String = XML(event.targ).child("images").child("img")[0].@src;
		trace("\n\t\tXML Node: "+output+"\n\n");
	}
}

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**Drawing a SWF's Frames to BitmapData Array Example**
```
// Drawing a SWF's Frames to BitmapData Array Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/swf/externalimages.swf", null, {title:"SWF Images", drawFrames:true});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "SWF Images") {
		var startX:int = 0; var startY:int = 65;

		for (var i:int = 0; i<event.bmArray.length; i++) {
			var bm:Bitmap = new Bitmap(event.bmArray[i], "auto", true);
			bm.x = startX;
			bm.y = startY;
			bm.scaleX = bm.scaleY = .75;
			addChild(bm);
			startX = startX + 85;
		}
	}
}

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**Ignoring of Errors/Error Handling Example**
```
// Ignoring of Errors/Error Handling Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader(true); //<- true arg sets ignore errors

var img:Sprite = new Sprite();
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = .075;
addChild(img);

var img2:Sprite = new Sprite();
img2.x = 120;
img2.y = 20;
img2.scaleX = img2.scaleY = .075;
addChild(img2);

var img3:Sprite = new Sprite();
img3.x = 220;
img3.y = 20;
img3.scaleX = img3.scaleY = .075;
addChild(img3);

_oLoader.addItem("../flashassets/images/slideshow/1.jpg", img);
_oLoader.addItem("../flashassets/images/slideshow/12.jpg", img2);
_oLoader.addItem("../flashassets/images/slideshow/3.jpg", img3);

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_ERROR, onItemError,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemError(event:QueueLoaderEvent):void {
	trace("\n>>"+event.message+"\n");
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**Stop and Resume Example**
```
// Stop and Resume Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader(true); //<- true arg sets ignore errors

var img:Sprite = new Sprite();
img.x = 20;
img.y = 20;
img.scaleX = img.scaleY = .075;
addChild(img);

var img2:Sprite = new Sprite();
img2.x = 170;
img2.y = 20;
img2.scaleX = img2.scaleY = .075;
addChild(img2);

_oLoader.addItem("../flashassets/images/slideshow/1.jpg", img, {title:"Image 1"});
_oLoader.addItem("../flashassets/images/slideshow/2.jpg", img2, {title:"Image 2"});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "Image 1") {
		_oLoader.stop();
		// Set a 4 second to pause and resume the load
		setTimeout(resumeLoad, 4000);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}

function resumeLoad():void{
	_oLoader.resume();
}
```


**Bandwidth Detection Example**
```
// Bandwidth Detection Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var imageContainer:Sprite = new Sprite();
addChild(imageContainer);
imageContainer.x = imageContainer.y = 25;

var addedDefinitions:LoaderContext = new LoaderContext();
addedDefinitions.applicationDomain = ApplicationDomain.currentDomain;
var _oLoader:QueueLoader = new QueueLoader(false, addedDefinitions, true);

var startX:int = 0;
var startY:int = 0;

for (var i:int = 0; i < 3; i++) {
	var img:Sprite = new Sprite();
	img.name = "image_"+i;
	img.x = startX;
	img.y = startY;
	img.scaleX = img.scaleY = .075;
	imageContainer.addChild(img);
	_oLoader.addItem("../flashassets/images/slideshow/"+(i+1).toString()+".jpg", img, {title:"Image "+i});
	if (startX > 250) {
		startX = startX + 50;
		startY = startY + 100;
	} else {
		startX = startX + 150;
	}
}

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);
_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.bandwidth+"KB/s");
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```


**CSS Example**

```
// CSS Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../includes/admin/test.css", null, {title:"CSS"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_CSS) {
		trace("\t\tCSS: "+event.content.styleNames);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```



**XML Loading/Get Item By Title Example**
```
// XML Loading/Get Item By Title Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../includes/admin/test.xml", null, {title:"XML"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_XML) {
		trace("\t\tXML: "+event.content);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace("\n\nXML Node:\n"+XMLList(_oLoader.getItemByTitle("XML").content).queueloader.item[0]);
}

```


**Sorting Example**
```
// Sorting Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/mp3/GetDown.mp3", null, {title:"MP3"});
_oLoader.addItem("../flashassets/swf/externalsounds.swf", this, {title:"SWF"});
_oLoader.addItem("../includes/admin/test.xml", null, {title:"XML"});
_oLoader.addItem("../includes/admin/data.php?id=1&user=yourname", null,
     {title:"XML PHP", mimeType:QueueLoader.FILE_XML}
);
_oLoader.addItem("../flashassets/swf/externalimages.swf", null, {title:"SWF Images", drawFrames:true});
_oLoader.addItem("../includes/admin/test.css", null, {title:"CSS"});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_START, onQueueStart, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueStart(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader.getQueuedItems());
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "MP3") {
                // This takes an array of two items (second arg)
                // from 4th position (1st arg) and inserts them
                // into the 2nd position (3rd arg)
		_oLoader.shuffle(4, 2, 2);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader.getLoadedItems());
}
```



**Adding Items On-The-Fly Example**
```
// Adding Items On-The-Fly Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/mp3/GetDown.mp3", null, {title:"MP3"});
_oLoader.addItem("../flashassets/swf/externalsounds.swf", this, {title:"SWF"});


_oLoader.addEventListener(QueueLoaderEvent.QUEUE_START, onQueueStart, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueStart(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader.getQueuedItems());
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "SWF") {
		_oLoader.addItem("../includes/admin/test.xml", null, {title:"XML"});
		_oLoader.addItem("../flashassets/swf/externalimages.swf", null, {title:"SWF Images"});
		_oLoader.addItem("../includes/admin/test.css", null, {title:"CSS"});
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader.getLoadedItems());
}
```



**QLManager Example**
```
// QLManager Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;
import com.hydrotik.queueloader.QLManager;

var _oLoader:QueueLoader = new QueueLoader(false, null, true, "loader1");

_oLoader.addItem("../flashassets/mp3/GetDown.mp3", null, {title:"MP3"});
_oLoader.addItem("../flashassets/swf/externalsounds.swf", this, {title:"SWF"});

_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();



var _oLoader2:QueueLoader = new QueueLoader(false, null, true, "loader2");

_oLoader2.addItem("../includes/admin/test.xml", null, {title:"XML"});
_oLoader2.addItem("../flashassets/swf/externalimages.swf", null, {title:"SWF Images"});
_oLoader2.addItem("../includes/admin/test.css", null, {title:"CSS"});

_oLoader2.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueue2Complete,false, 0, true);

_oLoader2.execute();

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader.getLoadedItems());
}

function onQueue2Complete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
	trace(_oLoader2.getLoadedItems());
	setTimeout(callDipose, 3000);
}

function callDipose():void{
	trace("QLManager Accessing Items:");
	trace("\t"+QLManager.getQueue("loader1").getItemAt(0).title);
	trace("\t"+QLManager.getQueue("loader2").getItemAt(0).title);
	QLManager.disposeAll();
	trace("QLManager Disposing:");
	trace("\t"+QLManager.getQueue("loader1"));
	trace("\t"+QLManager.getQueue("loader2"));
}
```



**Zip Loading Example**
Make sure you have the nochump package in your source folder.
```
// Zip Loading Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/zip/assets.zip", null);

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_ZIP) {
		trace("\t\tZIP Array: "+event.content);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}

```



**PCM Wav Loading Example**
Make sure the Popforge library is included in your source along with the modified SoundFactory class that bypasses the swf.bin file. This modified class writes the bytes to a ByteArray instead.
```
//PCM Wav Loading Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var soundChannel:SoundChannel = new SoundChannel();

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/pcm/loop1.wav", null, {title:"Loop1"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_WAV) {
		soundChannel = event.content.play(0,999);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```



**MP3 Loading Example**!
```
//MP3 Loading Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var soundChannel:SoundChannel = new SoundChannel();

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/mp3/GetDown.mp3", null, {title:"MP3"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_MP3) {
		soundChannel = event.content.play(0);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```



**Direct QL Formatted XML Loading Example**
This snippet of XML can reside anywhere in your XML document. It allows for automatic passing of QueueLoader data. The prefix attribute simply adds the prefix when the movie is in external/standalone mode when publishing locally. If your paths jump directories or require absolute paths, then you can leave it as prefix="".

XML:
```
<queueloader prefix="../">
		<item container="this" src="flashassets/swf/externalimages.swf">
			<info>
				<title><![CDATA[SWF Images]]></title>
				<cacheKiller><![CDATA[true]]></cacheKiller>
				<drawFrames><![CDATA[true]]></drawFrames>
			</info>
		</item>
		<item container="imageContainer" src="flashassets/images/slideshow/1.jpg">
			<info>
				<title><![CDATA[Image 1]]></title>
				<cacheKiller><![CDATA[true]]></cacheKiller>
			</info>
		</item>
		<item container="null" src="flashassets/images/slideshow/2.jpg">
			<info>
				<title><![CDATA[Image 2]]></title>
				<cacheKiller><![CDATA[true]]></cacheKiller>
			</info>
		</item>
		<item container="null" src="flashassets/images/slideshow/3.jpg">
			<info>
				<title><![CDATA[Image 3]]></title>
				<cacheKiller><![CDATA[true]]></cacheKiller>
			</info>
		</item>
	</queueloader>
```



The loadXML() method also accepts a scope variable which relates to the container attribute. I.E. scope[container](container.md). If it's null, then the container has no parent reference and is the same as adding null to an addItem() method.

Actionscript:
```
//Direct QL Formatted XML Loading Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../includes/admin/test.xml", null, {title:"XML"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "XML") {
		_oLoader.loadXML(event.content);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```



**SWF Timeline Example**
```
//SWF Timeline Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../flashassets/swf/timeline.swf", this);

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	queueprog.width = 150 * event.queuepercentage;
	queue_txt.text = "QUEUE: "+Math.round((event.queuepercentage*100)).toString() + "% COMPLETE";
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.fileType == QueueLoader.FILE_SWF) {
		event.content.fireFunction();
		event.content.gotoAndPlay(2);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```



**Generic Data Loading Example**
```
//Generic Data Loading Example

import com.hydrotik.queueloader.QueueLoader;
import com.hydrotik.queueloader.QueueLoaderEvent;

var _oLoader:QueueLoader = new QueueLoader();

_oLoader.addItem("../queueloader.html", null, {title:"HTML"});

_oLoader.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, onItemComplete,false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, onQueueProgress, false, 0, true);
_oLoader.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, onQueueComplete,false, 0, true);

_oLoader.execute();

function onQueueProgress(event:QueueLoaderEvent):void {
	trace("\t>>onQueueProgress: "+event.queuepercentage);
}

function onItemComplete(event:QueueLoaderEvent):void {
	trace("\t>> "+event.type, "item title: "+event.title);
	if (event.title == "HTML") {
		trace(event.content);
	}
}

function onQueueComplete(event:QueueLoaderEvent):void {
	trace("** "+event.type);
}
```