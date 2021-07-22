
# A Proper VIPER Example found by me

View: Class that has all the code to show the app interface to the user and get their responses. Upon receiving a response View alerts the Presenter.

Interactor: Has the business logic of an app. e.g if business logic depends on making network calls then it is Interactor’s responsibility to do so.

Presenter: Nucleus of a module. It gets user response from the View and works accordingly. 
           The only class to communicate with all the other components. Calls the router for wire-framing, 
           Interactor to fetch data (network calls or local data calls), view to update the UI.
           
Entity: Contains plain model classes used by the Interactor.

Router: Does the wire-framing. Listens from the presenter about which screen to present and executes that.

# For MVVM check below links:--

https://medium.com/@dev.omartarek/mvp-vs-mvvm-in-ios-using-swift-337884d4fc6f 
https://www.youtube.com/watch?v=L634o_Rjly0
https://www.raywenderlich.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach
https://www.captechconsulting.com/blogs/ios-design-patterns-mvc-and-mvvm
https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52


# MVC ?

The Model is where your data resides. Things like persistence, model objects, parsers, managers, and networking code live there.
The View layer is the face of your app. Its classes are often reusable as they don’t contain any domain-specific logic. For example, a UILabel is a view that presents text on the screen, and it’s reusable and extensible.
The Controller mediates between the View and the model via the delegation pattern. In an ideal scenario, the controller entity won’t know the concrete view it’s dealing with. Instead, it will communicate with an abstraction via a protocol. A classic example is the way a UITableView communicates with its data source via the UITableViewDataSource protocol.

# Problems of MVC

Weak separation of concerns, the controller handle every thing here almost, it handles the business logic and the presentation logic, updating UI, applying some animations.
Hard to unit test because business logic, presentation logic and UIKit members are mixed in the controller. Testable classes shouldn’t depend on any UIKit member
Can not scale up easily
Hard to maintain, when the project get growing the controller will be chaotic


# Model View Presenter (MVP)

The View here is the same as the view in Model-View-Controller pattern, except that the View should not interact with the Model directly, the View can interact only with the presenter

The Model is also the same as the model in Model-View-Controller pattern, but the Model also can not interact directly with the View, it should interact only with the Presenter

The Presenter is the new layer introduced by Model-View-Presenter pattern, as illustrated in “Figure 4”, the Presenter is an intermediate layer that handle the communication between View and Model. it solved a lot of MVC problems like testability, maintainability, scalability.


# Presenter responsibilities
It should handle the presentation logic in general. It is responsible for what should be shown and when based on presentation conditions

Most of times the presenter handle the business logic also, but in applications that have huge business logic, you should add a business layer for your business. 
Let’s agree that architecture pattern are not a Bible, you can custom it based in your application and its business, but without violating the patterns theory’s

The presenter acts as an intermediate layer between View and Model, so it can handle the inputs received from the controller and doing some operation on them like reformatting the data, validate input or filter the data ,…etc. Also the Presenter should update Controller when the model changed in order to update the View


After this tour in MVP implementation, let’s discuss about it

It is very obvious now that, the ViewController responsibilities are reduced compared to MVC. 
The ViewController now is responsible for only UI functions like updating UI, animation, presenting views, …etc.
The Presenter now separate the presentation and business logic from the View, and this makes MVP has the ability to scale up safely, this will make your code also maintainable and testable(actually it is not fully testable using this implementation). But still there are some problems here!!!

# MVP problem

There are still a tight coupling between View and Presenter.
The Presenter is not reusable component, because it depends on a specific type, for example suppose we have register form with the same view as the update profile and the same logic, we will not able to reuse the Presenter because it depends on UpdateProfileViewController instance not RegisterViewController.
The Presenter will not be fully testable because it depend on UIKit elements and UIKit elements can not be mocked.


# What is the correct approach to implement MVP?
We can not completely decouple the view from the Presenter but we defiantly can handle it somehow to be injected in reusable and testable way.
The solution for the above three problems is to use Protocols.


# View-Model:- 

The ViewModel is at the heart of the MVVM architectural pattern and provides the connection between the business/presentation logic and the View/ViewController . 
The View (UI) responds to user input by passing input data (defined by the Model) to the ViewModel. In turn, the ViewModel evaluates the input data and responds with an appropriate UI presentation according business logic workflow.

The ViewModel responsibilities are the same as the Presenter in MVP in addition to two points:

The ViewModel should be hocked up with View via Data Binding paradigms, the most widely used is Reactive Programming, there are many frameworks which implements 
Reactive programming like RxSwift, ReactiveCocoa and Bond

The ViewModel should represent the View’s current state at any time, and this means that, the ViewModel is a model that represents the View literally(for example 
if we have login screen that has two UITextfields for username and password. Then, the ViewModel should have two String properties which represents the username 
Textfield and password TextField) and this is very easy when you implement it using any reactive framework or using any data binding method












