<a href='http://wiki.github.com/hydrotik/QueueLoader'>QueueLoader has moved and is now most current on GitHub</a> I will still keep a current download of the latest rev in the download section

**Public vars and contstants**
```
// Event types
public static var ITEM_START : String = "itemStart";

public static var ITEM_PROGRESS : String = "itemProgress";

public static var ITEM_COMPLETE : String = "itemComplete";

public static var ITEM_ERROR : String = "itemError";

public static var ITEM_HTTP_STATUS : String = "itemHTTPStatus";

public static var QUEUE_START : String = "queueStart";

public static var QUEUE_PROGRESS : String = "queueProgress";

public static var QUEUE_COMPLETE : String = "queueComplete";


// Public properties
public var container : *;

public var targ : *;

public var content : *;

public var title : String = "";

public var fileType : int;

public var path : String;

public var bytesLoaded : Number = -1;

public var bytesTotal : Number = -1;	

public var percentage : Number = 0;

public var queuepercentage : Number = 0;

public var index : int;	

public var length : int;

public var bandwidth:Number;

public var width : Number;

public var height : Number;

public var message : String = "";

public var bmArray : Array;

public var info : Object = null;
```