
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
