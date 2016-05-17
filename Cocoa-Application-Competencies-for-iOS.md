#Cocoa Application Competencies for iOS

[原文連結](https://developer.apple.com/library/ios/documentation/General/Conceptual/Devpedia-CocoaApp/ApplicationObject.html#//apple_ref/doc/uid/TP40009071-CH10-SW1)

##Application object

An application object is responsible for the initial routing of user events and overall management of a running application. When an application is launched, it creates the application object in its main function. Within an application’s main event loop, the application object takes an incoming event (representing a user action) and routes it to the window containing the view that is the focus of the action. It also receives action messages from controls and forwards them to the appropriate targets. It maintains a list of its windows and manages their current status.

一個應用程式物件負責使用者產生的一連串的事件的初始規劃和管理整個執行中的應用程式. 當應用程式啟動時, 會在主函式建立一個應用程式的物件. 在一個應用程式裡的主要事件裡, 這個應用程式物件要讓新的事件進來(表示使用者的動作), 然後將事件傳遞給視窗處理, 這個視窗包含了 action 觸發的視圖. 也會收到從控制元件的 action 訊息, 然後分派到適當的 target. 這維持一連串的視窗和管理他們現在的狀態.


###An Application Object Informs its Delegate of External Events
An application object also receives notifications from the operating system when external events affect the application itself—for example, when the user is shutting down the computer or, in iOS, when available memory is low. The application object   the help of its delegate in managing these external events as well as events related to the life cycle of the application. It informs the delegate of these events and, in some cases, acts upon the delegate’s response to its messages.

當外部的事件影響到應用程式本身時, 應用程式物件會接收到從作業系統來的通知, 例如當使用者關閉電腦時, 或者在  iOS 系統裡, 可用的記憶體變少時, 也會收到從作業系統來的通知. 應用程式物件的代理幫助管理這些外部的事件, 而這些外部的事件也和應用程式的生命週期緊緊相關. 應用程式會通知這些事件的代理, 在一些情況下, 會影響到代理回應他自己的訊息.

![!](https://developer.apple.com/library/ios/documentation/General/Conceptual/Devpedia-CocoaApp/Art/application_object.jpg)

###An Application Has a Single Application Object

The application object is a singleton—that is, a single instance is available to all objects in an application. In iOS, the application object is an instance of the UIApplication class (or a subclass of that class); in OS X, the application object derives from the NSApplication class. In both OS X and iOS, you can access the application object by invoking the class message sharedApplication.

應用程式物件是一個單體物件, 一個單體物件指的是, 在應用程式裡的所有物件下, 只有一個物件能被取得. 在 iOS 的系統裡, 一個應用程式物件就是一個叫 UIApplication 類別的實體物件, 而在 OS X 系統裡, 應用程式物件就變成了 NSApplication 類別的實體物件. 在 OS X 和 iOS 系統裡, 你可以藉由觸發類別訊息 sharedApplication 來存取一個應用程式物件.

Prerequisite Articles
Singleton
Delegation
Main event loop
Related Articles
Window object
View object
Control object
Target-Action
Definitive Discussion
App Programming Guide for iOS
Sample Code Projects
(None)

##Control object

A control is a type of view in a user interface that sends a message to another object when a user manipulates it in a certain way, such as tapping a button or dragging a slider. A control is the agent in the target-action model. A control (or, in OS X, the control’s cell) stores the information necessary for sending the message: a reference to the object to receive the message (the target) and a selector that identifies the method to invoke on the target (the action). When a user manipulates the control in a specific way, it sends a message to the application object, which then forwards the action message to the target.

control 是一個當使用者用特定的方法在使用者介面裡面的畫面操作時, 會傳遞訊息給另外一個物件的型別. 例如像觸碰按鈕, 或者捲動進度條. 一個 control 在 target-action 的模型裡是一個媒介. 一個 control 裡面儲存了一些要發送訊息的必要資訊 : 要接收訊息的物件參照 (target) 和選擇器, 選擇器是一個唯一識別碼, 指在 target 上哪個方法要被觸發 (action).所以當使用者使用特定的方式操作 control 時, 會發送訊息給應用程式物件, 然後應用程式物件會將 action 訊息轉發給 target.

![!](https://developer.apple.com/library/ios/documentation/General/Conceptual/Devpedia-CocoaApp/Art/target_action.jpg)

The abstract base classes for controls are UIControl, in the UIKit framework, and NSControl, in the AppKit framework. All controls are instances of concrete subclasses of these base classes. Common types of controls in these frameworks are buttons, sliders, and text fields. UIKit and AppKit also have controls that are specific to their platforms, for example, page controls (UIKit) and color wells (OS X).

在 UIKit 框架裡, Control 的抽象基底類別是叫做 UIControl, 然而在 AppKit 框架裡, 叫做 NSControl.  所有的 Control 實體物件都是繼承於這個基底類別. 在這些框架裡, Control 常用的類型有 按鈕, 滾動條, 文字輸入方塊. UIKit 和 AppKit 在他們的平台都有特定的控制元件, 例如 UIKit 裡面的 page control, OS X 裡面的 color.

###In UIKit, Control Events Determine When Action Messages are Sent
Control events are an aspect of the UIKit framework’s design for controls. In UIKit, a target and an action selector determine the form of an action message, but one or more control events—also associated with the control—determine when the message is sent. A control event is a enum constant that represents the behavior of a touch (for example, UIControlEventTouchUpInside), a phase of an editing session (for example, UIControlEventEditingDidEnd), or a change in value (UIControlEventValueChanged). You may associate multiple control events with a control, and if the action represented by any one of these constants occurs, the control sends the action message to the target.

Control 事件是 UIKit 框架為了 Control 物件所設計的. 在 UIKit 裡面, action 訊息由一個 target 和 action selector 所組成, 但是當訊息送出時, 一個或多個的 control 事件 也和 control 物件相關. 一個 control 事件是一個列舉常數型態, 表示觸碰的行為 (例如 UIControlEventTouchUpInside), 或在編輯方面 (UIControlEventEditingDidEnd), 或改變一個值(UIControlEventValueChanged). 你也許會把很多
 control 事件和一個 control 物件做關聯, 如果這些 action 表示的常數值事件有一個發生了, 則 control 物件就會傳遞 action 訊息給 target.
 
Some controls require that a certain control event be set. For example, UISwitch objects only send their action message when the UIControlEventValueChanged control event is satisfied.

有些控制元件需要設定特定的 control 事件, 例如 UISwitch 物件只有當 UIControlEventValueChanged 事件發生時, 才會送 action 訊息.

###In AppKit, Controls Can Have One or More Cells
Most controls in the AppKit framework have one or more cell objects associated with them. A cell is an instance of a class that inherits, directly or indirectly, from NSCell. Its main role is to store the target object and action selector for its control. Even though a cell is not a view, it can draw itself and respond to events, but only when instructed by its control. In the control-cell architecture, a control is the fronting view for its cell (or cells); it manages the behavior of the cell and composes and sends an action message when its distinctive user event occurs.

在 AppKit 框架裡的大多數的控制元件都有一個或多個的和單元元件有關連. 一個單元元件是一個直接或間接繼承 NSCell 的類別的實例. 他主要的角色是保存控制物件裡的 target 物件和 action 選擇器. 即使單元元件不在 view 上面, 他也可以畫出自己, 只有當 control 物件通知時, 單元元件就能回應事件. 

A few controls in the AppKit have multiple cells. For example, NSMatrix objects are controls that contain rows or matrices of cells of the same or different type. Each cell can have its own target and action selector. A few controls in AppKit store their target and action information themselves, and do not use a cell.

