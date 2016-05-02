
##MKMapView

[原文連結](https://developer.apple.com/library/mac/documentation/MapKit/Reference/MKMapView_Class/)

An MKMapView object provides an embeddable map interface, similar to the one provided by the Maps application. You use this class as-is to display map information and to manipulate the map contents from your application. You can center the map on a given coordinate, specify the size of the area you want to display, and annotate the map with custom information.

一個 MKMapView 物件提供一個與地圖應用類似的可被嵌入的地圖介面. 你可使用這個類別來顯示地圖的資訊以及操作在你應用程式上地圖的內容. 你可以使地圖定位在一個給定一個座標, 指定你想要顯示地圖的範圍, 然後使用自訂的資訊插入到地圖上當註解.


When you initialize a map view, you should specify the initial region for that map to display. You do this by setting the region property of the map. A region is defined by a center point and a horizontal and vertical distance, referred to as the span. The span defines how much of the map at the given point should be visible and is also how you set the zoom level. Specifying a large span results in the user seeing a wide geographical area and corresponds to a low zoom level. Specifying a small span results in the user seeing a more narrow geographical area and corresponds to a higher zoom level.

當你初始化地圖視圖時, 你應該指定一塊初始的區域, 作為要顯示的地圖. 一塊區域被定義成一個中心以及垂直和水平的距離, 稱為 span. 一個 span 定義了在地圖上有多少給定的座標可見和你要如何設定縮放層級. 在使用者看到的寬闊地理區域指定一個大的 span 結果, 對應到較低的縮放比例. 在使用者看到的狹窄地理區域指定一個小的 span 結果, 對應到較高的縮放比例.



In addition to setting the span programmatically, the MKMapView class supports many standard interactions for changing the position and zoom level of the map. In particular, map views support flick and pinch gestures for scrolling around the map and zooming in and out. Support for these gestures is enabled by default but can also be disabled using the scrollEnabled and zoomEnabled properties.

除了要用程式設定 span 外, MKMapView 類別為了改變地圖的位置和縮放比例, 支援很多標準的互動方式. 特別是, 地圖視圖用輕碰和捏來支援滑動地圖以及放大縮小地圖的方式. 這些支援的手勢預設是啟用的, 但是也可以使用 scrollEnabled 和 zoomEnabled 屬性來關閉這些支援的手勢.


You can also use projected map coordinates instead of regions to specify some values. When you project the curved surface of the globe onto a flat surface, you get a two-dimensional version of a map where longitude lines appear to be parallel. To specify locations and distances, you use the MKMapPoint, MKMapSize, and MKMapRect data types.

你也可以使用 projected map coordinates, 以取代區域, 去指定一些數值. 當你將地圖的曲線表面投射到平面表面時, 你可以獲得一個二維的地圖版本, 其中經線是互相平行的. 你也可以使用 MKMapPoint, MKMapSize 和 MKMapRect 這些資料型態去指定位置和距離.

Although you should not subclass the MKMapView class itself, you can get information about the map view’s behavior by providing a delegate object. The map view calls the methods of your custom delegate to let it know about changes in the map status and to coordinate the display of custom annotations, which are described in more detail in Annotating the Map. The delegate object can be any object in your application as long as it conforms to the MKMapViewDelegate protocol. For more information about implementing the delegate object, see MKMapViewDelegate Protocol Reference.


雖然你不應該繼承 MKMapView 類別, 你可以使用一個代理物件來得到關於地圖視圖上的行為資訊. 這個地圖視圖呼叫你自己的代理裡面的方法去讓他知道地圖上狀態的改變以及客製化的註解排列座標, 其中這是....



Annotating the Map

在地圖上加入註解

The MKMapView class supports the ability to annotate the map with custom information. Because a map may have potentially large numbers of annotations, map views differentiate between the annotation objects used to manage the annotation data and the view objects for presenting that data on the map.

MKMapView 類別支援能夠在地圖上插入註解. 因為一個地圖可能有大量的註解, 地圖畫面使用註解資料和和呈現在地圖上的資料物件來區分各個註解.


An annotation object is any object that conforms to the MKAnnotation protocol. Annotation objects are typically implemented using existing classes in your application’s data model. This allows you to manipulate the annotation data directly but still make it available to the map view. Each annotation object contains information about the annotation’s location on the map along with descriptive information that can be displayed in a callout.

一個 annotation 物件可以是任何一個遵循 MKAnnotation 協定的物件. annotation 物件通常實作在你的應用程式裡面的資料模型類別. 這讓你可以直接操作 annotation 的資料, 也可以在地圖畫面裡操作. 每個 annotation 物件包含一些資訊, 其中包含了 在地圖上的座標.....



The presentation of annotation objects on the screen is handled by an annotation view, which is an instance of the MKAnnotationView class. An annotation view is responsible for presenting the annotation data in a way that makes sense. For example, the Maps application uses a pin icon to denote specific points of interest on a map. (The Map Kit framework offers the MKPinAnnotationView class for similar annotations in your own applications.) You could also create annotation views that cover larger portions of the map.

螢幕上的 annotation 物件是用 annotation view 來呈現, 這是一個 MKAnnotationView 類別. 一個 annotation view 用一個合理的方式呈現 annotation 資料. 例如, 一個地圖應用程式使用大頭針圖示來表示地圖上有興趣的點. ( MapKit 框架提供 MKPinAnnotationView 類別, 相似於你自己的應用程式裡面的 annotation ) 你也可以建立在地圖上較大覆蓋的 annotation view.??


Because annotation views are needed only when they are onscreen, the MKMapView class provides a mechanism for queueing annotation views that are not in use. Annotation views with a reuse identifier can be detached and queued internally by the map view when they move offscreen. This feature improves memory use by keeping only a small number of annotation views in memory at once and by recycling the views you do have. It also improves scrolling performance by alleviating the need to create new views while the map is scrolling.

因為 annotation view 只有當在螢幕上時我們才需要, 所以 MKMapView 類別提供一個機制, 用來查詢哪些 annotation view 還沒被使用. 當 annotation view 不在畫面上時, annotation view 有一個重複使用的識別值, 會被地圖畫面分離和內部排隊??, 這個特色是藉由只使用小數量的 annotation view 放在記憶體裡, 來改善記憶體的使用, 和重複利用你現有的 annotation view. 當地圖在捲動時, 藉由減少建立新的 view 來增強了捲動的效能.

When configuring your map interface, you should add all of your annotation objects right away. The map view uses the coordinate data in each annotation object to determine when the corresponding annotation view needs to appear onscreen. When an annotation moves onscreen, the map view asks its delegate to create a corresponding annotation view. If your application has different types of annotations, it can define different annotation view classes to represent each type.

當設定你的地圖介面, 你應該用正確的方式來加入所有的 annotation 物件. 這個地圖視圖裡的每一個 annotation view 都是用座標來對應, 讓他出現在螢幕上面. 當一個 annotation 在螢幕上移動, 地圖視圖就會向代理要求建立一個對應的 annotation view. 如果你的應用程式有很多不同類型的 annotation, 對於每個不同類型的 annotation view,  都可以被定義成不同的 annotation view 類別.