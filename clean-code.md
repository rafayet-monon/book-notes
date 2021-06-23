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


