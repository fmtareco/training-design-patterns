# Behavioural Patterns

List of Behavioral Design Patterns, ordered from the most straightforward to those that require more architectural overhead (increasing complexity).

1. Strategy

* Complexity: Low
* Description: Defines a family of algorithms, puts each of them into a separate class, and makes their objects interchangeable.
* Example: Choosing between different payment methods (Credit Card, PayPal, Crypto) at checkout.

2. Template Method

* Complexity: Low
* Description: Defines the skeleton of an algorithm in a superclass but lets subclasses override specific steps of the algorithm without changing its structure.
* Example: A data miner that follows the same steps (Open, Read, Process, Close) but handles different file formats (PDF, CSV).

3. Command

* Complexity: Medium
* Description: Turns a request into a stand-alone object that contains all information about the request. This allows you to pass requests as method arguments, delay or queue a request's execution, and support undoable operations.
* Example: A "Remote Control" where each button is a command object that knows how to turn a specific device on or off.

4. State

* Complexity: Medium
* Description: Lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.
* Example: A Vending Machine that behaves differently depending on whether it's "Waiting for Coin," "Selecting Product," or "Out of Stock."

5. Observer

* Complexity: Medium
* Description: Defines a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.
* Example: A YouTube channel (Subject) notifying all its subscribers (Observers) when a new video is posted.

6. Iterator

* Complexity: Medium
* Description: Lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).
* Example: A "Next" button that works the same way whether you are browsing a Facebook feed or a local folder of photos.

7. Chain of Responsibility

* Complexity: High
* Description: Lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
* Example: A customer support system: Level 1 (Bot) → Level 2 (Human) → Level 3 (Manager).

8. Mediator

* Complexity: High
* Description: Reduces chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.
* Example: An Air Traffic Control tower that manages communication between planes so they don't have to talk to each other directly.

9. Memento

* Complexity: High
* Description: Lets you save and restore the previous state of an object without revealing the details of its implementation (encapsulation).
* Example: An "Undo" (Ctrl+Z) feature in a text editor.

10. Visitor

* Complexity: Very High
* Description: Lets you separate algorithms from the objects on which they operate. You can add new operations to existing object structures without modifying those structures.
* Example: An insurance agent (Visitor) visiting a house (Object) to provide an estimate without the house needing to know how to calculate insurance.


