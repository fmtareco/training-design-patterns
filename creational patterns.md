# Creational Patterns

List of Creational Design Patterns, ordered from the most straightforward to those that require more architectural overhead (increasing complexity).
These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

* Singleton
* Complexity: Low
   * Description: Ensures that a class has only one instance while providing a global access point to this instance.
   
  public class DatabaseConnection {
    private static DatabaseConnection instance;

    private DatabaseConnection() {} // Private constructor

    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
}
 
* Factory Method
* Complexity: Medium
   * Description: Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
   
// Product interface
interface Notification { void send(); }

// Concrete Products
class Email implements Notification { public void send() { System.out.println("Sending Email"); } }
class SMS implements Notification { public void send() { System.out.println("Sending SMS"); } }

// Creator (The Factory)
class NotificationFactory {
    public Notification createNotification(String type) {
        if (type.equals("EMAIL")) return new Email();
        if (type.equals("SMS")) return new SMS();
        return null;
    }
}
   
   
* Builder
* Complexity: Medium
   * Description: Lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.
   
   public class Car {
    private String engine;
    private int wheels;
    private boolean hasGPS;

    private Car(Builder builder) {
        this.engine = builder.engine;
        this.wheels = builder.wheels;
        this.hasGPS = builder.hasGPS;
    }

    public static class Builder {
        private String engine;
        private int wheels;
        private boolean hasGPS;

        public Builder setEngine(String e) { this.engine = e; return this; }
        public Builder setWheels(int w) { this.wheels = w; return this; }
        public Builder setGPS(boolean g) { this.hasGPS = g; return this; }
        public Car build() { return new Car(this); }
    }
}
// Usage: Car c = new Car.Builder().setEngine("V8").setGPS(true).build();

   
* Prototype
* Complexity: Medium
   * Description: Allows copying existing objects without making your code dependent on their classes (cloning).
   
   abstract class Shape implements Cloneable {
    public String type;
    public Object clone() {
        try { return super.clone(); } 
        catch (CloneNotSupportedException e) { return null; }
    }
}

class Circle extends Shape {
    public Circle() { type = "Circle"; }
}
// Usage: Circle c1 = new Circle(); Circle c2 = (Circle) c1.clone();

   
* Abstract Factory
* Complexity: High
   * Description: Lets you produce families of related objects without specifying their concrete classes. 
   It is often described as a "Factory of Factories."
   
// Families: Victorian vs Modern
interface Chair { void sitOn(); }
interface Table { void eatOn(); }

interface FurnitureFactory {
    Chair createChair();
    Table createTable();
}

class ModernFurnitureFactory implements FurnitureFactory {
    public Chair createChair() { return new ModernChair(); }
    public Table createTable() { return new ModernTable(); }
}
// This allows you to swap the entire "style" of the app by changing one factory.
