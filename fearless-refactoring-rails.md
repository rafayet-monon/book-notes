# Fearless Refactoring
### Rails Controllers
#### Andrzej Krzywda




## Chapter 1: Rails controllers

### What is the problem with Rails controllers?

- At the beginning they all start simple, as the one scaffolded with a generator
  ```ruby
  def create
    @issue = Issue.new(issue_params)
  
    respond_to do |format|
    if @issue.save
      format.html { redirect_to @issue, notice: "Success." }
      format.json { render action: 'show', status: :created, location: @issue }
    else
      format.html { render action: 'new' }
      format.json { render json: @issue.errors, status: :unprocessable_entity } end
    end
  end
  ```
- For some resources the controllers and actions stay simple. In some of them, though, they start to grow.
  
  Typical “patterns” include:

    - before_filter groups 
    - multiple, nested if-branches
    - setting @ivars to access them in the view • Controller inheritance
    - Controller mixins/concers 

### The gateway drug - service objects

- The most popular way of having better controllers is through introducing the layer of service objects.
- Service objects are the perfect small step. After that you’ll see further improvements.

### The Boy Scout rule

- Refactoring is an ongoing activity. Refactoring is a team activity. Refactoring is best when everyone understands the
  reasons and agrees on the direction of the code changes.
- **Always leave the campground cleaner than you found it.**

### Why service objects?

- Services are not the silver bullet. They don’t solve all the problems. They are good as the first step into the
  process of improving the design of your application.
- Services helps to achieve the following goals

  - isolate from the Rails HTTP-related parts
  - faster build time
  - easier testing
  - easier reuse for API
  - less coupling
  - thinner controllers
    
### Why not service objects?

- If your app is fairly small (mostly CRUD), you don’t see the problem of frequent bugs, your tests are fast enough and
  introducing new changes is very fast, then you probably don’t gain much from introducing the service layer. You’ll be fine with just having the code in the controller actions.
- **Don't fire a canon to kill mosquito**

#### What is a Rails service object?

- _According to Martin Fowler’s P of EEA Catalog:_ Defines an application’s boundary with a layer of services that 
  establishes a set of available operations and coordinates the application’s response in each operation.
- _According to Bryan Helmkamp_: Some actions in a system warrant a Service Object to encapsulate their operation. I
  reach for Service Objects when an action meets one or more of these criteria:

    - The action is complex (e.g. closing the books at the end of an accounting period)
    - The action reaches across multiple models (e.g. an e-commerce purchase using
      Order, CreditCard and Customer objects)
    - The action interacts with an external service (e.g. posting to social networks)
    - The action is not a core concern of the underlying model (e.g. sweeping up
      outdated data after a certain time period).
    - There are multiple ways of performing the action (e.g. authenticating with an
      access token or password). This is the Gang of Four Strategy pattern.
      
- _According to Eric Evans:_ A standalone operation within the context of your domain. A Service Object collects one or
  more services into an object. Typically you will have only one instance of each service object type within your execution context.

### What it’s not

- The concept of SOA (Service Oriented Architecture) is conceptually similar, in the way of having a set of services.
  However, in practice, SOA includes the protocol layer (http, soap), which is less relevant to the idea of service objects.

### Refactoring

- Martin Fowler: Refactoring is a controlled technique for improving the design of an existing code base. Its essence
  is applying a series of small behavior-preserving transformations, each of which “too small to be worth doing”.
- Joshua Kerievsky: By continuously improving the design of code, we make it easier and easier to work with. This is in
  sharp contrast to what typically happens: little refactoring and a great deal of attention paid to expediently adding
  new features. If you get into the hygienic habit of refactoring continuously, you’ll find that it is easier to extend and maintain code.
- Michael Feathers: One of the clearest preconditions for refactoring is the existence of tests. Martin Fowler is pretty
  explicit about that in his Refactoring book, and everything I’ve experienced with teams backs it up. Want to do make
  things better? Sure, but if you don’t have tests to support you, you’re gambling. Can you do a little refactoring to
  get tests in place? Yes, I advise it, but when you start to do significant refactoring, you’d better have tests to
  back you up. If you don’t, it’s only a matter of time before your teammates take away your keyboard.

### Refactoring and the human factor

- Not all team members are equally pro-refactoring.
- People have different perceptions of which code is actually good.

### Do we really need to change the existing code?

- Is it because you spend a tremendous time on bug fixing?
- Is it because adding new features takes more and more time? 
- Maybe it’s because the app is slow and refactoring can help you extract some parts and later optimize them?
- Whatever is the reason, make sure everyone understands it.
- Once you all see facts, metrics and numbers, it’s easier to agree on the same solution.

### Refactoring takes a lot of time

- Become so good at refactoring that it almost happens at no-time. Split the bigger changes into multiple smaller ones.
  If you keep delivering value, while cleaning up the codebase then you don’t need to justify the time spent.

### I wouldn’t refactor this part

- Time is our currency, make sure we spend it in the best way.

## Chapter 2: Refactoring recipes

### Inline controller filters

-  Bring together the code that belongs together so that you can move it as a whole somewhere else. It’s one of those
   ‘eliminate Rails magic’ techniques, that help reasoning about the code in one place.

### Explicitly render views with locals

- Algorithm:
  - Go to the view, replace all `@ivar` with `var`
  - Do the same in all partials that are called from the view and always pass the params to partials explicitly with 
      
    `render “products/form”, {product: product}`
      
  - At the end of the action add an explicit render call with a full path and the locals:
      
    `render “products/new”, :locals => {product: product}`
    
  - Find all controllers that were using the views/partials that you changed and apply the same.

### Extract render/redirect methods

- Algorithm:
  - Identify all render and redirect calls in your controllers’ actions.
  - Extract a private method for each render and redirect call you found with descriptive name that shows your intention.
  - Find and remove any duplicated methods you might created during this refactoring in the same controller.

### Extract a Single Action Controller class

- A typical Rails controller doesn’t follow the Single Responsibility Principle. Each action is usually a separate
  responsibility. In the early phases of a Rails app, it may make sense to keep them together, as they operate on one resource.

- Algorithm:
  
  - A new route declaration above the previous (first wins)
  - Create an empty controller `CreateProductController` which inherits from the previous
  - Copy the action content to the new controller
  - Remove the action from the previous controller
  - Copy the filters/methods that are used by the action to the new controller 

### Extract routing constraint

- Algorithm:
  - Go to the controller, duplicate existing action method under different name.
  - Create a constraint that can recognize which action should be called. Put it in routes.rb
  - Duplicate the relevant routing rule in routes.rb
  - Protect first routing rule with the constraint.
  - Change the second routing rule so it delegates to the new controller action. If necessary, protect it with similar constraint
  - Remove the irrelevant code from controller actions. Make them do only one thing.
  - (Optionally) Move the constraint(s) to separate file(s).
    
### Extract an adapter object

- Algorithm:
  - Extract external library code to private methods of your controller
  - Parametrize thes emethods - remove explicit `request/params/session` statements
  - Pack return values from external lib calls into simple data structures.
  - Create an adapter class inside the same file as the controller
  - Move newly created controller methods to adapter (one by one), replace these method calls with calls to adapter object
  - Pack exceptions raised by an external library to your exceptions
  - Move your adapter to another file (ex. app/adapters/your_adapter.rb)
  
### Extract a repository object

- Algorithm:
  
  - Create a class called ProductsRepository inside the same file as the controller
  - Find all calls to typical Product.find/all/new/save/create methods in the controller
  - Create those methods in the repo object
  - Add a private method, called repo in the controller (possibly in the ApplicationController) where you 
    instantiate the repo.
  - Move the repository class to `app/repos/`  

### Extract a service object using the SimpleDelegator

- Algorithm:
  
  - Move the action definition into new class and inherit from SimpleDelegator.
  - Step by step bring back controller responsibilities into the controller.
  - Remove inheriting from SimpleDelegator.
  - (Optional) Use exceptions for control flow in unhappy paths.
  
### Extract conditional validation into Service Object

- Algorithm:
  
  - Make an object from the validation.
  - Assign the validation object to constant.
  - Split `save!` into validation and saving separately.
  - Use the validation in service object.
    
    - Call the validation after calling valid?.
    - Remove the validation from model.
    - Remove the accessor from model.
  
### Extract a form object

- Algorithm:
  
  - Create new class, e.g.under `app/forms` directory
  - Include ActiveModel::Model to have a possibility to use validations and other Rails conven-
    tions related to view rendering and form submission (routing)
  - Define required attributes on your form object
  - Copy validations relevant in this particular context from your model
  - Use the form object in controller and view
  - Remove validations from your model which are covered by a form object
  

