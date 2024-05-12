Factory method -- creational design pattern which solves the problem of creating product objects without specifying their concrete classes.

```java
// Library classes
abstract class Vehicle {
  public abstract void printVehicle();
}

class TwoWheeler extends Vehicle {
  public void printVehicle() {
    System.out.println("I am two wheeler");
  }
}

class FourWheeler extends Vehicle {
  public void printVehicle() {
    System.out.println("I am four wheeler");
  }
}

// Factory Interface
interface AbstractFactory {
  Vehicle createVehicle(String vehicleType);
}

// Concrete Factory
class VehicleFactory implements VehicleFactory {
  public Vehicle createVehicle(String vehicleType) {
	if("TWOWHEELER".equalsIgnoreCase(vehicleType))
    	return new TwoWheeler();
	if("FOURWHEELER".equalsIgnoreCase(vehicleType))
		return new TwoWheeler();
	return null;
  }
}

// Driver program
public class GFG {
  public static void main(String[] args) {
    VehicleFactory vehicleFactory = new VehicleFactory();
    Vehicle twoWheeler = vehicleFactory.createVehicle("TWOWHEELER");
    twoWheeler.printVehicle();
    Vehicle fourWheeler = vehicleFactory.createVehicle("FOURWHEELER");
    fourWheeler.printVehicle();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Abstract factory method -- Same thing as factory method but for group of related objects. Creational design pattern, which solves the problem of creating entire product families without specifying their concrete classes. In simpler terms the Abstract Factory Pattern is a way of organizing how you create groups of objects that are related to each other.

```java
// Library classes
abstract class Vehicle {
  public abstract void printVehicle();
}

class TwoWheeler extends Vehicle {
  public void printVehicle() {
    System.out.println("I am two wheeler");
  }
}

class FourWheeler extends Vehicle {
  public void printVehicle() {
    System.out.println("I am four wheeler");
  }
}

abstract class Engine {
  public abstract void printEngine();
}

class TwoWheelerEngine extends Engine {
  public void printEngine() {
    System.out.println("I am two wheeler engine");
  }
}

class FourWheelerEngine extends Engine {
  public void printEngine() {
    System.out.println("I am four wheeler engine");
  }
}

// Abstract Factory
interface AbstractFactory {
  Vehicle createVehicle();
  Engine createEngine();
}

// Concrete Factory for TwoWheelers
class TwoWheelerFactory implements AbstractFactory {
  public Vehicle createVehicle() {
    return new TwoWheeler();
  }
  public Engine createEngine() {
    return new TwoWheelerEngine();
  }
}

// Concrete Factory for FourWheelers
class FourWheelerFactory implements AbstractFactory {
  public Vehicle createVehicle() {
    return new FourWheeler();
  }
  public Engine createEngine() {
    return new FourWheelerEngine();
  }
}

// Driver program
public class GFG {
  public static void main(String[] args) {
    AbstractFactory twoWheelerFactory = new TwoWheelerFactory();
    Vehicle twoWheeler = twoWheelerFactory.createVehicle();
    Engine twoWheelerEngine = twoWheelerFactory.createEngine();
    twoWheeler.printVehicle();
    twoWheelerEngine.printEngine();

    AbstractFactory fourWheelerFactory = new FourWheelerFactory();
    Vehicle fourWheeler = fourWheelerFactory.createVehicle();
    Engine fourWheelerEngine = fourWheelerFactory.createEngine();
    fourWheeler.printVehicle();
    fourWheelerEngine.printEngine();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Builder -- creational design pattern, which allows constructing complex objects step by step.

```java
public class Vehicle {

  // Required parameters
  private String vehicleType;
  private int wheels;

  // Optional parameters
  private String color;
  private boolean hasSunroof;

  private Vehicle(Builder builder) {
    this.vehicleType = builder.vehicleType;
    this.wheels = builder.wheels;
    this.color = builder.color;
    this.hasSunroof = builder.hasSunroof;
  }

  public static class Builder {

    // Required parameters
    private String vehicleType;
    private int wheels;

    // Optional parameters
    private String color;
    private boolean hasSunroof;

	// constructor for required fields
    public Builder(String vehicleType, int wheels) {
      this.vehicleType = vehicleType;
      this.wheels = wheels;
    }

	// setter methods for optional fields
    public Builder color(String val) {
      color = val;
      return this;
    }
    public Builder hasSunroof(boolean val) {
      hasSunroof = val;
      return this;
    }
    public Vehicle build() {
      return new Vehicle(this);
    }
  }
}

public class BuilderPatternDemo {
  public static void main(String[] args) {
    Vehicle car = new Vehicle.Builder("car", 4)
        .color("Red")
        .hasSunroof(true)
        .build();
    System.out.println(car.toString());
    Vehicle bike = new Vehicle.Builder("bike", 2)
        .color("Black")
        .hasSunroof(false)
        .build();
    System.out.println(bike.toString());
  }
}
```

------------------------------------------------------------------------------------------------------------------

Prototype -- creational design pattern that allows cloning objects, even complex ones, without coupling to their specific classes, i.e, it enables the creation of new objects by copying an existing object

```java
abstract class Vehicle {
  protected String vehicleType;
  protected String color;

  abstract void printVehicle();
  abstract Vehicle makeCopy();

  public void setColor(String color) {
    this.color = color;
  }
  public String getColor() {
    return color;
  }
}

class TwoWheeler extends Vehicle {
  public TwoWheeler() {
    this.vehicleType = "Two Wheeler";
  }

  @Override
  void printVehicle() {
    System.out.println("This is a " + this.color + " two wheeler vehicle");
  }

  @Override
  Vehicle makeCopy() {
    TwoWheeler copy = new TwoWheeler();
    copy.setColor(this.color);
    return copy;
  }
}

class FourWheeler extends Vehicle {
  public FourWheeler() {
    this.vehicleType = "Four Wheeler";
  }

  @Override
  void printVehicle() {
    System.out.println("This is a " + this.color + " four wheeler vehicle");
  }

  @Override
  Vehicle makeCopy() {
    FourWheeler copy = new FourWheeler();
    copy.setColor(this.color);
    return copy;
  }
}

public class Main {
  public static void main(String[] args) {
    Vehicle twoWheeler = new TwoWheeler();
    twoWheeler.setColor("Red");
    twoWheeler.printVehicle(); // This is a Red two wheeler vehicle

    Vehicle clonedTwoWheeler = twoWheeler.makeCopy();
    clonedTwoWheeler.printVehicle(); // This is a Red two wheeler vehicle

    Vehicle fourWheeler = new FourWheeler();
    fourWheeler.setColor("Blue");
    fourWheeler.printVehicle(); // This is a Blue four wheeler vehicle

    Vehicle clonedFourWheeler = fourWheeler.makeCopy();
    clonedFourWheeler.printVehicle(); // This is a Blue four wheeler vehicle
  }
}
```

------------------------------------------------------------------------------------------------------------------

Singleton -- creational design pattern, which ensures that only one object of its kind exists and provides a single point of access to it for any other code. [Must read the article https://www.baeldung.com/java-bill-pugh-singleton-implementation - this is for both multithreading & eager loading]
Scenarios -
	1.	Below example is of lazy loading. It can be eagerly loaded - implementation by making the instance variable static final and inside private constructor just do -> return new Singleton(). And in the static getInstance method return the instance.

```java
public class Vehicle {
  private static Vehicle instance;
  private String color;

  private Vehicle() {
  }

  public static Vehicle getInstance() {
    if (instance == null) {
      instance = new Vehicle();
    }
    return instance;
  }

  public void setColor(String color) {
    this.color = color;
  }
  public String getColor() {
    return color;
  }
  public void printVehicle() {
    System.out.println("This is a " + this.color + " vehicle");
  }
}

public class Main {
  public static void main(String[] args) {

    Vehicle vehicle = Vehicle.getInstance();
    vehicle.setColor("Red");
    vehicle.printVehicle(); // This is a Red vehicle

    Vehicle anotherVehicle = Vehicle.getInstance();
    anotherVehicle.printVehicle(); // This is still a Red vehicle
  }
}
```

------------------------------------------------------------------------------------------------------------------

Adapter -- structural design pattern, which allows incompatible objects to collaborate. An Adapter pattern acts as a connector between two incompatible interfaces that otherwise cannot be connected directly. Note that it is similar to bridge design pattern - bridge is up-front strategy whereas adapter is helpful in existing application.
Object Type adapter (Using composition) -
	1.	Use this when Bicycle class is a third party or client side class which is not modifiable, in that case it is better to have the adaptee as an object
	2.	Use this when you want to adapt multiple classes to same target interface
Class Type adapter (Using inheritance) -
	1.	Use when Bicycle class or adaptee class is modifiable.
	2.	When you want to minimize number of objects.
	3.	Straigthforward

```java
// Existing class
interface Vehicle {
  void start();
  void stop();
  }
}

// New class
class Bicycle {
  void pedal() {
    System.out.println("Bicycle is pedaling");
  }
  void brakes() {
    System.out.println("Bicycle is applying brakes");
  }
}

// OBJECT TYPE ADAPTER - uses composition of adaptee in the adapter
class BicycleToVehicleAdapter implements Vehicle {

  private Bicycle bicycle;

  public BicycleToVehicleAdapter(Bicycle bicycle) {
    this.bicycle = bicycle;
  }

  @Override
  void start() {
    bike.pedal();
  }
  @Override
  void stop() {
    bike.brakes();
  }
}

public class Main {
  public static void main(String[] args) {

    Bicycle bicycle = new Bicycle();
    Vehicle bikeAdapter = new BicycleToVehicleAdapter(bicycle);
    bikeAdapter.start(); // Bicycle is pedaling
    bikeAdapter.stop(); // Bicycle is applying brakes
  }
}

// Similar to above we can have CLASS TYPE ADAPTER - uses inheritance
class BicycleToVehicleAdapter2 extends Bicycle implements Vehicle {
 @Override
 void start() {
  pedal();
 }
 @Override
 void stop() {
  brakes();
 }
}
```

------------------------------------------------------------------------------------------------------------------

Bridge -- structural design pattern that divides business logic or huge class into separate class hierarchies that can be developed independently. It separate the abstraction from its implementation, so that the two can vary independently. One of these hierarchies (often called the Abstraction) will get a reference to an object of the second hierarchy (Implementation). Always remember it has 2 parts - abstraction & implementation.
Bridge design pattern can be used when both abstraction and implementation can have different hierarchies independently and we want to hide the implementation from the client application.

```java
// Implementor
interface Engine {
  void startEngine();
}

class PetrolEngine implements Engine {
  public void startEngine() {
    System.out.println("Petrol Engine started");
  }
}

class ElectricEngine implements Engine {
  public void startEngine() {
    System.out.println("Electric Engine started");
  }
}

// Abstraction
abstract class Vehicle {

  protected Engine engine; // composition implementor

  public Vehicle(Engine engine) {
    this.engine = engine;
  }
  abstract void start();
}

// Refined Abstraction
class Car extends Vehicle {
  public Car(Engine engine) {
    super(engine);
  }
  void start() {
    System.out.print("Car ");
    engine.startEngine();
  }
}

class Bike extends Vehicle {
  public Bike(Engine engine) {
    super(engine);
  }
  void start() {
    System.out.print("Bike ");
    engine.startEngine();
  }
}

public class Main {
  public static void main(String[] args) {

    Vehicle vehicle1 = new Car(new PetrolEngine());
    vehicle1.start(); // Car Petrol Engine started

    Vehicle vehicle2 = new Bike(new ElectricEngine());
    vehicle2.start(); // Bike Electric Engine started
  }
}
```

------------------------------------------------------------------------------------------------------------------

Composite -- structural design pattern that allows composing objects into a tree-like structure and work with the it as if it was a singular object. The composite pattern is meant to allow treating individual objects and compositions of objects, or “composites” in the same way. 

```java
// Base component
abstract class VehiclePart {
  void printPart() {}
}

// Leaf
class Engine extends VehiclePart {
  @Override
  void printPart() {
    System.out.println("Engine");
  }
}

// Leaf
class Wheel extends VehiclePart {
  @Override
  void printPart() {
    System.out.println("Wheel");
  }
}

// Composite
class Vehicle extends VehiclePart {

  private List<VehiclePart> parts = new ArrayList<>(); // important - it demonstrates the composition of objects, also methods for adding & removing elements from the list.

  void addPart(VehiclePart part) {
    parts.add(part);
  }
  void removePart(VehiclePart part) {
    parts.remove(part);
  }
  @Override
  void printPart() {
    for (VehiclePart part : parts) {
      part.printPart();
    }
  }
}

public class Main {
  public static void main(String[] args) {

    VehiclePart engine = new Engine();
    VehiclePart wheel = new Wheel();

    Vehicle vehicle = new Vehicle();
    vehicle.addPart(engine);
    vehicle.addPart(wheel);
    vehicle.printPart(); // Engine Wheel
  }
}
```

------------------------------------------------------------------------------------------------------------------

Decorator -- structural pattern that allows adding new behaviors to objects dynamically by placing them inside special wrapper objects, called decorators.
Use the Decorator pattern when you need to be able to assign extra behaviors to objects at runtime without breaking the code that uses these objects.
The disadvantage of decorator design pattern is that it uses a lot of similar kind of objects (decorators).

```java
// Component
abstract class Vehicle {
  abstract String getDescription();
  abstract double getCost();
}

// ConcreteComponent
class Car extends Vehicle {
  String getDescription() {
    return "Car";
  }
  double getCost() {
    return 10000.0;
  }
}

// Decorator
abstract class VehicleDecorator extends Vehicle {
  protected Vehicle vehicle;
}

// ConcreteDecoratorA
class WithSunroof extends VehicleDecorator {
  WithSunroof(Vehicle vehicle) {
    this.vehicle = vehicle;
  }
  String getDescription() {
    return vehicle.getDescription() + ", with sunroof";
  }
  double getCost() {
    return vehicle.getCost() + 500.0;
  }
}

// ConcreteDecoratorB
class WithNavigation extends VehicleDecorator {
  WithNavigation(Vehicle vehicle) {
    this.vehicle = vehicle;
  }
  String getDescription() {
    return vehicle.getDescription() + ", with navigation";
  }
  double getCost() {
    return vehicle.getCost() + 300.0;
  }
}

public class Main {
  public static void main(String[] args) {
    Vehicle car = new Car();
    System.out.println(car.getDescription() + " $" + car.getCost()); // Car $10000.0

    car = new WithSunroof(car);
    System.out.println(car.getDescription() + " $" + car.getCost()); // Car, with sunroof $10500.0

    car = new WithNavigation(car);
    System.out.println(car.getDescription() + " $" + car.getCost()); // Car, with sunroof, with navigation $10800.0
  }
}
```

------------------------------------------------------------------------------------------------------------------

Facade -- structural design pattern that provides a simplified (but limited) interface to a complex system of classes, library or framework. Simply put, a facade encapsulates a complex subsystem behind a simple interface. It hides much of the complexity and makes the subsystem easy to use. Also, if we need to use the complex subsystem directly, we still can do that; we aren’t forced to use the facade all the time. E.g - call the customer care, he will guide through everything like balance check, complaint, new plans, stop/start service, recharge etc. Basically, it means one stop shop for everything user wants to do, but it is encapsulated behind the facade, user gets his job done in simple terms.
Disadvantages- Being simple in implementation, sometimes the pattern can be overused in simple scenarios, which will lead to redundant implementations.

```java
class Engine {
  public void start() {
    System.out.println("Engine started");
  }
}

class Lights {
  public void on() {
    System.out.println("Lights turned on");
  }
}

class Radio {
  public void play() {
    System.out.println("Radio playing");
  }
}

// Facade
class Vehicle {
  private Engine engine;
  private Lights lights;
  private Radio radio;

  public Vehicle() {
    this.engine = new Engine();
    this.lights = new Lights();
    this.radio = new Radio();
  }

// facade method which hides the details - user only knows vehicle.start() not about what is happening in this method 
  public void start() {
    engine.start();
    lights.on();
    radio.play();
  }
}

public class Main {
  public static void main(String[] args) {
    Vehicle vehicle = new Vehicle();
    vehicle.start(); // Engine started Lights turned on Radio playing
  }
}
```

------------------------------------------------------------------------------------------------------------------

Flyweight -- structural design pattern that allows programs to support vast quantities of objects by keeping their memory consumption low. The pattern achieves it by sharing parts of object state between multiple objects. In other words, the Flyweight saves RAM by caching the same data used by different objects.
Before we apply flyweight design pattern, we need to consider following factors:
	1.	The number of Objects to be created by application should be huge.
	2.	The object creation is heavy on memory and it can be time consuming too.
	3.	The object properties can be divided into intrinsic and extrinsic properties. Intrinsic properties make the Object unique whereas extrinsic properties are set by client code and used to perform different operations

```java
// Flyweight
interface Vehicle {
  void assignDriver(String driverName);
  void move();
}

// ConcreteFlyweight
class Car implements Vehicle {
  private final String color; // intrinsic state
  public Car(String color) {
    this.color = color;
  }
  public void assignDriver(String driverName) { // extrinsic state
    System.out.println("Assigning driver " + driverName + " to " + color + " car");
  }
  public void move() {
    System.out.println(color + " car is moving");
  }
}

// FlyweightFactory
class VehicleFactory {

  private Map<String, Vehicle> vehicles = new HashMap<>();

  public Vehicle getVehicle(String color) {
    Vehicle vehicle = vehicles.get(color);
    if (vehicle == null) {
      vehicle = new Car(color);
      vehicles.put(color, vehicle);
      System.out.println("Creating a " + color + " car");
    }
    return vehicle;
  }
}

public class Main {
  public static void main(String[] args) {

    VehicleFactory vehicleFactory = new VehicleFactory();
    Vehicle vehicle1 = vehicleFactory.getVehicle("red");
    vehicle1.assignDriver("John");
    vehicle1.move();

    Vehicle vehicle2 = vehicleFactory.getVehicle("blue");
    vehicle2.assignDriver("Jane");
    vehicle2.move();

    Vehicle vehicle3 = vehicleFactory.getVehicle("red"); // reuses existing red car
    vehicle3.assignDriver("Rick");
    vehicle3.move();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Proxy -- structural design pattern that provides an object that acts as a substitute for a real service object used by a client. A proxy receives client requests, does some work (access control, caching, etc.) and then passes the request to a service object.
When to use the Proxy pattern:
	1.	When we want a simplified version of a complex or heavy object. In this case, we may represent it with a skeleton object which loads the original object on demand, also called as lazy initialization. This is known as the Virtual Proxy
	2.	When the original object is present in different address space, and we want to represent it locally. We can create a proxy which does all the necessary boilerplate stuff like creating and maintaining the connection, encoding, decoding, etc., while the client accesses it as it was present in their local address space. This is called the Remote Proxy
	3.	When we want to add a layer of security to the original underlying object to provide controlled access based on access rights of the client. This is called Protection Proxy

```java
// Subject
interface Vehicle {
  void drive();
}

// RealSubject
class Car implements Vehicle {
  public void drive() {
    System.out.println("Car is being driven");
  }
}

// Proxy
class CarProxy implements Vehicle {
  private Car car;
  private String driverLicense;
  public CarProxy(String driverLicense) {
    this.driverLicense = driverLicense;
    this.car = new Car();
  }
  public void drive() {
    if (checkLicense()) {
      car.drive(); // delegates the call to the Car object.
    } else {
      System.out.println("Driver's license is not valid. Cannot drive the car.");
    }
  }
  private boolean checkLicense() {
    // Suppose valid license should start with "Valid"
    return driverLicense.startsWith("Valid");
  }
}

public class Main {
  public static void main(String[] args) {
    Vehicle car = new CarProxy("Valid123");
    car.drive(); // Car is being driven
    Vehicle car2 = new CarProxy("Invalid456");
    car2.drive(); // Driver's license is not valid. Cannot drive the car.
  }
}
```

------------------------------------------------------------------------------------------------------------------

Chain of Responsibility -- behavioral design pattern that lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
Usage -
	1.	Use the Chain of Responsibility pattern when your program is expected to process different kinds of requests in various ways, but the exact types of requests and their sequences are unknown beforehand.
	2.	Use the pattern when it’s essential to execute several handlers in a particular order.

```java
// Handler interface
interface VehicleInspector {
  void handle(VehicleCheck check);
  void setNext(VehicleInspector next);
}

// Concrete handler - Level 1 inspection
class Level1Inspector implements VehicleInspector {
  private VehicleInspector next;

  @Override
  public void handle(VehicleCheck check) {
    if (check.getDescription().equals("Level 1")) {
      System.out.println("Level 1 inspection performed");
    } else if (next != null) {
      next.handle(check);
    } else {
      System.out.println("No inspector available to handle this check");
    }
  }

  @Override
  public void setNext(VehicleInspector next) {
    this.next = next;
  }
}

// Concrete handler - Level 2 inspection
class Level2Inspector implements VehicleInspector {
  private VehicleInspector next;

  @Override
  public void handle(VehicleCheck check) {
    if (check.getDescription().equals("Level 2")) {
      System.out.println("Level 2 inspection performed");
    } else if (next != null) {
      next.handle(check);
    } else {
      System.out.println("No inspector available to handle this check");
    }
  }

  @Override
  public void setNext(VehicleInspector next) {
    this.next = next;
  }
}

// Concrete handler - Level 3 inspection
class Level3Inspector implements VehicleInspector {
  private VehicleInspector next;

  @Override
  public void handle(VehicleCheck check) {
    if (check.getDescription().equals("Level 3")) {
      System.out.println("Level 3 inspection performed");
    } else if (next != null) {
      next.handle(check);
    } else {
      System.out.println("No inspector available to handle this check");
    }
  }

  @Override
  public void setNext(VehicleInspector next) {
    this.next = next;
  }
}

// Request class
class VehicleCheck {
 private String description;
 public VehicleCheck(String description) {
  this.description = description;
 }
 public String getDescription() {
  return description;
 }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create inspectors
    VehicleInspector level1Inspector = new Level1Inspector();
    VehicleInspector level2Inspector = new Level2Inspector();
    VehicleInspector level3Inspector = new Level3Inspector();

    // Chain the inspectors
    level1Inspector.setNext(level2Inspector);
    level2Inspector.setNext(level3Inspector);

    // Perform checks
    VehicleCheck check = new VehicleCheck("Level 2");

    // Start the chain of responsibility
    level1Inspector.handle(check);
  }
}
```

------------------------------------------------------------------------------------------------------------------

Command -- Simply put, the pattern intends to encapsulate in an object all the data required for performing a given action (command), including what method to call, the method’s arguments, and the object to which the method belongs.
Process - In command pattern, the request is sent to the invoker and invoker pass it to the encapsulated command object. Command object passes the request to the appropriate method of Receiver to perform the specific action. (think of the implementation as multi-level composition). To remember the pattern, remember the word multi-level composition.
Example - Hotel. You go to hotel, waiter (invoker) comes to take the order (request) and creates a order note (command object). This order note is then sent to kitchen where it is first read by chef to prepare the food. Once coocked, the chef leaves it on shelf on a tray with the order note which is then taken up by another waiter to see if order note things are proper in the tray and then take it back to customer. 

```java
// Receiver interface
interface Vehicle {
  void start();
}

// Concrete receiver - Car
class Car implements Vehicle {
  @Override
  public void start() {
    System.out.println("Car started");
  }
}

// Command interface
interface Command {
  void execute();
}

// Concrete command - StartCommand
class StartCommand implements Command {
  private Vehicle vehicle;

  public StartCommand(Vehicle vehicle) {
    this.vehicle = vehicle;
  }

  @Override
  public void execute() {
    vehicle.start();
  }
}

// Invoker
class VehicleOperator {
  private Command command;

  public void setCommand(Command command) {
    this.command = command;
  }

  public void executeCommand() {
    command.execute();
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create receiver
    Vehicle car = new Car();

    // Create command
    Command startCarCommand = new StartCommand(car);

    // Create invoker
    VehicleOperator vehicleOperator = new VehicleOperator();
    vehicleOperator.setCommand(startCarCommand);

    // Execute command
    vehicleOperator.executeCommand();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Iterator -- behavioral design pattern that lets you traverse elements of an aggregate object without exposing its underlying representation (list, stack, tree, etc.).
Usage -
	1.	when your collection has a complex data structure under the hood, but you want to hide its complexity from clients
	2.	Use the pattern to reduce duplication of the traversal code across your app
	3.	when you want your code to be able to traverse different data structures or when types of these structures are unknown beforehand

```java
// Vehicle class
class Vehicle {
  private String name;

  public Vehicle(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }
}

// Custom Iterator interface
interface MyIterator<T> {
  boolean hasNext();
  T next();
}

// Concrete aggregate - VehicleList
class VehicleList {
  private List<Vehicle> vehicles;

  public VehicleList() {
    vehicles = new ArrayList<>();
  }

  public void addVehicle(Vehicle vehicle) {
    vehicles.add(vehicle);
  }

  public MyIterator<Vehicle> createIterator() {
    return new VehicleIterator();
  }

  // Nested class implementing Iterator<Vehicle>
  private class VehicleIterator implements MyIterator<Vehicle> {
    private int position = 0;

    @Override
    public boolean hasNext() {
      return position < vehicles.size();
    }

    @Override
    public Vehicle next() {
      if (hasNext()) {
        return vehicles.get(position++);
      }
      return null;
    }
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create a collection of vehicles
    VehicleList vehicleList = new VehicleList();
    vehicleList.addVehicle(new Vehicle("Car"));
    vehicleList.addVehicle(new Vehicle("Motorcycle"));

    // Create and use a custom iterator
    MyIterator<Vehicle> iterator = vehicleList.createIterator();
    while (iterator.hasNext()) {
      Vehicle vehicle = iterator.next();
      System.out.println("Vehicle: " + vehicle.getName());
    }
  }
}
```

------------------------------------------------------------------------------------------------------------------

Interpreter -- defines a grammatical representation for a language and provides an interpreter to interpret sentences in that language. It allows you to create a domain-specific language and interpret expressions written in that language. In essence, the Interpreter pattern involves defining a grammar for the language and implementing interpreters to evaluate expressions based on that grammar. This pattern is useful when you have a language that can be represented in a formal grammar and you want to interpret expressions in that language.
Usage -
	1.	When dealing with domain-specific languages
	2.	When you have a grammar to interpret
	3.	When adding new operations/commands is frequent

```java
// Abstract expression interface
interface Expression {
  int interpret();
}

// Terminal expression - Number
class NumberExpression implements Expression {
  private int number;

  public NumberExpression(int number) {
    this.number = number;
  }

  @Override
  public int interpret() {
    return number;
  }
}

// Non-terminal expression - Addition
class AdditionExpression implements Expression {
  private Expression left;
  private Expression right;

  public AdditionExpression(Expression left, Expression right) {
    this.left = left;
    this.right = right;
  }

  @Override
  public int interpret() {
    return left.interpret() + right.interpret();
  }
}

// Non-terminal expression - Subtraction
class SubtractionExpression implements Expression {
  private Expression left;
  private Expression right;

  public SubtractionExpression(Expression left, Expression right) {
    this.left = left;
    this.right = right;
  }

  @Override
  public int interpret() {
    return left.interpret() - right.interpret();
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create expressions
    Expression expression1 = new AdditionExpression(new NumberExpression(10), new NumberExpression(5));
    Expression expression2 = new SubtractionExpression(new NumberExpression(20), new NumberExpression(8));

    // Evaluate expressions
    System.out.println("Result of expression 1: " + expression1.interpret()); // Output: 15
    System.out.println("Result of expression 2: " + expression2.interpret()); // Output: 12
  }
}
```

------------------------------------------------------------------------------------------------------------------

Mediator -- lets you reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object. It defines an object, the mediator, to centralize communication between various components or objects in a system.
Usage -
	1.	Use the Mediator pattern when it’s hard to change some of the classes because they are tightly coupled to a bunch of other classes.
	2.	When you want a Centralized Control
	3.	if we have to deal with a set of objects that are tightly coupled (not too tightly though) and hard to maintain.

```java
// Mediator interface
interface TrafficPolice {
  void notify(Vehicle sender, String event);
}

// Component interface
abstract class Vehicle {
  protected TrafficPolice mediator;

  public Vehicle(TrafficPolice mediator) {
    this.mediator = mediator;
  }

  public abstract void send(String event);

  public abstract void receive(String event);
}

// Concrete component - Car
class Car extends Vehicle {
  public Car(TrafficPolice mediator) {
    super(mediator);
  }

  @Override
  public void send(String event) {
    mediator.notify(this, event);
  }

  @Override
  public void receive(String event) {
    System.out.println("Car received event: " + event);
  }

  public void start() {
    send("Start");
  }

  public void stop() {
    send("Stop");
  }
}

// Concrete mediator - TrafficPoliceMan
class TrafficPoliceMan implements TrafficPolice {
  private List<Vehicle> vehicles;

  public TrafficPoliceMan() {
    this.vehicles = new ArrayList<>();
  }

  public void registerVehicle(Vehicle vehicle) {
    vehicles.add(vehicle);
  }

  @Override
  public void notify(Vehicle sender, String event) {
    for (Vehicle vehicle : vehicles) {
      if (vehicle != sender) {
        vehicle.receive(event);
      }
    }
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create mediator
    TrafficPoliceMan trafficPoliceMan = new TrafficPoliceMan();

    // Create components and register them with mediator
    Car car1 = new Car(trafficPoliceMan);
    Car car2 = new Car(trafficPoliceMan);

    trafficPoliceMan.registerVehicle(car1);
    trafficPoliceMan.registerVehicle(car2);

    // Simulate vehicle operations
    car1.start();
    car2.stop();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Memento -- lets you save and restore the previous state of an object without revealing the details of its implementation. The Memento makes the object itself responsible for creating a snapshot of its state. No other object can read the snapshot, making the original object’s state data safe and secure.
Usage -
	1.	when you want to produce snapshots of the object’s state to be able to restore a previous state of the object
	2.	When you need to implement an undo feature in your application that allows users to revert changes made to an object’s state
	3.	When you need to rollback changes to an object’s state in case of errors or exceptions, such as in database transactions

```java
// Memento class
class VehicleMemento {
  private int speed;
  private double fuelLevel;
  private double mileage;

  public VehicleMemento(int speed, double fuelLevel, double mileage) {
    this.speed = speed;
    this.fuelLevel = fuelLevel;
    this.mileage = mileage;
  }

  public int getSpeed() {
    return speed;
  }

  public double getFuelLevel() {
    return fuelLevel;
  }

  public double getMileage() {
    return mileage;
  }
}

// Originator class - Vehicle
class Vehicle {
  private int speed;
  private double fuelLevel;
  private double mileage;

  public void setSpeed(int speed) {
    this.speed = speed;
  }

  public void setFuelLevel(double fuelLevel) {
    this.fuelLevel = fuelLevel;
  }

  public void setMileage(double mileage) {
    this.mileage = mileage;
  }

  public VehicleMemento saveState() {
    return new VehicleMemento(speed, fuelLevel, mileage);
  }

  public void restoreState(VehicleMemento memento) {
    this.speed = memento.getSpeed();
    this.fuelLevel = memento.getFuelLevel();
    this.mileage = memento.getMileage();
  }

  public void printState() {
    System.out.println("Speed: " + speed + " mph, Fuel Level: " + fuelLevel + " gallons, Mileage: " + mileage + " miles");
  }
}

// Caretaker class - VehicleCareTaker
class VehicleCareTaker {
    private List<VehicleMemento> mementoList =new ArrayList<>();

    public void addMemento(VehicleMemento memento) {
        mementoList.add(memento);
    }

    public VehicleMemento getMemento(int index) {
        return mementoList.get
(index);
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Create vehicle
        Vehicle vehicle = new Vehicle();
        vehicle.setSpeed(60);
        vehicle.setFuelLevel(10.5);
        vehicle.setMileage(2000.0);

        // Create caretaker
        VehicleCareTaker careTaker = new VehicleCareTaker();

        // Save initial state
        careTaker.addMemento(vehicle.saveState());
        System.out.println("Original state:");
        vehicle.printState();

        // Make changes
        vehicle.setSpeed(70);
        vehicle.setFuelLevel(9.5);
        vehicle.setMileage(2100.0);
        System.out.println("\nModified state:");
        vehicle.printState();

        // Save modified state
        careTaker.addMemento(vehicle.saveState());

        // Restore initial state
        vehicle.restoreState(careTaker.getMemento(0));
        System.out.println("\nRestored to original state:");
        vehicle.printState();

        // Restore modified state
        vehicle.restoreState(careTaker.getMemento(1));
        System.out.println("\nRestored to modified state:");
  
      vehicle.printState();
    }
}
```

------------------------------------------------------------------------------------------------------------------

Observer (Pub-Sub) -- lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing. It defines a one-to-many dependency between objects so that when one object (the subject) changes state, all its dependents (observers) are notified and updated automatically.
Usage --
	1.	when some objects in your app must observe others, but only for a limited time or in specific cases
	2.	often used in event handling systems

```java
// Subscriber interface
interface MailSubscriber {
  void receiveMail(String message);
}

// Concrete subscriber - UserMailbox
class UserMailbox implements MailSubscriber {
  private String email;

  public UserMailbox(String email) {
    this.email = email;
  }

  @Override
  public void receiveMail(String message) {
    System.out.println("Mail received by " + email + ": " + message);
  }
}

// Subject interface
interface MailPublisher {
    void addSubscriber(MailSubscriber subscriber);
    void removeSubscriber(MailSubscriber subscriber);
    void notifySubscribers(String message);
}

// Concrete subject - NewsletterPublisher
class NewsletterPublisher implements MailPublisher {
    private List<MailSubscriber> subscribers = new ArrayList<>();

    @Override
    public void addSubscriber(MailSubscriber subscriber) {
        subscribers.add(subscriber);
    }

    @Override
    public void removeSubscriber(MailSubscriber subscriber) {
        subscribers.remove(subscriber);
    }

    @Override
    public void notifySubscribers(String message) {
        for (MailSubscriber subscriber : subscribers) {
            subscriber.receiveMail(message);
        }
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Create newsletter publisher
        NewsletterPublisher publisher = new NewsletterPublisher();

        // Create mail subscribers
        MailSubscriber subscriber1 = new UserMailbox("user1@example.com");
        MailSubscriber subscriber2 = new UserMailbox("user2@example.com");

        // Register subscribers
        publisher.addSubscriber(subscriber1);
        publisher.addSubscriber(subscriber2);

        // Notify subscribers
      
        publisher.notifySubscribers("Check out our latest offers!");
    }
}
```

------------------------------------------------------------------------------------------------------------------

State -- lets an object alter its behavior when its internal state changes. It appears as if the object changed its class. It achieves this by encapsulating the object’s behavior within different state objects, and the object itself dynamically switches between these state objects depending on its current state.
Usage -
1. If your object exists in several states (e.g., On/Off, Open/Closed, Started/Stopped), and each state dictates unique behaviors, the State pattern can encapsulate this logic effectively.
2. When conditional statements (if-else or switch-case) become extensive and complex within your object, the State pattern helps organize and separate state-specific behavior into individual classes
3. If your object transitions between states frequently

```java
// Context class - Vehicle
class Vehicle {
    private State state;

    public Vehicle() {
        // Initial state is stopped
        this.state = new StoppedState();
    }

    public void setState(State state) {
        this.state = state;
    }

    public void start() {
        state.start(this);
    }

    public void stop() {
        state.stop(this);
    }
}

// State interface
interface State {
    void start(Vehicle vehicle);
    void stop(Vehicle vehicle);
}

// Concrete state - StoppedState
class StoppedState implements State {
    @Override
    public void start(Vehicle vehicle) {
        System.out.println("Starting the vehicle...");
        vehicle.setState(new RunningState());
    }

    @Override
    public void stop(Vehicle vehicle) {
        System.out.println("Vehicle is already stopped.");
    }
}

// Concrete state - RunningState
class RunningState implements State {
    @Override
    public void start(Vehicle vehicle) {
        System.out.println("Vehicle is already running.");
    }

    @Override
    public void stop(Vehicle vehicle) {
        System.out.println("Stopping the vehicle...");
        vehicle.setState(new StoppedState());
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Create a vehicle
        Vehicle vehicle = new Vehicle();

        // Perform actions on the vehicle
        vehicle.start(); // Output: Starting the vehicle...
        vehicle.stop();  // Output: Stopping the vehicle...
        vehicle.stop();  // Output: Vehicle is already stopped.
 
       vehicle.start(); // Output: Starting the vehicle...
    }
}
```

------------------------------------------------------------------------------------------------------------------

Strategy -- lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable. It defines a family of algorithms, encapsulates each one, and makes them interchangeable, allowing clients to switch algorithms dynamically without altering the code structure.
Usage -
1. when you want to use different variants of an algorithm within an object.
2. When you need to dynamically select and switch between different algorithms at runtime based on user preferences

```java
// Strategy interface
interface SortingStrategy {
  void sort(int[] arr);
}

// Concrete strategy - BubbleSort
class BubbleSort implements SortingStrategy {
  @Override
  public void sort(int[] arr) {
    System.out.println("Sorting array using Bubble Sort");
    // Implementation of bubble sort algorithm
  }
}

// Concrete strategy - QuickSort
class QuickSort implements SortingStrategy {
  @Override
  public void sort(int[] arr) {
    System.out.println("Sorting array using Quick Sort");
    // Implementation of quick sort algorithm
  }
}

// Context class - Sorter
class Sorter {
  private SortingStrategy strategy;

  public Sorter(SortingStrategy strategy) {
    this.strategy = strategy;
  }

  public void setStrategy(SortingStrategy strategy) {
    this.strategy = strategy;
  }

  public void performSort(int[] arr) {
    strategy.sort(arr);
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create a context with BubbleSort strategy
    Sorter sorter = new Sorter(new BubbleSort());

    // Array to be sorted
    int[] arr = {5, 3, 9, 1, 7};

    // Perform sorting using BubbleSort
    sorter.performSort(arr);

    // Change the sorting strategy to QuickSort
    sorter.setStrategy(new QuickSort());

    // Perform sorting using QuickSort
    sorter.performSort(arr);
  }
}
```

------------------------------------------------------------------------------------------------------------------

Template Method -- defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. It It promotes code reuse by encapsulating the common algorithmic structure in the superclass while allowing subclasses to provide concrete implementations for certain steps, thus enabling customization and flexibility.
Usage -
1. when you want to let clients extend only particular steps of an algorithm, but not the whole algorithm or its structure.
2. when you have several classes that contain almost identical algorithms with some minor differences. 

```java
// Abstract class defining the template method
abstract class Vehicle {
  // Template method defining the algorithm for building a vehicle
  public final void assembleVehicle() {
    buildWheels();
    installEngine();
    addBody();
    System.out.println("Vehicle assembly completed.");
    // return new Vehicle(with all components);
  }

  // Abstract methods to be implemented by subclasses
  protected abstract void buildWheels();
  protected abstract void installEngine();
  protected abstract void addBody();
}

// Concrete subclass implementing the template methods for a car
class Car extends Vehicle {
  @Override
  protected void buildWheels() {
    System.out.println("Building wheels for the car");
  }

  @Override
  protected void installEngine() {
    System.out.println("Installing engine for the car");
  }

  @Override
  protected void addBody() {
    System.out.println("Adding body to the car");
  }
}

// Concrete subclass implementing the template methods for a bike
class Bike extends Vehicle {
  @Override
  protected void buildWheels() {
    System.out.println("Building wheels for the bike");
  }

  @Override
  protected void installEngine() {
    System.out.println("Bikes don't have engines to install");
  }

  @Override
  protected void addBody() {
    System.out.println("Adding body to the bike");
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Assemble a car
    Vehicle car = new Car();
    car.assembleVehicle();

    System.out.println();

    // Assemble a bike
    Vehicle bike = new Bike();
    bike.assembleVehicle();
  }
}
```

------------------------------------------------------------------------------------------------------------------

Visitor -- lets you separate algorithms from the objects on which they operate. It is used when we have to perform an operation on a group of similar kind of Objects. With the help of visitor pattern, we can move the operational logic from the objects to another class.
Usage -
1. when you need to perform an operation on all elements of a complex object structure.

```java
// Element interface
interface VehiclePart {
  void accept(ShoppingVisitor visitor);
}

// Concrete element - Engine
class Engine implements VehiclePart {
  @Override
  public void accept(ShoppingVisitor visitor) {
    visitor.visit(this);
  }
}

// Concrete element - Body
class Body implements VehiclePart {
  @Override
  public void accept(ShoppingVisitor visitor) {
    visitor.visit(this);
  }
}

// Visitor interface
interface ShoppingVisitor {
  void visit(Engine engine);
  void visit(Body body);
}

// Concrete visitor implementation
class ShoppingVisitorImpl implements ShoppingVisitor {
  private double totalPrice = 0;

  @Override
  public void visit(Engine engine) {
    totalPrice += 5000; // Assume engine price
  }

  @Override
  public void visit(Body body) {
    totalPrice += 10000; // Assume body price
  }

  public double getTotalPrice() {
    return totalPrice;
  }
}

// Client code
public class Main {
  public static void main(String[] args) {
    // Create vehicle parts
    VehiclePart engine = new Engine();
    VehiclePart body = new Body();

    // Create visitor
    ShoppingVisitor shoppingVisitor = new ShoppingVisitorImpl();

    // Accept visitor
    engine.accept(shoppingVisitor);
    body.accept(shoppingVisitor);

    // Get total price
    double totalPrice = ((ShoppingVisitorImpl) shoppingVisitor).getTotalPrice();
    System.out.println("Total price of vehicle parts: $" + totalPrice);
  }
}
```
