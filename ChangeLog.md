<a href='http://wiki.github.com/hydrotik/QueueLoader'>QueueLoader has moved and is now most current on GitHub</a> I will still keep a current download of the latest rev in the download section

03.08.2007**-**3.0**Initial port to AS3.0 (Donovan Adams)
  ***03.16.2007**-**3.0.1**Added get method for data
  ***08.10.2007**-**3.0.2**Rewrote data output using custom event QueueLoaderEvent class.
  ***08.13.2007**-**3.0.3**Added QueueLoader progress and event.
  ***08.14.2007**-**3.0.4**Added IO Error event.
  ***09.10.2007**-**3.0.5**Fixed ITEM\_INIT duped dispatching, changed item name to title to match custom event
  ***09.14.2007**-**3.0.6**Added External mp3 and filetype cheking as well as direct access to file for easier swf access
  ***10.29.2007**-**3.0.7**Added LoaderContext for accessing loaded class references/Added stopping of loading/Loader unloading of memory for Garbage Collection
  ***10.29.2007**-**3.0.8**Added CSS/XML filetype, Optimized Loader, removeItemAt, function sorting
  ***11.15.2007**-**3.0.9**Manual MIME type, pass dataObj, index based reordering, frame drawing of external swf
  ***12.3.2007**-**3.0.10**Testing and formatting of frame drawing
  ***12.5.2007**-**3.0.11**Stable Testing, Bandwidth Detection, CacheKilling
  ***12.8.2007**-**3.0.12**Bandwidth fix with decimal rounding, Bandwidth Constuctor activiation. Event inits changed to complete to reflect internal structure
  ***12.9.2007**-**3.0.13**Event output
  ***12.9.2007**-**3.0.14**FLV Support using VideoPlayer, static debug access for compatibility.
  ***12.10.2007**-**3.0.18**SVN sync
  ***12.12.2007**-**3.0.27**FLV switched to NetStream, QueueLoader bundling (Jesse Graupmann)
  ***12.15.2007**-**3.0.29**Dispose bug fixed as a result of FLV support
  ***01.19.2008**-**3.0.27**Fixed reversed error dispatch arguments (Thanks Jesse!)
  ***08.01.2008**-**3.0.34**Fixed complete bug in IE with complete conditional checking.
  ***08.09.2008**-**3.0.36**Added individual MIME type designation and PHP loading of XML data. (soundstep.com)
  ***10.29.2008**-**3.1.0**Major changes and rewrite of class [Features and Usage](http://blog.hydrotik.com/2008/10/29/queueloader-rev-31-major-update-usage/)
  ***11.02.2008**-**3.1.1**Fixed an error thrown in Flex 4 SDK in FLVItem.as
  ***11.07.2008**-**3.1.2**Changed event.path to URLRequest type.
  ***11.30.2008**-**3.1.3**Fixed width and height prop for SWF and Image items. Added autoPlay togglePause for FLV
  ***12.28.2008**-**3.1.4**F4V added to item list. Fixed video streaming progress bug.
  ***01.25.2009**-**3.1.5**Converted even listeners to a default of strong references for consistency. mp4 shifted to FLV item.
  ***04.13.2009**-**3.1.6**Fixed ampersand bug with url vars at end of path. Support and testing with phpThumb
  ***09.29.2009**-**3.1.7**Missing first item error bug. QueueLoader constants moved. QueueLoader interface added.
  ***11.24.2009**-**3.1.8**throw Error for no items in queue. Also fixed complete event for no items in queue with ignore errors set.**

http://github.com/hydrotik/QueueLoader 11/25/2009 PROJECT HAS MOVED TO GITHUB