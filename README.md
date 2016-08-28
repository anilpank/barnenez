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


### I Can't Get This Class into a Test Harness

#### Most common problems in getting class into Test Harness
- Objects of the class can't be created easily.
- The constructor we need to use has bad side effects.
-  Significant work happens in the constructor, and we need to sense it.

#### How do we get started? How to take care of irritating parameters
- the best approach is to just try to do it.
- We could do a lot of analysis to find out why it would or would not be easy or hard, but it is just as easy to create a JUnit test class, type this into it, and compile the code:
public void testCreate() {
     LegacyClass validator = new LegacyClass();
}
- the best way to make a fake object is to use Extract Interface.

#### Test Code vs. Production Code
- Test code doesn't have to live up to the same standards as production code.
- I don't mind breaking encapsulation by making variables public if it makes it easier to write tests.

#### Pass Null
- When you are writing tests and an object requires a parameter that is hard to construct, consider just passing null instead.
-  If the parameter is used in the course of your test execution, the code will throw an exception and the test harness will catch the exception. 

#### Null Object Pattern
- The Null Object Pattern is a way of avoiding the use of null in programs. 
- An instance of NullEmployee has no name and no address, and when you tell it to pay, it just does nothing

#### Other ways of approaching irritating parameters.
- Pass Null and Extract Interface are two ways of approaching irritating parameters. 
- If the problematic dependency in a parameter isn't hard-coded into its constructor, we can use Subclass and Override Method to get rid of the dependency.
- If the constructor of Base class uses its connect method to form a connection, we could break the dependency by overriding connect() in a testing subclass.

#### The Case of the Hidden Dependency
- Some classes are deceptive. We look at them, we find a constructor that we want to use, and we try to call it. Then, bang! We run into an obstacle. One of the most common obstacles is hidden dependency.
-  The constructor uses some resource that we just can't access nicely in our test harness.
- The fundamental problem here is that the dependency on some special class is hidden in the constructor.
- One of the techniques we can use is Parameterize Constructor.
- With this technique, we externalize a dependency that we have in a constructor by passing it into the constructor.
- Dependencies hidden in constructors can be tackled with many techniques. Often we can use Extract and Override Getter (352), Extract and Override Factory Method, and Supersede Instance Variable, but I like to use Parameterize Constructor (379) as often as I can.

#### To Parameterize Constructor, follow these steps:

- Identify the constructor that you want to parameterize and make a copy of it.

- Add a parameter to the constructor for the object whose creation you are going to replace. Remove the object creation and add an assignment from the parameter to the instance variable for the object.

- If you can call a constructor from a constructor in your language, remove the body of the old constructor and replace it with a call to the old constructor. Add a new expression to the call of the new constructor in the old constructor. If you canâ€™t call a constructor from another constructor in your language, you may have to extract any duplication among the constructors to a new method.

#### Construction Blob
- Parameterize Constructor is one of the easiest techniques that we can use to break hidden dependencies in a constructor.
-  If a constructor constructs a large number of objects internally or accesses a large number of globals, we could end up with a very large parameter list.
-  In worse situations, a constructor creates a few objects and then uses them to create other objects.
- One option to solve this is to supersede instance variable.
void supersedeCursor(FocusWidget newCursor) {
    cursor = newCursor;
}
- We can't use it on final instance variables in Java.





#### Irritating Global Dependencies aka Singletons

- The first step is to add a new static method to the singleton class. The method allows us to replace the static instance in the singleton.

    public static void setTestingInstance(MyRepo newInstance)
    {
        instance = newInstance;
    }
	
- Reset For Testing

  public class MyRepo
{
    ...
    public void resetForTesting() {
        instance = null;
    }
    ...
}
If we call this method in our test setUp (and it's a good idea to call it in tearDown also), we can create fresh singletons for every test.



















