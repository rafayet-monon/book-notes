# Clean Code
### A handbook of agile software craftsmanship
#### Robert C. Martin




## Chapter 1: Clean Code

### There will be code

- We will never be rid of code
- Code is really the language in which we ultimately express the requirements

### Bad code

- Bad code can bring a company down
- LeBlanc’s law: **Later equals never**

### The Total Cost of Owning a Mess

- Over time if a codebase is messy, it becomes so big and so deep and so tall, they can not clean it up.
- As mess builds in a code, the productivity of the team continues to decrease, asymptotically approaching zero

#### The Grand Redesign in the Sky

- Keeping a codebase clean is not just cost effective, it’s a matter of professional survival

#### Attitude

- The managers and marketers look to us for the information they need to make promises and commitments
- The users look to us to validate the way the requirements will fit into the system
- The project managers look to us to help work out the schedule
- it is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes

#### The Primal Conundrum

- Deadline cannot be met by making a mess in the code
- Mess will slow us down more and make us miss the deadline

#### The Art of Clean Code?

- Writing clean code is a lot like painting a picture
- Writing clean code requires the disciplined use of a myriad little techniques applied through a painstakingly 
  acquired sense of `cleanliness`.
- A programmer with `code-sense` will look at a messy module and see options and variations.
- A programmer who writes clean code is an artist who can take a blank screen through a series of transformations until
  it is an elegantly coded system.

### What Is Clean Code?

#### Bjarne Stroustrup, inventor of C++ and author of The C++ Programming Language

- Code should be elegant and efficient
- Bad code tempts the mess to grow
- Clean code exhibits close attention to detail
- Clean code does one thing well

#### Grady Booch, author of Object Oriented Analysis and Design with Applications

- Clean code reads like well-written prose
- It should contain only what is necessary

#### “Big” Dave Thomas, founder of OTI, godfather of the Eclipse strategy

- Clean code makes it easy for other people to enhance it
- Code without tests, is not clean
- The code should be composed in such a form as to make it readable by humans

#### Michael Feathers, author of Working Effectively with Legacy Code

- Clean code always looks like it was written by someone who cares

#### Ron Jeffries, author of Extreme Programming Installed and Extreme Programming Adventures in C#

- Contains no duplication
- An object should not do more than one thing
- One method that says more clearly what it does, and some submethods saying how it is done

#### Ward Cunningham, inventor of Wiki, inventor of Fit, coinventor of eXtreme Programming. Motive force behind Design Patterns. Smalltalk and OO thought leader. The godfather of all those who care about code.

- When you read clean code you won’t be surprised at all
- Beautiful code makes the language look like it was made for the problem
- It is not the language that makes programs appear simple. It is the programmer that make the language appear simple

### We are authors

- The ratio of time spent reading vs. writing is well over 10:1.
  We are constantly reading old code as part of the effort to write new code
- The code I'm trying to write today will be hard or easy to write depending on how hard or easy the surrounding 
  code is to read

### The Boy Scout Rule

- Leave the campground cleaner than it is found


## Chapter 2: Meaningful Names

### Introduction

- Names are everywhere in a software
- We should do this well

### Use Intention-Revealing Names

- Good variable name should tell why it exists, what it does, and how it is used
- With simple names, it’s not difficult to understand what’s going on. This is the power of choosing good names

### Avoid Disinformation

- Do not refer to a grouping of accounts as an accountList unless it’s actually a List. The word list means something
  specific to programmers. If the container holding the accounts is not actually a List, it may lead to false conclusions.1 So accountGroup or bunchOfAccounts or just plain accounts would be better.
- Spelling similar concepts similarly is information. Using inconsistent spellings is dis- information.
- A truly awful example of disinformative names would be the use of lower-case L or uppercase O as variable names,
  especially in combination. The problem, of course, is that they look almost entirely like the constants one and zero, respectively.

### Use Pronounceable Names

- Names must be pronounceable easily so that new developers doesn't need help understanding new variable or class names.

### Use Searchable Names

- Single-letter names can ONLY be used as local vari- ables inside short methods. The length of a name should 
  correspond to the size of its scope.
- Write in a way so that names are easily searchable

### Avoid Mental Mapping

- One difference between a smart programmer and a professional programmer is that the professional understands that
 clarity is king
- Readers shouldn’t have to mentally translate my names into other names they already know.

### Class Names

- Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`, and `AddressParser`.
  Avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name of a class. A class name should not be a verb.

### Method Names

- Methods should have verb or verb phrase names like `postPayment`, `deletePage`, or `save`. `Accessors`, `mutators`, and
  predicates should be named for their value and prefixed with `get` or `set`.
  
### Don’t Be Cute

- Never use names like `HolyHandGrenade`? Sure, it’s cute, but maybe in this case DeleteItems might be a better name.
- **Say what you mean. Mean what you say.**

### Pick One Word per Concept

- A consistent lexicon is a great boon to the programmers who must use my code.
- For example, it’s confusing to have a controller and a manager and a driver in the same code base. What is the
  essential difference between a DeviceManager and a Protocol- Controller? Why are both not controllers or both not managers?

### Don’t Pun

- For example, we have many classes where `add` will create a new value by adding or concatenating two existing values. 
  Now let’s say we are writing a new class that has a method that puts its single parameter into a collection. Should we
  call this method `add`? It might seem consistent because we have so many other add methods, but in this case, the 
  semantics are different, so we should use a name like `insert` or `append` instead. To call the new method add would 
  be a pun.

### Use Solution Domain Names

- The people who will read code will be programmers. So go ahead and use computer science (CS) terms, algorithm names, 
  pattern names, math terms, and so forth. It is not wise to draw every name from the problem domain because we don’t 
  want our coworkers to have to run back and forth to the customer asking what every name means when they already know 
  the concept by a different name.

### Use Problem Domain Names

- The code that has more to do with problem domain concepts should have names drawn from the problem domain.

### Don’t Add Gratuitous Context

- Shorter names are generally better than longer ones, so long as they are clear. Add no
  more context to a name than is necessary.
  
## Chapter 3: Functions

### Small!

- Functions should be small, no more that three or four lines

### Do One Thing

- Functions should do only one thing.

### Reading Code from Top to Bottom: The Stepdown Rule

- We want to be able to read the program as though it were a set of TO paragraphs, each of which is describing the 
  current level of abstraction and referencing subsequent TO paragraphs at the next level down.

### Use Descriptive Names

- I know I am writing clean code when each routine turns out to be pretty much what is expected.
- Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name.
- It is not at all uncommon that hunting for a good name results in a favorable restructuring of the code.

### Function Arguments

- The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by 
  two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very 
  special justification—and then shouldn’t be used anyway.
- Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It immediately 
  complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one 
  thing if the flag is true and another if the flag is false!
- Functions that take three arguments are significantly harder to understand than dyads. The issues of ordering, 
  pausing, and ignoring are more than doubled. It is suggested to think very carefully before creating a triad.
- When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be
wrapped into a class of their own. Consider, for example, the difference between the two following declarations:
  ```
  Circle makeCircle(double x, double y, double radius);
  Circle makeCircle(Point center, double radius);
  ```
- The function and argument should form a very nice verb/noun pair. For example, `write(name)` is very evocative. Whatever
  this “name” thing is, it is being “written.” An even better name might be `writeField(name)`, which tells us that the 
  “name” thing is a “field.”

### Have No Side Effects

- Side effects are lies. Function promises to do one thing, but it also does other hidden things.

### Command Query Separation

- Functions should either do something or answer something, but not both. Either my function should change the 
  state of an object, or it should return some information about that object.

### Prefer Exceptions to Returning Error Codes

- Returning error codes from command functions is a subtle violation of command query separation. It promotes commands 
  being used as expressions in the predicates of if statements.
- If exceptions are used instead of returned error codes, then the error processing code can be separated from the happy
  path code and can be simplified.
- Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with 
  normal processing. So it is better to extract the bodies of the try and catch blocks out into functions of their own.

### Don’t Repeat Yourself

- Duplication may be the root of all evil in software.
- There should never be duplicate lines of code

### Structured Programming

- There should only be one return statement in a func- tion, no break or continue statements in a loop, and never, ever,
  any goto statements.

## Chapter 4: Comments

Nothing can be quite so helpful as a well-placed comment. Nothing can clutter up a mod- ule more than frivolous dogmatic
comments.Comments are not like Schindler’s List. They are not “pure good.” Indeed, comments are, at best, a necessary 
evil.

### Comments Do Not Make Up for Bad Code

- Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments.

### Explain Yourself in Code

- It takes only a few seconds of thought to explain most of my intent in code. In many cases it’s simply a matter of 
  creating a function that says the same thing as the comment I want to write.

### Good Comments

- Sometimes our corporate coding standards force us to write certain comments for legal reasons. For example, copyright
  and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.
- It is sometimes useful to provide basic information with a comment. For example, con- sider this comment that explains the return value of an abstract method:
  ```
  // Returns an instance of the Responder being tested.
  protected abstract Responder responderInstance();
  ```
- Sometimes it is useful to warn other pro- grammers about certain consequences. For example, here is a comment that 
  explains why a particular test case is turned off
- It is sometimes reasonable to leave “To do” notes in the form of //TODO comments. In the following case, the TODO 
comment explains why the function has a degenerate implementation and what that function’s future should be.
- A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

### Bad Comments

- Plopping in a comment just because you feel you should or because the process requires it, is a hack. If you decide to
  write a comment, then spend the time necessary to make sure it is the best comment you can write.
- Avoid redundant comments which doesn't serve a purpose
- Sometimes, with all the best intentions, a programmer makes a statement in his comments that isn’t precise enough 
  to be accurate. 
- Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.
- Few practices are as odious as commenting-out code. Never do this!
- Don’t put interesting historical discussions or irrelevant descriptions of details into comments.

## Chapter 5: Formatting

### Vertical Formatting

- Small files are usually easier to understand than large files are.
- There should be blank lines between methods for vertical openness
- Concepts that are closely related should be kept vertically close to each other
- Dependent Functions. If one function calls another, they should be vertically close, and the caller should be 
  above the callee.
- As in newspaper articles, we expect the most important concepts to come first, and we expect them to be expressed with
  the least amount of polluting detail. We expect the low-level details to come last. This allows us to skim source 
  files, getting the gist from the first few functions, without having to immerse ourselves in the details.

### Horizontal Formatting

- Lines should not be more than 120 characters long
- Use horizontal white space to associate things that are strongly related and disassociate things that are more 
  weakly related.
- Should be nicely indented

### Team Rules

- Teams should decide on a rule for formatting

## Chapter 6: Objects and Data Structures

### Data Abstraction

- Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding
  implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.
- We do not want to expose the details of our data. Rather we want to express our data in abstract terms. This is not
  merely accomplished by using interfaces and/or getters and setters. Serious thought needs to be put into the best way to represent the data that an object contains. The worst option is to blithely add getters and setters.

### Data/Object Anti-Symmetry

- Objects hide their data behind abstractions and expose functions that operate on that data. Data struc- ture expose
  their data and have no meaningful functions.
  
  > Procedural code (code using data structures) makes it easy to add new functions without changing the existing data
  >structures. OO code, on the other hand, makes it easy to add new classes without changing existing functions. 

  The complement is also true:
  
  > Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it 
  > hard to add new functions because all the classes must change.
  
### Law of Demeter

- The Law of Demeter says that a method f of a class C should only call the methods of these:
    - C
    - An object created by f
    - An object passed as an argument to f
    - An object held in an instance variable of C
- Talk to friends, not to strangers.

### Train Wrecks


## Chapter 7: Error Handling

### Use Exceptions Rather Than Return Codes

- It is better to throw an exception when you encounter an error. The calling code is cleaner. Its logic is not 
  obscured by error handling.

### Write Your Try-Catch-Finally Statement First

- In a way, try blocks are like transactions. Your catch has to leave your program in a consistent state, no matter what
  happens in the try. For this reason it is good practice to start with a try-catch-finally statement when you are writing code that could throw exceptions. This helps you define what the user of that code should expect, no matter what goes wrong with the code that is executed in the try.

### Use Unchecked Exceptions

- Checked exceptions can sometimes be useful if you are writing a critical library: You must catch them. But in general
  application development the dependency costs outweigh the benefits.

### Provide Context with Exceptions

- Create informative error messages and pass them along with your exceptions. Men- tion the operation that failed and
  the type of failure. If you are logging in your application, pass along enough information to be able to log the error in your catch.

### Define Exception Classes in Terms of a Caller’s Needs

- wrapping third-party APIs is a best practice. When you wrap a third-party API, you minimize your dependencies upon it.
- You can choose to move to a different library in the future without much penalty.
- Wrapping also makes it easier to mock out third-party calls when you are testing your own code.

### Define the Normal Flow

- SPECIAL CASE PATTERN [Fowler]: You create a class or configure an object so that it handles a special case for you. 
  When you do, the client code doesn’t have to deal with exceptional behavior. That behavior is encapsulated in the special case object.
  ```
  try {
    MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
    m_total += expenses.getTotal();
  } catch(MealExpensesNotFound e) {
    m_total += getMealPerDiem();
  }
  ```
  can become better by below example -
  ```
  MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
  m_total += expenses.getTotal();
  // the Exception is handled in the DAO and getMails returns
  // PerDiemMealExpenses if an error is thrown...
  public class PerDiemMealExpenses implements MealExpenses {
    public int getTotal() {
    // return the per diem default
    }
  }
  ```

### Don’t Return Null

- When we return null, we are essentially creating work for ourselves and foisting problems upon our callers. All it
  takes is one missing null check to send an application spinning out of control.
- If you are tempted to return null from a method, consider throwing an exception or returning a SPECIAL CASE object
  instead. If you are calling a null-returning method from a third-party API, consider wrapping that method with a
  method that either throws an exception or returns a special case object.

### Don’t Pass Null

- Returning null from methods is bad, but passing null into methods is worse. Unless you are working with an API which 
  expects you to pass null, you should avoid passing null in your code whenever possible.

## Boundaries

- There is a natural tension between the provider of an interface and the user of an interface. Providers of third-party 
  packages and frameworks strive for broad applicability so they can work in many environments and appeal to a wide audience. Users, on the other hand, want an interface that is focused on their particular needs. This tension can cause problems at the boundaries of our systems.
- In JAVA Maps have a very broad interface with plenty of capabilities. Certainly this power and flexi- bility is useful, but it can also be a liability.
  If we need a Map of Sensors we can implement it like below 
  ```
  // Without generics
  Map sensors = new HashMap();
  Sensor s = (Sensor) sensors.get(sensorId);
  // With generics:
  Map<Sensor> sensors = new HashMap<Sensor>();
  Sensor s = sensors.get(sensorId);
  ```
  We can make it cleaner by encapsulating -
  ```
  public class Sensor {
    private Map sensors = new HashMap();

    public Sensor getById(String id) {
      return (Sensor) sensor.get(id);
    }
  }
  ```
### Exploring and Learning Boundaries

- Learning the third-party code is hard. Integrating the third-party code is hard too. Doing both at the same time is
  doubly hard. What if we took a different approach? Instead of experimenting and trying out the new stuff in our production code, we could write some tests to explore our understanding of the third-party code.

### Learning Tests Are Better Than Free

- Learning tests verify that the third-party packages we are using work the way we expect them to.
- Whether you need the learning provided by the learning tests or not, a clean boundary should be supported by a set of
  outbound tests that exercise the interface the same way the production code does. Without these boundary tests to ease the migration, we might be tempted to stay with the old version longer than we should.

### Using Code That Does Not Yet Exist

- Sometimes you have boundaries in your system that represents things that had not been designed yet. Inteface can 
  be used for this purpose.
  
### Clean Boundaries

- Code at the boundaries needs clear separation and tests that define expectations. We should avoid letting too much of
  our code know about the third-party particulars. It’s better to depend on something you control than on something 
  you don’t control, lest it end up controlling you.


## Chapter 9: Unit Tests

### The Three Laws of TDD

- **First Law** You may not write production code until you have written a failing unit test.
- **Second Law** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
- **Third Law** You may not write more production code than is sufficient to pass the currently failing test.

### Keeping Tests Clean

- Test code is just as important as production code. It is not a second-class citizen. It requires thought, design, and care. It must be kept as clean as production code.

### Tests Enable the -ilities

- If you don’t keep your tests clean, you will lose them. And without them, you lose the very thing that keeps your
  production code flexible.
- Tests enable all the -ilities, because tests enable change.
- If your tests are dirty, then your ability to change your code is hampered, and you begin to lose the ability to
  improve the structure of that code. The dirtier your tests, the dirtier your code becomes. Eventually you lose the tests, and your code rots.

### Clean Tests

- What makes a clean test? Three things. Readability, readability, and readability.

  Example

  Without refactor:

  ```
  public void testGetPageHieratchyAsXml() throws Exception{
    crawler.addPage(root, PathParser.parse("PageOne"));
    crawler.addPage(root, PathParser.parse("PageOne.ChildOne"));
    crawler.addPage(root, PathParser.parse("PageTwo"));
    
    request.setResource("root");
    request.addInput("type", "pages");
    Responder responder = new SerializedPageResponder();
    SimpleResponse response =(SimpleResponse) responder.makeResponse(new FitNesseContext(root), request);
    String xml = response.getContent();
    
    assertEquals("text/xml", response.getContentType());
    assertSubString("<name>PageOne</name>", xml);
    assertSubString("<name>PageTwo</name>", xml);
    assertSubString("<name>ChildOne</name>", xml);
  }
  ```
  Refactored:
  ```
  public void testGetPageHierarchyAsXml() throws Exception {
    makePages("PageOne", "PageOne.ChildOne", "PageTwo");
  
    submitRequest("root", "type:pages");
  
    assertResponseIsXML();
    assertResponseContains("<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>");
  }
  ```

### Domain-Specific Testing Language

- This testing API is not designed up front; rather it evolves from the continued refac- toring of test code that has
  gotten too tainted by obfuscating detail.

### A Dual Standard

- There are things that you might never do in a production environment that are perfectly fine in a test environment.
  Usually they involve issues of memory or CPU efficiency. But they never involve issues of cleanliness.

### One Assert per Test

- The number of asserts in a test ought to be minimized.

### Single Concept per Test

- The best rule is that you should minimize the number of asserts per concept and test just one concept per test 
  function.

### F.I.R.S.T.

- Fast: you want to run them fequently.
- Independent: should not depend on each other.
- Repeatable: in any environment, in your laptop, without network...
- Self-Validating: should have a boolean output... not a log that you have to read to know the result.
- Timely: Write them before the production code, if you do it after maybe the production code will be hard to test.

## Chapter 10: Classes

### Class Organization

- public static constants
- private static variables 
- private instance variables
- public functions
- private functions 

### Encapsulation

- Utitlity functions should be private but could be protected to be accesible by tests in the same package.

### Classes Should Be Small!

- As small as possible
- With functions we count lines, with classes we count responsibilities.
- The more ambiguous the class name, the more likely it has too many responsibilities. For example, class names
  including weasel words like Processor or Manager or Super often hint at unfortunate aggregation of responsibilities.
- We should also be able to write a brief description of the class in about 25 words, without using the words “if,”
  “and,” “or,” or “but.”

### The Single Responsibility Principle

- Classes should have one responsibility—one reason to change.
- A system with many small classes has no more moving parts than a system with a few large classes. There is just as
  much to learn in the system with a few large classes. So the question is: Do you want your tools organized into toolboxes with many small drawers each containing well-defined and well-labeled components? Or do you want a few drawers that you just toss everything into?
  
### Cohesion

- the more variables a method manipulates the more cohesive that method is to its class. A class in which each variable
  is used by each method is maximally cohesive.
- We would like cohesion to be high. When cohesion is high, it means that the methods and variables of the class are
  co-dependent and hang together as a logical whole.

### Maintaining Cohesion Results in Many Small Classes

- When classes lose cohesion split them!
- Breaking a large function into many smaller functions often gives us the opportunity to split several smaller classes
  out as well
- Write a test suit that verified the precise behavior of the first version. Then tiny little changes, one at a time 
  to get the desired result.

### Organizing for Change

- Classes should be open for extension but closed for modification.
- We want to structure our systems so that we muck with as little as possible when we update them with new or changed
  features. In an ideal system, we incorporate new fea- tures by extending the system, not by making modifications to existing code.

### Isolating from Change

-  Classes should depend upon abstractions, not on concrete details.

## Chapter 11: Systems

### Separate Constructing a System from Using It

- Software systems should separate the startup process, when the application objects are constructed and the
  dependencies are “wired” together, from the runtime logic that takes over after startup.
  ```
  public Service getService() { if (service == null)
    service = new MyServiceImpl(...); // Good enough default for most cases? return service;
  }
  ```
  This is the LAZY INITIALIZATION/EVALUATION idiom, and it has several merits. We don’t incur the overhead of
  construction unless we actually use the object, and our startup times can be faster as a result. We also ensure that null is never returned.

  However, we now have a hard-coded dependency on MyServiceImpl and everything its constructor requires (which I have
  elided). We can’t compile without resolving these dependencies, even if we never actually use an object of this type
  at runtime!

  If we are diligent about building well-formed and robust systems, we should never let little, convenient idioms lead
  to modularity breakdown. The startup process of object con- struction and wiring is no exception. We should modularize
  this process separately from the normal runtime logic and we should make sure that we have a global, consistent
  strategy for resolving our major dependencies.

### Separation of Main

- One way to separate construction from use is simply to move all aspects of construction to main, or modules called by
  main, and to design the rest of the system assuming that all objects have been constructed and wired up appropriately.

### Dependency Injection

- In the context of dependency management, an object should not take responsibility for instantiating dependencies
  itself. Instead, it should pass this responsibility to another “authoritative” mecha- nism, thereby inverting the control.

### Scaling Up

- It is a myth that we can get systems “right the first time.” Instead, we should imple- ment only today’s stories, then
  refactor and expand the system to implement new stories tomorrow. This is the essence of iterative and incremental agility. Test-driven develop- ment, refactoring, and the clean code they produce make this work at the code level.
- Software systems are unique compared to physical systems. Their architectures can grow incrementally, if we maintain
  the proper separation of concerns.

### Optimize Decision Making

- Modularity and separation of concerns make decentralized management and decision making possible. In a sufficiently
  large system, whether it is a city or a software project, no one person can make all the decisions.
- We all know it is best to give responsibilities to the most qualified persons. We often forget that it is also best to
  postpone decisions until the last possible moment. This isn’t lazy or irresponsible; it lets us make informed choices
  with the best possible information. A premature decision is a decision made with suboptimal knowledge. We will have
  that much less customer feedback, mental reflection on the project, and experience with our implementation choices if
  we decide too soon.

### Use Standards Wisely, When They Add Demonstrable Value

- Standards make it easier to reuse ideas and components, recruit people with relevant experience, encapsulate good
  ideas, and wire components together. However, the process of creating standards can sometimes take too long for
  industry to wait, and some standards lose touch with the real needs of the adopters they are intended to serve.

### Systems Need Domain-Specific Languages

- A good DSL minimizes the “communication gap” between a domain concept and the code that implements it, just as agile
  practices optimize the communications within a team and with the project’s stakeholders. If you are implementing
  domain logic in the same language that a domain expert uses, there is less risk that you will incorrectly trans-
  late the domain into the implementation.
- DSLs, when used effectively, raise the abstraction level above code idioms and design patterns. They allow the
  developer to reveal the intent of the code at the appropriate level of abstraction.
