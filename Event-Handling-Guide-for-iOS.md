#Event Handling Guide for iOS

https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541-CH1-SW1

##Introduction
###About Events in iOS

Users manipulate their iOS devices in a number of ways, such as touching the screen or shaking the device. iOS interprets when and how a user is manipulating the hardware and passes this information to your app. The more your app responds to actions in natural and intuitive ways, the more compelling the experience is for the user.


使用者用各種不同的方式操作他們的 iOS 設備, 例如像觸碰螢幕或者搖擺裝置. iOS 會把使用者操作硬體的行為當作傳遞訊息到你的應用程式. 當你的應用程式回應越多動作時, ??

###At a Glance

Events are objects sent to an app to inform it of user actions. In iOS, events can take many forms: Multi-Touch events, motion events, and events for controlling multimedia. This last type of event is known as a remote control event because it can originate from an external accessory.

每個事件都是物件, 將使用者的行為傳遞和通知應用程式. 在 iOS 裡, 事件可以是任何形式: 多點觸碰事件, 移動事件, 以及控制音量的事件. 最後一種類型的事件就是著名的遠端操作事件, 因為他是可以從外部的輔助物品來產生的.

###UIKit Makes It Easy for Your App to Detect Gestures
iOS apps recognize combinations of touches and respond to them in ways that are intuitive to users, such as zooming in on content in response to a pinching gesture and scrolling through content in response to a flicking gesture. 

iOS 的應用程式認得各種觸碰的事件, 和如何使用直覺的方式回應給使用者, 例如像使用捏的手勢來放大內容, 以及使用快速滑動的手勢來捲動內容.

In fact, some gestures are so common that they are built in to UIKit. For example, UIControl subclasses, such as UIButton and UISlider, respond to specific gestures—a tap for a button and a drag for a slider. 

事實上, 有些手勢很常用到, 所以 UIKit 本身就內建他們. 例如 UIControl 的子類別, 例如像 UIButton 和 UISlider, 使用特定的手勢 ： 輕碰 來代表點擊按鈕, 使用 拖曳 來調整進度條.

When you configure these controls, they send an action message to a target object when that touch occurs. You can also employ the target-action mechanism on views by using gesture recognizers. When you attach a gesture recognizer to a view, the entire view acts like a control—responding to whatever gesture you specify.

設定完這些 control, 當觸碰事件發生時, 他們會向 target 物件傳遞一個 action 訊息. 你可以使用 gesture recognizers 來在畫面上採用 target-action 的機制. 當你在畫面上加了一個 gesture recognizer, 整個畫面就會扮演一個像 control—responding 的東西去回應你指定的手勢.

Gesture recognizers provide a higher-level abstraction for complex event handling logic. Gesture recognizers are the preferred way to implement touch-event handling in your app because gesture recognizers are powerful, reusable, and adaptable. You can use one of the built-in gesture recognizers and customize its behavior. Or you can create your own gesture recognizer to recognize a new gesture.

Gesture recognizer 為了處理複雜的事件邏輯提供了一個更高階抽象方法. Gesture recognizer 也被推薦在實作在你的應用程式裡, 因為 Gesture recognizer 功能強大, 可重複使用, 擁有適應性. 你可以使用 Gesture recognizer 內建的行為或者採用自定義的行為. 或者你也可以建立自己的 Gesture recognizer 去認得新的手勢.



Relevant Chapter: Gesture Recognizers


###An Event Travels Along a Specific Path Looking for an Object to Handle It

When iOS recognizes an event, it passes the event to the initial object that seems most relevant for handling that event, such as the view where a touch occurred. If the initial object cannot handle the event, iOS continues to pass the event to objects with greater scope until it finds an object with enough context to handle the event. This sequence of objects is known as a responder chain, and as iOS passes events along the chain, it also transfers the responsibility of responding to the event. This design pattern makes event handling cooperative and dynamic.

當 iOS 認得一個事件, 就會傳遞這個事件給和他最有關係的初始物件, 例如在畫面上產生觸碰事件. 如果初始物件不能處理這個事件, iOS 就會繼續傳遞這個事件給更大的作用域, 直到找到一個物件有足夠的能力去處理這個事件. 這種物件的順序就是著名的 responder chain, 當 iOS 沿著這個鏈結傳遞事件, 也會轉移要處理這個物件的責任權. 這種設計模式讓事件處理變得可合作, 更彈性.

Relevant Chapter: Event Delivery: The Responder Chain


###A UIEvent Encapsulates a Touch, Shake-Motion, or Remote-Control Event
Many events are instances of the UIKit UIEvent class. A UIEvent object contains information about the event that your app uses to decide how to respond to the event. As a user action occurs—for example, as fingers touch the screen and move across its surface—iOS continually sends event objects to an app for handling. Each event object has a type—touch, “shaking” motion, or remote control—and a subtype.

很多事件都是 UIKit UIEvent 類別裡面的物件. 一個 UIEvent 物件包含一些關於事件的資訊, 例如你的應用程式使用什麼來決定如何回應這個事件. 例如, 一個使用者的行為產生像手指觸碰螢幕然後移動, 會持續的傳遞事件物件給應用程式來處理. 每個事件物件都會有觸碰的類型, 搖動的行為, 或者遠端操作.


Relevant Chapters: Multitouch Events, Motion Events, and Remote Control Events


###An App Receives Multitouch Events When Users Touch Its Views
Depending on your app, UIKit controls and gesture recognizers might be sufficient for all of your app’s touch event handling. Even if your app has custom views, you can use gesture recognizers. As a rule of thumb, you write your own custom touch-event handling when your app’s response to touch is tightly coupled with the view itself, such as drawing under a touch. In these cases, you are responsible for the low-level event handling. You implement the touch methods, and within these methods, you analyze raw touch events and respond appropriately.

UIKit 的控制元件和 gesture recognizer 已經足夠應付你應用程式裡的所有觸碰事件. 即使你的應用程式有自定義的畫面, 你也可以使用 gesture recognizer. 通常當你的應用程式回應觸碰事件是緊緊地和畫面連結在一起時, 你可以編寫你自己的觸碰手勢去處理事件. 在這些例子裡, 你要負責低階的事件處理, 你可以實在這些觸碰的方法, 在這些方法之間, 你可以分析一些觸份事件和使用正確的方式來回應.

Relevant Chapter:  Multitouch Events
An App Receives Motion Events When

###Users Move Their Devices
Motion events provide information about the device’s location, orientation, and movement. By reacting to motion events, you can add subtle, yet powerful features to your app. Accelerometer and gyroscope data allow you to detect tilting, rotating, and shaking.

移動事件提供一些關於裝置的位置, 旋轉方向, 和移動的資訊. 當移動事件被觸發時, 你可以加入敏銳又強大的特色到你的應用程式. 加速度和陀螺儀的資料讓你可以偵測 傾斜, 旋轉, 擺動等行為.

Motion events come in different forms, and you can handle them using different frameworks. When users shake the device, UIKit delivers a UIEvent object to an app. If you want your app to receive high-rate, continuous accelerometer and gyroscope data, use the Core Motion framework.

移動事件有各種不同的形式, 你可以使用各種不同的框架處理他們. 當使用者搖動裝置, UIKit 會傳遞一個 UIEvent 物件到你的應用程式. 如果你想要你的應用程式接收到 高頻率, 連續性的加速度和陀螺儀資料, 可以使用 Core Motion 框架.

Relevant Chapter: Motion Events



###An App Receives Remote Control Events When Users Manipulate Multimedia Controls
iOS controls and external accessories send remote control events to an app. These events allow users to control audio and video, such as adjusting the volume through a headset. Handle multimedia remote control events to make your app responsive to these types of commands.

iOS 控制元件和外部的附件傳遞遠端控制事件到你的應用程式, 這些事件讓使用者去控制音樂和影片, 例透過耳機調整音量. 使用多媒體遠端控制事件去讓你的應用程式回應這些命令的類型.

Relevant Chapter: Remote Control Events



###Prerequisites

This document assumes that you are familiar with:

這份文件假設你已經熟悉以下幾點

1. The basic concepts of iOS app development
2. The different aspects of creating your app’s user interface
3. How views and view controllers work, and how to customize them

---

1. 基本的 iOS 應用程式開發
2. 能夠使用不同的方式來建立你應用程式的使用者介面
3. 知道 view 和 view controller 是如何運作以及要怎麼自定義他們

If you are not familiar with those concepts, start by reading Start Developing iOS Apps (Swift). Then, be sure to read either View Programming Guide for iOS or View Controller Programming Guide for iOS, or both.

如果你還沒熟悉這些概念, 請先閱讀 Developing iOS Apps. 然後確保你也讀完 View Programming Guide for iOS 或 View Controller Programming Guide for iOS, 或者兩個都讀過

###See Also

In the same way that iOS devices provide touch and device motion data, most iOS devices have GPS and compass hardware that generates low-level data that your app might be interested in. Location and Maps Programming Guide discusses how to receive and handle location data.

iOS 裝置用一樣的方式提供觸碰和裝置移動的資料, 大部分的 iOS 設備都有 GPS 和羅盤的硬體, 可以產生你也許有興趣的低階資料. 位置和地圖編程教學討論了如何接收和處理位置資料.

For advanced gesture recognizer techniques such as curve smoothing and applying a low-pass filter, see WWDC 2012: Building Advanced Gesture Recognizers.

對於更進階的 gesture recognizer, 類似像平滑的曲線和 low-pass filter 的應用, 可以看 WWDC 2012: Building Advanced Gesture Recognizers.


Many sample code projects in the iOS Reference Library have code that uses gesture recognizers and handles events. Among these are the following projects:

Simple Gesture Recognizers is a perfect starting point for understanding gesture recognition. This app demonstrates how to recognize tap, swipe, and rotate gestures. The app responds to each gesture by displaying and animating an image at the touch location.
Handling Touches Using Responder Methods and Gesture Recognizers includes two projects that demonstrate how to handle multiple touches to drag squares around onscreen. One version uses gesture recognizers, and the other uses custom touch-event handling methods. The latter version is especially useful for understanding touch phases because it displays the current touch phase onscreen as the touches occur.
MoveMe shows how to animate a view in response to touch events. Examine this sample project to further your understanding of custom touch-event handling.

