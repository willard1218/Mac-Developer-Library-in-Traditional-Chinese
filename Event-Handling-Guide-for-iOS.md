#Event Handling Guide for iOS
 
[原文連結](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541-CH1-SW1)

##Introduction
###About Events in iOS

Users manipulate their iOS devices in a number of ways, such as touching the screen or shaking the device. iOS interprets when and how a user is manipulating the hardware and passes this information to your app. The more your app responds to actions in natural and intuitive ways, the more compelling the experience is for the user.


使用者用各種不同的方式操作他們的 iOS 設備, 例如像觸碰螢幕或者搖擺裝置. iOS系統會把使用者操作硬體的行為當作訊息傳遞到你的應用程式. 當你的應用程式用自然且直覺的方式回應越多動作時, 使用者經驗就會越好.

###At a Glance

Events are objects sent to an app to inform it of user actions. In iOS, events can take many forms: Multi-Touch events, motion events, and events for controlling multimedia. This last type of event is known as a remote control event because it can originate from an external accessory.

每個事件都是物件, 將使用者的操作傳遞給應用程式, 通知應用程式這是使用者的動作. 在 iOS 系統裡, 事件可以是任何形式: 多點觸碰事件, 移動事件, 以及控制音量的事件. 最後一種類型的事件就是著名的遠端操作事件, 因為他是可以從外部的輔助物品來產生的.

###UIKit Makes It Easy for Your App to Detect Gestures
iOS apps recognize combinations of touches and respond to them in ways that are intuitive to users, such as zooming in on content in response to a pinching gesture and scrolling through content in response to a flicking gesture. 

iOS 的應用程式認得各種觸碰的事件, 也知道如何使用直覺的方式回應給使用者, 例如像使用捏的手勢來放大內容, 以及使用快速滑動的手勢來捲動內容.

In fact, some gestures are so common that they are built in to UIKit. For example, UIControl subclasses, such as UIButton and UISlider, respond to specific gestures—a tap for a button and a drag for a slider. 

事實上, 有些手勢很常用到, 所以 UIKit 本身就內建他們. 例如 UIControl 的子類別, 像 UIButton 和 UISlider, 使用特定的手勢 ： 輕碰 來代表點擊按鈕, 使用 拖曳 來調整進度條.

When you configure these controls, they send an action message to a target object when that touch occurs. You can also employ the target-action mechanism on views by using gesture recognizers. When you attach a gesture recognizer to a view, the entire view acts like a control—responding to whatever gesture you specify.

設定完這些 control, 當觸碰事件發生時, 他們會向 target 物件傳遞一個 action 訊息. 你可以藉由 gesture recognizer, 在畫面上建立 target-action 的機制. 當你在畫面上加了一個 gesture recognizer, 整個畫面就會扮演一個control—responding 的東西去回應你指定的手勢.

Gesture recognizers provide a higher-level abstraction for complex event handling logic. Gesture recognizers are the preferred way to implement touch-event handling in your app because gesture recognizers are powerful, reusable, and adaptable. You can use one of the built-in gesture recognizers and customize its behavior. Or you can create your own gesture recognizer to recognize a new gesture.

Gesture recognizer 為了處理複雜的事件邏輯提供了一個更高階抽象方法. Gesture recognizer 也被推薦在實作在你的應用程式裡, 因為 Gesture recognizer 功能強大, 可重複使用, 擁有適應性. 你可以使用 Gesture recognizer 內建的行為或者採用自定義的行為. 或者你也可以建立自己的 Gesture recognizer 去認得新的手勢.



Relevant Chapter: Gesture Recognizers


###An Event Travels Along a Specific Path Looking for an Object to Handle It

When iOS recognizes an event, it passes the event to the initial object that seems most relevant for handling that event, such as the view where a touch occurred. If the initial object cannot handle the event, iOS continues to pass the event to objects with greater scope until it finds an object with enough context to handle the event. This sequence of objects is known as a responder chain, and as iOS passes events along the chain, it also transfers the responsibility of responding to the event. This design pattern makes event handling cooperative and dynamic.

當 iOS 認得一個事件, 就會傳遞這個事件給和他最有關係的初始物件, 例如在畫面上產生觸碰事件. 如果初始物件不能處理這個事件, iOS 就會繼續傳遞這個事件給更大層級的物件, 直到找到一個物件有足夠的能力去處理這個事件. 這種物件的順序就是著名的 responder chain, 當 iOS 沿著這個鏈結傳遞事件, 也會轉移要處理這個物件的責任權. 這種設計模式讓事件處理變得可合作, 更彈性.

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

- The basic concepts of iOS app development
- The different aspects of creating your app’s user interface
- How views and view controllers work, and how to customize them



- 基本的 iOS 應用程式開發
- 能夠使用不同的方式來建立你應用程式的使用者介面
- 知道 view 和 view controller 是如何運作以及要怎麼自定義他們

If you are not familiar with those concepts, start by reading Start Developing iOS Apps (Swift). Then, be sure to read either View Programming Guide for iOS or View Controller Programming Guide for iOS, or both.

如果你還沒熟悉這些概念, 請先閱讀 Developing iOS Apps. 然後確保你也讀完 View Programming Guide for iOS 或 View Controller Programming Guide for iOS, 或者兩個都讀過

###See Also

In the same way that iOS devices provide touch and device motion data, most iOS devices have GPS and compass hardware that generates low-level data that your app might be interested in. Location and Maps Programming Guide discusses how to receive and handle location data.

iOS 裝置用一樣的方式提供觸碰和裝置移動的資料, 大部分的 iOS 設備都有 GPS 和羅盤的硬體, 可以產生你也許有興趣的低階資料. 位置和地圖編程教學討論了如何接收和處理位置資料.

For advanced gesture recognizer techniques such as curve smoothing and applying a low-pass filter, see WWDC 2012: Building Advanced Gesture Recognizers.

對於更進階的 gesture recognizer, 類似像平滑的曲線和 low-pass filter 的應用, 可以看 WWDC 2012: Building Advanced Gesture Recognizers.


Many sample code projects in the iOS Reference Library have code that uses gesture recognizers and handles events. Among these are the following projects:

在 iOS Reference Library 裡面有很多範例專案, 都有關於使用 gesture recognizer 和處理事件的程式碼. 包含以下專案：
 
- Simple Gesture Recognizers is a perfect starting point for understanding gesture recognition. This app demonstrates how to recognize tap, swipe, and rotate gestures. The app responds to each gesture by displaying and animating an image at the touch location.
- Handling Touches Using Responder Methods and Gesture Recognizers includes two projects that demonstrate how to handle multiple touches to drag squares around onscreen. One version uses gesture recognizers, and the other uses custom touch-event handling methods. The latter version is especially useful for understanding touch phases because it displays the current touch phase onscreen as the touches occur.
- MoveMe shows how to animate a view in response to touch events. Examine this sample project to further your understanding of custom touch-event handling.

##Gesture Recognizers

Gesture recognizers convert low-level event handling code into higher-level actions. They are objects that you attach to a view, which allows the view to respond to actions the way a control does. Gesture recognizers interpret touches to determine whether they correspond to a specific gesture, such as a swipe, pinch, or rotation. If they recognize their assigned gesture, they send an action message to a target object. The target object is typically the view’s view controller, which responds to the gesture as shown in Figure 1-1. This design pattern is both powerful and simple; you can dynamically determine what actions a view responds to, and you can add gesture recognizers to a view without having to subclass the view.

Gesture Recognizer 把低階事件處理的程式碼轉換成高階的動作. 他們可以加入到畫面裡, 這可以讓你的畫面回應控制做的方法??. 如果他們對應到特定的手勢, 例如像拖曳, 捏, 旋轉. Gesture recognizer 就會認出這些觸碰事件. 如果他們認得自己設定的姿勢, 他們會傳遞動作訊息給目標物件. 這些目標物件通常是畫面的 view controller, 就像圖 1-1. 這個設計模式強大又單純; 你可以動態的決定畫面要對哪些動作做反應, 也可以在不用繼承 view 的情況下. 把 gesture recognizer 加入到 view 裡面.


###Use Gesture Recognizers to Simplify Event Handling

The UIKit framework provides predefined gesture recognizers that detect common gestures. It’s best to use a predefined gesture recognizer when possible because their simplicity reduces the amount of code you have to write. In addition, using a standard gesture recognizer instead of writing your own ensures that your app behaves the way users expect.

UIKit 框架提供了預定義的 gesture recognizer 來偵測常用的姿勢. 最好先使用預定義的 gesture recognizer, 因為他們的簡化了你原本要寫的程式碼. 另外, 使用標準的 gesture recognizer 而不是自定義的姿勢, 可以確保你的應用程式行為正是使用者所預期的.

If you want your app to recognize a unique gesture, such as a checkmark or a swirly motion, you can create your own custom gesture recognizer. To learn how to design and implement your own gesture recognizer, see Creating a Custom Gesture Recognizer.

如果你想要你的應用程式認得特別的手勢, 例如像打勾勾或者旋渦的動作, 你可以建立你自定義的 gesture recognizer. 要學習如何設計和實作你自定義的 gesture recognizer, 可以參考 Creating a Custom Gesture Recognizer.



####Built-in Gesture Recognizers Recognize Common Gestures
When designing your app, consider what gestures you want to enable. Then, for each gesture, determine whether one of the predefined gesture recognizers listed in Table 1-1 is sufficient.

當設計應用程式時, 需要考慮要啟用哪些手勢. 然後對於每個姿勢, 決定好在表格 1-1 的預定義手勢是否足夠.

| Gesture | UIKit class |
| ------------- | ------------- |
| Tapping (any number of taps) | UITapGestureRecognizer |
| Pinching in and out (for zooming a view) | UIPinchGestureRecognizer |
| Panning or dragging | UIPanGestureRecognizer |
| Swiping (in any direction) | UISwipeGestureRecognizer |
| Rotating (fingers moving in opposite directions) | UIRotationGestureRecognizer |
| Long press (also known as “touch and hold”) | UILongPressGestureRecognizer |




Your app should respond to gestures only in ways that users expect. For example, a pinch should zoom in and out whereas a tap should select something. For guidelines about how to properly use gestures, see Apps Respond to Gestures, Not Clicks.

你的應用程式應該要依照使用者預期來回應這些手勢. 例如, 在如何正確的使用姿勢的教學裡, 當使用者捏時, 應該是執行縮放的動作, 而不是選擇某個東西, 應用程式不能解釋成為點的手勢.

Note: In iOS 7 and later, expect users to swipe up from the bottom of the screen to reveal Control Center. If iOS determines that a touch that begins at the bottom of the screen should reveal Control Center, it doesn’t deliver the gesture to the currently running app. If iOS determines that the touch should not reveal Control Center, the touch may be slightly delayed before it reaches the app.

注意: 在 iOS 7 或更新的版本, 當使用者從螢幕底部往上滑的時候, 期待出現控制中心. 如果 iOS 認為從螢幕底部往上滑會出現控制中心時, 就不會傳遞手勢給現在正在運作的應用程式, 如果 iOS 認為從螢幕底部往上滑不會出現控制中心時, 則這種觸碰會先延遲一點時間, 在傳遞給正在運行的應用程式.


####Gesture Recognizers Are Attached to a View
Every gesture recognizer is associated with one view. By contrast, a view can have multiple gesture recognizers, because a single view might respond to many different gestures. For a gesture recognizer to recognize touches that occur in a particular view, you must attach the gesture recognizer to that view. When a user touches that view, the gesture recognizer receives a message that a touch occurred before the view object does. As a result, the gesture recognizer can respond to touches on behalf of the view.

每個 Gesture recognizer 都跟一個畫面有關連. 相反的, 一個畫面可以有很多 Gesture recognizer, 因為單一個畫面也許對很多不同的手勢做出反應. 為了讓 gesture recognizer 能在特定的畫面上認得觸碰手勢, 你必須要把 gesture recognizer 加在畫面上. 當使用者觸碰畫面時, gesture recognizer 就會比畫面更早收到訊息. 因此, gesturingture recognizer 可以代替畫面來回應觸碰的事件.


####Gestures Trigger Action Messages
When a gesture recognizer recognizes its specified gesture, it sends an action message to its target. To create a gesture recognizer, you initialize it with a target and an action.

當 gesture recognizer 認得特定的手勢, 就會傳送動作訊息給目標物件. 所以要建立一個 gesture recognizer, 你需要使用 action 和 target 來做初始化.


#####Discrete and Continuous Gestures

Gestures are either discrete or continuous. A discrete gesture, such as a tap, occurs once. A continuous gesture, such as pinching, takes place over a period of time. For discrete gestures, a gesture recognizer sends its target a single action message. A gesture recognizer for continuous gestures keeps sending action messages to its target until the multitouch sequence ends, as shown in Figure 1-2.

手勢可以分成離散或連續的. 一個離散的手勢, 例如像輕碰, 只會發生一次. 一個連續的手勢, 例如捏放, 要持續一段時間. 對於離散的手勢, gesture recognizer 會傳遞給目標物件一個動作訊息. 對於連續的手勢, gesture recognizer 會持續傳遞訊息給目標物件, 直到多指觸碰的續發事件停止.

Figure 1-2  Discrete and continuous gestures

![1-2](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Art/discrete_vs_continuous_2x.png)


###Responding to Events with Gesture Recognizers

There are three things you do to add a built-in gesture recognizer to your app:



1. Create and configure a gesture recognizer instance. This step includes assigning a target, action, and sometimes assigning gesture-specific attributes (such as the numberOfTapsRequired).
2. Attach the gesture recognizer to a view.
3. Implement the action method that handles the gesture.


1. 建立和設定 gesture recognizer 物件. 包含以下步驟 : 指定 target, action, 有時候要指定特定的手勢屬性, 例如 numberOfTapsRequired.
2. 將 gesture recognizer 加到一個 view 上面.
3. 實作處理手勢觸碰時, 要執行的 action 方法.


####Using Interface Builder to Add a Gesture Recognizer to Your App
Within Interface Builder in Xcode, add a gesture recognizer to your app the same way you add any object to your user interface—drag the gesture recognizer from the object library to a view. When you do this, the gesture recognizer automatically becomes attached to that view. You can check which view your gesture recognizer is attached to, and if necessary, change the connection in the nib file.

在 Xcode 裡面的 Interface Builder, 加入一個 gesture recognizer 加到你的應用程式, 就如同你加入任何物件到你的使用者介面--從物件函式庫拖曳 gesture recognizer 到畫面上. 當你這麼做的時候, gesture recognizer 會自動的和畫面連結在一起. 你可以檢查畫面是否和你的 gesture recognizer 連結在一起, 如果需要的話, 可以更改在 nib 檔案的連結關係.

After you create the gesture recognizer object, you need to create and connect an action method. This method is called whenever the connected gesture recognizer recognizes its gesture. If you need to reference the gesture recognizer outside of this action method, you should also create and connect an outlet for the gesture recognizer. Your code should look similar to Listing 1-1.

在你建立一個 gesture recognizer 物件之後, 你需要建立和連結 action 方法, 這方法用連結 gesture recognizer, 讓他認得手勢. 如果你需要將 gesture recognizer 連結到 action 方法, 你應該要建立 outlet, 然後連結到 gesture recognizer. 你的程式碼應該長得像清單 1-1.

Listing 1-1  Adding a gesture recognizer to your app with Interface Builder

```
	@interface APLGestureRecognizerViewController ()
	@property (nonatomic, strong) IBOutlet UITapGestureRecognizer *tapRecognizer;
	@end
	 
	@implementation
	- (IBAction)displayGestureForTapRecognizer:(UITapGestureRecognizer *)recognizer
	     // Will implement method later...
	}
	@end
```


####Adding a Gesture Recognizer Programmatically
You can create a gesture recognizer programmatically by allocating and initializing an instance of a concrete UIGestureRecognizer subclass, such as UIPinchGestureRecognizer. When you initialize the gesture recognizer, specify a target object and an action selector, as in Listing 1-2. Often, the target object is the view’s view controller.

你可以藉由分配和初始化來建立一個繼承 UIGestureRecognizer 的實體物件, 例如像 UIPinchGestureRecognizer. 當你初始化  gesture recognizer, 要明確的指定 target 物件和 action 方法, 就像清單 1-2. 通常

If you create a gesture recognizer programmatically, you need to attach it to a view using the addGestureRecognizer: method. Listing 1-2 creates a single tap gesture recognizer, specifies that one tap is required for the gesture to be recognized, and then attaches the gesture recognizer object to a view. Typically, you create a gesture recognizer in your view controller’s viewDidLoad method, as shown in Listing 1-2.




