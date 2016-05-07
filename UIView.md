
The UIView class defines a rectangular area on the screen and the interfaces for managing the content in that area. At runtime, a view object handles the rendering of any content in its area and also handles any interactions with that content. The UIView class itself provides basic behavior for filling its rectangular area with a background color. 

UIView 類別定義在一個螢幕上的正方形區域, 是一個介面, 負責管理在這區域裡面的內容.
在執行期間, 一個 view 物件處理任何顯示在這區域上的內容是如何渲染的, 還有處理在內容上的所有互動行為. UIView 類別本身提供用背景顏色來填滿自身區域的基本行為.


More sophisticated content can be presented by subclassing UIView and implementing the necessary drawing and event-handling code yourself. The UIKit framework also includes a set of standard subclasses that range from simple buttons to complex tables and can be used as-is. For example, a UILabel object draws a text string and a UIImageView object draws an image.


很多複雜的內容可以用繼承 UIView 然後實作必要的繪圖功能和你事件處理的程式來呈現. UIKit 框架也包含了一系列標準的子類別, 從簡單的按鈕到複雜的表格都有, 他們都可以直接被使用. 例如, 一個 UILabel 物件可以畫出一個文字字串, 以及一個 UIImageView 物件可以畫出一張圖片.


Because view objects are the main way your application interacts with the user, they have a number of responsibilities. Here are just a few:

因為在你的應用程式裡, 主要是用 view 物件和使用者互動, 他們有幾個責任, 這邊舉幾個例子

Drawing and animation

繪圖和動畫

Views draw content in their rectangular area using technologies such as UIKit, Core Graphics, and OpenGL ES.

view 使用像 UIKit, Core Graphics, and OpenGL ES 的技術來把內容畫在他們正方形的區域上

Some view properties can be animated to new values.

有些 view 的屬性可以？？？
Layout and subview management
布局和 subview 管理

A view may contain zero or more subviews.

一個 view 可以包含零到多個 subview

Each view defines its own default resizing behavior in relation to its parent view.

每個 view 預設使用自己的 parent view 來定義自己的 resizing 行為

A view can define the size and position of its subviews as needed.

一個 view 可以定義大小, 如果需要的話, 也可以定義 subview 的位置.

Event handling

事件處理

A view is a responder and can handle touch events and other events defined by the UIResponder class.

一個 view 是一個響應者, 可以處理觸碰事件, 和其他被定義在 UIResponder 類別的事件.

Views can use the addGestureRecognizer: method to install gesture recognizers to handle common gestures.

View 可以使用 addGestureRecognizer: 方法來設定各種可被辨識的手勢, 來讓特定手勢發生時, view 會做回應.


Views can embed other views and create sophisticated visual hierarchies. This creates a parent-child relationship between the view being embedded (known as the subview) and the parent view doing the embedding (known as the superview). Normally, a subview’s visible area is not clipped to the bounds of its superview, but in iOS you can use the clipsToBounds property to alter that behavior. A parent view may contain any number of subviews but each subview has only one superview, which is responsible for positioning its subviews appropriately.

View 可以被其他 View 嵌入, 和建立複雜的視覺的階層. 這可以在被嵌入的頁面中, 建立一個 parent-child 關係 (subview) 和 parent view 被嵌入 (superview). 通常, subview 可以被看見的區域不是????, 但是在 iOS 裡面你可以使用 clipsToBounds 屬性來代替這個行為. 一個 parent view 可能包含很多 subview, 但是每一個 subview 都只有一個 superview, 負責把自己的 subview 放到合適的位置.

The geometry of a view is defined by its frame, bounds, and center properties. The frame defines the origin and dimensions of the view in the coordinate system of its superview and is commonly used during layout to adjust the size or position of the view. 

一個 view 的形狀是由本身的 frame, bound, center 屬性來定義. frame 定義了原點和在自己的 superview 裡的座標系統的中的 view 大小. 通常用來排版以及調整大小或者 view 的位置.

The center property can be used to adjust the position of the view without changing its size. The bounds defines the internal dimensions of the view as it sees them and is used almost exclusively in custom drawing code. The size portion of the frame and bounds rectangles are coupled together so that changing the size of either rectangle updates the size of both.

center 屬性可以在不改變本身的大小下, 調整 view 的位置. bound 定義了？？？. 一部分的 frame 大小和正方形的 bound 都結合在一起, 使得改變正方形的大小也會更新他的大小???


For detailed information about how to use the UIView class, see View Programming Guide for iOS.

對於如何使用 UIView 類別的細節, 請看 iOS 的 view
