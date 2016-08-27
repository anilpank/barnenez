# barnenez
Tips to work with legacy code

- Documentation
- One bite at a time

- A unit test that takes 1/10th of a second to run is a slow unit test.
- If we can put some other code in its place and test through it, we can write our tests. In object orientation, these other pieces of code are often called fake objects
- Fake Objects Support Real Tests

Unit tests run fast. If they don't run fast, they aren't unit tests.
Other kinds of tests often masquerade as unit tests. A test is not a unit test if:
1. It talks to a database.
2. It communicates across a network.
3. It touches the file system.
4. You have to do special things to your environment (such as editing configuration files) to run it.

Dependency is one of the most critical problems in software development. Much legacy code work involves breaking dependencies so that change can be easier.

A seam is a place where you can alter behavior in your program without editing in that place.
In Java first thing you do is to extend classes to interfaces, so that interfaces are always method parameters, instance variables, etc. This way you can always alter their behaviors in order to test them.
Enabling Point - Every seam has an enabling point, a place where you can make the decision to use one behavior or another.
It is important to choose the right type of seam when you want to get pieces of code under test. In general, object seams are the best choice in object-oriented languages.

refactoring (n.). A change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its existing behavior.
Try out some refactoring tools

## CHANGING SOFTWARE

### I Don't Have Much Time and I Have to Change It

- With tests around the code, nailing down functional problems is often easier.
- Assume the worst case. The change was simple, but we got the code around the change under test anyway; we make all of our changes correctly. Were the tests worth it? We don't know when we shall get back to that area of the code and make another change.
- Would it be easier to understand if the classes were smaller and there were unit tests? Chances are, it would.
- When you get over the hump, life isn't completely rosy, but it is better. When you know the value of testing and you've felt the difference, the only thing that you have to deal with is the cold, mercenary decision of what to do in each particular case.
- If you have to make a change to a class right now, try instantiating the class in a test harness

#### Sprout Method
- When you need to add a feature to a system and it can be formulated completely as new code, write the code in a new method. 
- Call it from the places where the new functionality needs to be.

#### Steps to create a sprout method
- Identify where you need to make your code change.
-  If the change can be formulated as a single sequence of statements in one place in a method, write down a call for a new method that will do the work involved and then comment it out.
- Determine what local variables you need from the source method, and make them arguments to the call.
- Determine whether the sprouted method will need to return values to source method. If so, change the call so that its return value is assigned to a variable.
- Develop the sprout method using test-driven development.
- Remove the comment in the source method to enable the call.

#### Sprout Class
Here are the steps for Sprout Class:
- Identify where you need to make your code change.
- If the change can be formulated as a single sequence of statements in one place in a method, think of a good name for a class that could do that work. Afterward, write code that would create an object of that class in that place, and call a method in it that will do the work that you need to do; then comment those lines out.
- Determine what local variables you need from the source method, and make them arguments to the classesâ€™ constructor.
- Determine whether the sprouted class will need to return values to the source method. If so, provide a method in the class that will supply those values, and add a call in the source method to receive those values.
- Develop the sprout class test first (see test-driven development (88)).
- Remove the comment in the source method to enable the object creation and calls.

#### Wrap Method
Here are the steps for the first version of the Wrap Method:
- Identify a method you need to change.
- If the change can be formulated as a single sequence of statements in one place, rename the method and then create a new method with the same name and signature as the old method. Remember to Preserve Signatures (312) as you do this.
- Place a call to the old method in the new method.
- Develop a method for the new feature, test first (see test-driven development (88)), and call it from the new method
- In the second version, when we donâ€™t care to use the same name as the old method, the steps look like this:
- Identify a method you need to change.
- If the change can be formulated as a single sequence of statements in one place, develop a new method for it using test-driven development (88).
- Create another method that calls the new method and the old method.

### It takes a lot of time to make a change
- In a legacy system, it can take a long time to figure out what to do, and the change is difficult also. 
- it seems like no amount of time will be enough to understand everything you need to do to make a change
- you have to walk blindly into the code and start.
- Changes often take a long time for another very common reason: lag time. Lag time is the amount of time that passes between a change that you make and the moment that you get real feedback about the change
- Dependencies can be problematic, but, fortunately, we can break them. In object-oriented code, often the first step is to attempt to instantiate the classes that we need in a test harness.


### How Do I Add a Feature
- In general, it's better to confront the beast than hide from it.
- The most powerful feature-addition technique I know of is test-driven development (TDD).

#### Test-driven development 
- Write a failing test case.
- Get it to compile.
- Make it pass.
- Remove duplication.
- Repeat.

#### TDD and Legacy Code
- One of the most valuable things about TDD is that it lets us concentrate on one thing at a time.
- We are either writing code or refactoring; we are never doing both at once.
- That separation is particularly valuable in legacy code because it lets us write new code independently of new code.









