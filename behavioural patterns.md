## Behavioural Patterns

List of Behavioral Design Patterns, ordered from the most straightforward to those that require more architectural overhead (increasing complexity).

# Strategy
* Complexity: Low
* Description: Defines a family of algorithms, puts each of them into a separate class, and makes their objects interchangeable.
* Example: Choosing between different payment methods (Credit Card, PayPal, Crypto) at checkout.
---
	// Swaps algorithms at runtime.

	interface PaymentStrategy { void pay(int amount); }

	class PayPal implements PaymentStrategy { public void pay(int a) { System.out.println("Paid " + a + " via PayPal"); } }
	class CreditCard implements PaymentStrategy { public void pay(int a) { System.out.println("Paid " + a + " via Card"); } }

	class ShoppingCart {
		private PaymentStrategy strategy;
		public void setStrategy(PaymentStrategy s) { this.strategy = s; }
		public void checkout(int amount) { strategy.pay(amount); }
	}
---

# Template Method
* Complexity: Low
* Description: Defines the skeleton of an algorithm in a superclass but lets subclasses override specific steps of the algorithm without changing its structure.
* Example: A data miner that follows the same steps (Open, Read, Process, Close) but handles different file formats (PDF, CSV).
---
	// Defines the skeleton of an algorithm, letting subclasses fill in the blanks.

	abstract class Game {
		abstract void initialize();
		abstract void start();
		public final void play() { // The Template
			initialize();
			start();
		}
	}

	class Football extends Game {
		void initialize() { System.out.println("Football Init"); }
		void start() { System.out.println("Kick-off"); }
	}
---

# Command
* Complexity: Medium
* Description: Turns a request into a stand-alone object that contains all information about the request. This allows you to pass requests as method arguments, delay or queue a request's execution, and support undoable operations.
* Example: A "Remote Control" where each button is a command object that knows how to turn a specific device on or off.
---
	// Encapsulates a request as an object.

	interface Command { void execute(); }

	class Light { void on() { System.out.println("Light On"); } }
	class LightOnCommand implements Command {
		private Light light;
		public LightOnCommand(Light l) { this.light = l; }
		public void execute() { light.on(); }
	}

	class RemoteControl {
		public void pressButton(Command c) { c.execute(); }
	}
---

# State
* Complexity: Medium
* Description: Lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.
* Example: A Vending Machine that behaves differently depending on whether it's "Waiting for Coin," "Selecting Product," or "Out of Stock."
---
	// Object behavior changes based on its internal state.

	interface State { void handle(); }

	class SilentState implements State { public void handle() { System.out.println("Vibrating..."); } }
	class RingerState implements State { public void handle() { System.out.println("Ringing!!!"); } }

	class MobilePhone {
		private State currentState = new RingerState();
		public void setState(State s) { this.currentState = s; }
		public void alert() { currentState.handle(); }
	}
---

# Observer
* Complexity: Medium
* Description: Defines a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.
* Example: A YouTube channel (Subject) notifying all its subscribers (Observers) when a new video is posted.
---
	// the Publisher-Subscriber" model.

	interface Observer { void update(String msg); }

	class User implements Observer {
		private String name;
		public User(String n) { this.name = n; }
		public void update(String m) { System.out.println(name + " received: " + m); }
	}

	class Newsletter {
		private List<Observer> subs = new ArrayList<>();
		public void subscribe(Observer o) { subs.add(o); }
		public void notifyAll(String m) { for(Observer o : subs) o.update(m); }
	}
---

# Iterator
* Complexity: Medium
* Description: Lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).
* Example: A "Next" button that works the same way whether you are browsing a Facebook feed or a local folder of photos.
---
	// Accesses elements of a collection sequentially without exposing its internal structure

	interface MyIterator { boolean hasNext(); Object next(); }

	class NameRepository {
		public String names[] = {"John", "Jane", "Joe"};
		public MyIterator getIterator() { return new NameIterator(); }

		private class NameIterator implements MyIterator {
			int index;
			public boolean hasNext() { return index < names.length; }
			public Object next() { return hasNext() ? names[index++] : null; }
		}
	}
---

# Chain of Responsibility
* Complexity: High
* Description: Lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
* Example: A customer support system: Level 1 (Bot) → Level 2 (Human) → Level 3 (Manager).
---
	// Passes a request along a chain of potential handlers.

	abstract class Logger {
		protected Logger next;
		public void setNext(Logger n) { this.next = n; }
		abstract void log(String msg, int level);
	}

	class ConsoleLogger extends Logger {
		void log(String m, int l) { 
			System.out.println("Console: " + m);
			if (next != null) next.log(m, l); 
		}
	}
---


# Mediator
* Complexity: High
* Description: Reduces chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.
* Example: An Air Traffic Control tower that manages communication between planes so they don't have to talk to each other directly.
---
	// Centralizes complex communications between multiple objects.

	class ChatRoom { // The Mediator
		public static void showMessage(String user, String msg) {
			System.out.println(user + ": " + msg);
		}
	}

	class UserProfile {
		private String name;
		public UserProfile(String n) { this.name = n; }
		public void send(String msg) { ChatRoom.showMessage(this.name, msg); }
	}
---

# Memento
* Complexity: High
* Description: Lets you save and restore the previous state of an object without revealing the details of its implementation (encapsulation).
* Example: An "Undo" (Ctrl+Z) feature in a text editor.
---
	// Captures and restores an object's internal state

	class EditorMemento {
		private final String content;
		public EditorMemento(String c) { this.content = c; }
		public String getContent() { return content; }
	}

	class Editor {
		private String content;
		public void setContent(String c) { this.content = c; }
		public EditorMemento save() { return new EditorMemento(content); }
		public void restore(EditorMemento m) { this.content = m.getContent(); }
	}
---

# Visitor
* Complexity: Very High
* Description: Lets you separate algorithms from the objects on which they operate. You can add new operations to existing object structures without modifying those structures.
* Example: An insurance agent (Visitor) visiting a house (Object) to provide an estimate without the house needing to know how to calculate insurance.
---
	// Adds new operations to a class hierarchy without modifying the classes.

	interface Element { void accept(Visitor v); }
	interface Visitor { void visit(Book b); }

	class Book implements Element {
		public void accept(Visitor v) { v.visit(this); }
	}

	class PriceVisitor implements Visitor {
		public void visit(Book b) { System.out.println("Calculating Price..."); }
	}
---
