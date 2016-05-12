UIControl

The UIControl class implements common behavior for visual elements that convey a specific action or intention in response to user interactions. Controls implement elements such as buttons and sliders, which your app might use to facilitate navigation, gather user input, or manipulate content. Controls use the target-action mechanism to report user interactions to your app.

UIControl 類別實現

You do not create instances of this class directly. The UIControl class is a subclassing point that you extend to implement custom controls. You can also subclass existing control classes to extend or modify their behaviors. For example, you might override the methods of this class to track touch events yourself or to determine when the state of the control changes.

A control’s state determines its appearance and its ability to support user interactions. Controls can be in one of several states, which are defined by the UIControlState type. You can change the state of a control programmatically based on your app’s needs. For example, you might disable a control to prevent the user from interacting with it. User interactions can also change the state of a control.

The Target-Action Mechanism
Controls use the target-action mechanism to report interesting events happening to your code. The target-action mechanism simplifies the code that you write to use controls in your app. Instead of writing code to track touch events, you write action methods to respond to control-specific events. For example, you might write an action method that responds to changes in the value of a slider. The control handles all the work of tracking incoming touch events and determining when to call your methods.

When adding an action method to a control, you specify both the action method and an object that defines that method to the addTarget:action:forControlEvents: method. (You can also configure the target and action of a control in Interface Builder.) The target object can be any object, but it is typically the view controller whose root view contains the control. If you specify nil for the target object, the control searches the responder chain for an object that defines the specified action method.

The signature of an action method takes one of three forms, which are listed in Listing 1. The sender parameter corresponds to the control that calls the action method, and the event parameter corresponds to the UIEvent object that triggered the control-related event.

Listing 1Action method definitions
OBJECTIVE-C

- (IBAction)doSomething;
- (IBAction)doSomething:(id)sender;
- (IBAction)doSomething:(id)sender forEvent:(UIEvent*)event;
Action methods are called when the user interacts with the control in specific ways. The UIControlEvents type defines the types of user interactions that a control can report and those interactions mostly correlate to specific touch events within the control. When configuring a control, you must specify which events trigger the calling of your method. For a button control, you might use the UIControlEventTouchDown or UIControlEventTouchUpInside event to trigger calls to your action method. For a slider, you might care only about changes to the slider’s value changes and so you might choose to attach your action method to UIControlEventValueChanged events.

When a control-specific event occurs, the control calls any associated action methods right away. Action methods are dispatched through the current UIApplication object, which finds an appropriate object to handle the message, following the responder chain if needed. For more information about responders and the responder chain, see Event Handling Guide for iOS.

Interface Builder Attributes
Table 1 lists the attributes associated with instances of the UIControl class.

Table 1Control attributes
Attribute
Description
Alignment
The horizontal and vertical alignment of a control’s content. For controls that contain text or images, such as buttons and text fields, use these attributes to configure the position of that content within the control’s bounds.
These alignment options apply to the content of a control and not to the control itself. For information about how to align controls with respect to other controls and views, see Auto Layout Guide.
Content
The initial state of the control. Use the checkboxes to configure whether the control is enabled, selected, or highlighted initially.
Internationalization
Because UIControl is an abstract class, you do not internationalize it specifically. However, you do internationalize the content of subclasses like UIButton. For information about internationalizing a specific control, see the reference for that control.

Accessibility
Controls are accessible by default. To be useful, an accessible user interface element must provide accurate and helpful information about its screen position, name, behavior, value, and type. This is the information VoiceOver speaks to users. Visually impaired users can rely on VoiceOver to help them use their devices.

Controls support the following accessibility attributes:

Label. A short, localized word or phrase that succinctly describes the control or view, but does not identify the element’s type. Examples are “Add” or “Play.”

Traits. A combination of one or more individual traits, each of which describes a single aspect of an element’s state, behavior, or usage. For example, an element that behaves like a keyboard key and that is currently selected can be characterized by the combination of the Keyboard Key and Selected traits.

Hint. A brief, localized phrase that describes the results of an action on an element. Examples are “Adds a title” or “Opens the shopping list.”

Frame. The frame of the element in screen coordinates, which is given by the CGRect structure that specifies an element’s screen location and size.

Value. The current value of an element, when the value is not represented by the label. For example, the label for a slider might be “Speed,” but its current value might be “50%.”

The UIControl class provides default content for the value and frame attributes. Many controls enable additional specific traits automatically as well. You can configure other accessibility attributes programmatically or using the Identity inspector in Interface Builder.

For more information about accessibility attributes, see Accessibility Programming Guide for iOS.

Subclassing Notes
Subclassing UIControl gives you access to the built-in target-action mechanism and simplified event-handling support. You can subclass existing controls and modify its behavior in one of two ways:

Override the sendAction:to:forEvent: method of an existing subclass to observe or modify the dispatching of action methods to the control’s associated targets. You might use this method to modify the dispatch behavior based on the specified object, selector, or event.

Override the beginTrackingWithTouch:withEvent:, continueTrackingWithTouch:withEvent:, endTrackingWithTouch:withEvent:, and cancelTrackingWithEvent: methods to track touch events occurring in the control. You can use the tracking information to perform additional actions. Always use these methods to track touch events instead of the methods defined by the UIResponder class.

If you subclass UIControl directly, your subclass is responsible for setting up and managing your control’s visual appearance. Use the methods for tracking events to update your control’s state and to send an action when the control’s value changes.