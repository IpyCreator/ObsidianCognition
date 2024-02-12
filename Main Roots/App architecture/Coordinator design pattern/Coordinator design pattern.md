  

  

Lets say we are loading controller from the storyboard

easy way UIKIT provides us

So what is the problem

Lets see

1. Suppose I have controller in storyboard A and it contains a sequeue with name “Canda”, now  
    ”canda” navigate to B controller  
    
2. Now in prepare for sequeue method in Controller A, I have to check for this identifier. That's a  
    red flag here. You have to add a condition, its not flexible and A need to know the “Canda”  
    
3. The view controllers are tightly coupled to make it possible to navigate from the A controller to the B. This is a red flag we should address.
4. Suppose there is a button that navigates to settings screen in A, now A is responsible for instantiating the setting controller and navigate to this screen. Again tight coupling of controllers. In other words, A view controller is put in charge of navigating the application. This is another red flag
5. Suppose there is back button on settings view controller, Now a controller should not be a responsible guy for navigation anything. That's a rule.

**Controllers should not be responsible for navigation, that it.**

  

A view controller, as its name implies, should control a view and that should be its only responsibility. Any other tasks should be delegated to other objects and that includes navigation.

A view controller shouldn't need to know about other view controllers and it shouldn't be in charge of navigating between view controllers. It tightly couples the view controllers and limits their reusability.

  

  

It's important to understand that the UIKit framework _expects_ you to tightly couple view controllers. A view controller is _expected_ to be in charge of navigation. That's what the `present(_:animated:completion:)` method was designed for. The UIKit framework was built with the Model-View-Controller pattern in mind. The MVC pattern defines models, views, and controllers. As we discussed in [Mastering MVVM With Swift](https://cocoacasts.com/series/mastering-mvvm-with-swift), the controller is put in charge of many tasks, including navigation.

  

  

**What Is the Coordinator Pattern?**

  

A coordinator coordinates the flow of the application. View controllers are no longer involved in navigation. That task is handled by the coordinator.

The coordinator pattern introduces a new type of object to the application architecture to simplify the view controllers of the project. The result is flexibility and increased reusability.

  

The coordinator pattern can help us work around these limitations. Coordinators are in some ways similar to view models. A coordinator is nothing more than an object that removes a responsibility from a view controller. It is responsible for navigation and defines the flow of the application.

  

- Implement a coordinator pattern in a new project to simplify view controllers and increase reusability.
- Use a coordinator to handle navigation between view controllers instead of tightly coupling them together.
- Define a coordinator to handle the flow of the application, delegating tasks away from view controllers.
- Introduce a coordinator object to your existing project to improve the architecture and flexibility.
- Use coordinators to handle complex navigation flows in your application.
- Create a separate coordinator for each major feature of your application to keep responsibilities clear.
- Implement a parent-child coordinator pattern to handle nested view controllers and complex flows.
- Use coordinators to manage the lifecycle of view controllers, reducing the load on view controllers themselves.
- Consider using a third-party coordinator library to simplify implementation and reduce boilerplate code.
- Use coordinators to handle network requests and data persistence, keeping those responsibilities separate from view controllers.

  

**Coordinators have 2 responsibilities**

1. Navigation
2. Flow of controllers

  

[[Xcworkspace removel]]