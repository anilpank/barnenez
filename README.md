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

### CHANGING SOFTWARE
- I Don't Have Much Time and I Have to Change It
- With tests around the code, nailing down functional problems is often easier.
- Assume the worst case. The change was simple, but we got the code around the change under test anyway; we make all of our changes correctly. Were the tests worth it? We don't know when we shall get back to that area of the code and make another change.
- Would it be easier to understand if the classes were smaller and there were unit tests? Chances are, it would.
- When you get over the hump, life isn't completely rosy, but it is better. When you know the value of testing and you've felt the difference, the only thing that you have to deal with is the cold, mercenary decision of what to do in each particular case.


