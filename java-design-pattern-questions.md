# Java Design Pattern Questions and Answers
##Q. What are Design Patterns?
Solutions to general problems that developers faced in software development

##Q. Types of design pattern?
* **Creational**: Provide a way to create objects while hiding the creation logic
* **Structural**: Compose interfaces and define ways to compose objects to obtain functionalities
* **Behavioral**: Focus on communication between objects

## Q. Exaplain MVC, Front-Controller, DAO, DTO, Service-Locator, Prototype design patterns?

**2. Front-Controller**

The front controller design pattern is used to provide a centralized request handling mechanism so that all requests will be handled by a single handler. This handler can do the authentication/ authorization/ logging or tracking of request and then pass the requests to corresponding handlers. Following are the entities of this type of design pattern.

* Front Controller - Single handler for all kinds of requests coming to the application (either web based/ desktop based).

* Dispatcher - Front Controller may use a dispatcher object which can dispatch the request to corresponding specific handler.

* View - Views are the object for which the requests are made.

*Example:*

We are going to create a `FrontController` and `Dispatcher` to act as Front Controller and Dispatcher correspondingly. `HomeView` and `StudentView` represent various views for which requests can come to front controller.

FrontControllerPatternDemo, our demo class, will use FrontController to demonstrate Front Controller Design Pattern.

Step 1
Create Views.

*HomeView.java*
```java
public class HomeView {
   public void show(){
      System.out.println("Displaying Home Page");
   }
}
```
*StudentView.java*
```java
public class StudentView {
   public void show(){
      System.out.println("Displaying Student Page");
   }
}
```

Step2
Create Dispatcher.

*Dispatcher.java*
```java
public class Dispatcher {
   private StudentView studentView;
   private HomeView homeView;
   
   public Dispatcher(){
      studentView = new StudentView();
      homeView = new HomeView();
   }

   public void dispatch(String request){
      if(request.equalsIgnoreCase("STUDENT")){
         studentView.show();
      }
      else{
         homeView.show();
      }	
   }
}
```

Step3
Create FrontController.

*FrontController.java*
```java
public class FrontController {
	
   private Dispatcher dispatcher;

   public FrontController(){
      dispatcher = new Dispatcher();
   }

   private boolean isAuthenticUser(){
      System.out.println("User is authenticated successfully.");
      return true;
   }

   private void trackRequest(String request){
      System.out.println("Page requested: " + request);
   }

   public void dispatchRequest(String request){
      //log each request
      trackRequest(request);

      //authenticate the user
      if(isAuthenticUser()){
         dispatcher.dispatch(request);
      }
   }
}
```

Step4
Use the FrontController to demonstrate Front Controller Design Pattern.

*FrontControllerPatternDemo.java*
```java
public class FrontControllerPatternDemo {
   public static void main(String[] args) {
   
      FrontController frontController = new FrontController();
      frontController.dispatchRequest("HOME");
      frontController.dispatchRequest("STUDENT");
   }
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What are the design patterns available in Java?

Java Design Patterns are divided into three categories – creational, structural, and behavioral design patterns.

**1. Creational Design Patterns**

* Singleton Pattern
* Factory Pattern
* Abstract Factory Pattern
* Builder Pattern
* Prototype Pattern

**2. Structural Design Patterns**

* Adapter Pattern
* Composite Pattern
* Proxy Pattern
* Flyweight Pattern
* Facade Pattern
* Bridge Pattern
* Decorator Pattern

**3. Behavioral Design Patterns**

* Template Method Pattern
* Mediator Pattern
* Chain of Responsibility Pattern
* Observer Pattern
* Strategy Pattern
* Command Pattern
* State Pattern
* Visitor Pattern
* Interpreter Pattern
* Iterator Pattern
* Memento Pattern

**4. Miscellaneous Design Patterns**

* DAO Design Pattern
* Dependency Injection Pattern
* MVC Pattern

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain Singleton Design Pattern in Java?

Create an object while making sure only single object was created 

**Eg. Thread Safe Singleton**  
The easier way to create a thread-safe singleton class is to make the global access method synchronized, so that only one thread can execute this method at a time.

Example:
```java
public class ThreadSafeSingleton {

    private volatile static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static ThreadSafeSingleton getInstance() {
        if(instance == null){
            synchronized(this) {
                if(instance == null) {
                    instance = new ThreadSafeSingleton();
                }
            }
        }
        return instance;
    }
}
```


<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain Adapter Design Pattern in Java?

This pattern involves a single class to join functions of independent interfaces 

**Example**:

we have two incompatible interfaces: **MediaPlayer** and **MediaPackage**. So, we need to create an adapter to help to work with two incompatible interfaces.

MediaPlayer.java
```java
public interface MediaPlayer {
    void play(String filename);
}
```

MediaPackage.java
```java
public interface MediaPackage {
    void playFile(String filename);
}
```

FormatAdapter.java
```java
public class FormatAdapter implements MediaPlayer {
    private MediaPackage media;
    public FormatAdapter(MediaPackage m) {
        media = m;
    }
    @Override
    public void play(String filename) {
        System.out.print("Using Adapter --> ");
        media.playFile(filename);
    }
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain Factory Design Pattern in Java?

A Factory Pattern or Factory Method Pattern just define an interface or abstract class 
and the subclasses are responsible to create the instance of the class.

Example: Calculate Electricity Bill
Plan.java

```java
import java.io.*;      
abstract class Plan {  
    protected double rate;  
    abstract void getRate();  

    public void calculateBill(int units){  
        System.out.println(units*rate);  
    }  
}  
```

DomesticPlan.java
```java
class  DomesticPlan extends Plan{  
    @override  
    public void getRate(){  
        rate=3.50;              
    }  
}
```

CommercialPlan.java
```java
class  CommercialPlan extends Plan{  
    @override   
    public void getRate(){   
        rate=7.50;  
    }   
}  
```

InstitutionalPlan.java
```java
class  InstitutionalPlan extends Plan{  
    @override  
    public void getRate(){   
        rate=5.50;  
   }   
} 
```

GetPlanFactory.java
```java
class GetPlanFactory {  
      
    // use getPlan method to get object of type Plan   
    public Plan getPlan(String planType){  
        if(planType == null){  
            return null;  
        }  
        if(planType.equalsIgnoreCase("DOMESTICPLAN")) {  
                return new DomesticPlan();  
            }   
        else if(planType.equalsIgnoreCase("COMMERCIALPLAN")){  
            return new CommercialPlan();  
        }   
        else if(planType.equalsIgnoreCase("INSTITUTIONALPLAN")) {  
            return new InstitutionalPlan();  
        }  
         return null;  
    }  
} 
```

GenerateBill.java
```java
import java.io.*;    
class GenerateBill {

    public static void main(String args[])throws IOException {  
      GetPlanFactory planFactory = new GetPlanFactory();  
        
      System.out.print("Enter the name of plan for which the bill will be generated: ");  
      BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
      String planName=br.readLine();  
      System.out.print("Enter the number of units for bill will be calculated: ");  
      int units=Integer.parseInt(br.readLine());  
  
      Plan p = planFactory.getPlan(planName);  
      // call getRate() method and calculateBill()method of DomesticPaln.  
  
       System.out.print("Bill amount for "+planName+" of  "+units+" units is: ");  
           p.getRate();  
           p.calculateBill(units);  
    }  
} 
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain Strategy Design Pattern in Java?

Strategy design pattern is one of the behavioral design pattern. Strategy pattern is used when we have multiple algorithm for a specific task and client decides the actual implementation to be used at runtime.

Example: Simple Shopping Cart where we have two payment strategies – using Credit Card or using PayPal.

PaymentStrategy.java
```java
public interface PaymentStrategy {
	public void pay(int amount);
}
```

CreditCardStrategy.java
```java
public class CreditCardStrategy implements PaymentStrategy {

	private String name;
	private String cardNumber;
	private String cvv;
	private String dateOfExpiry;
	
	public CreditCardStrategy(String nm, String ccNum, String cvv, String expiryDate){
		this.name=nm;
		this.cardNumber=ccNum;
		this.cvv=cvv;
		this.dateOfExpiry=expiryDate;
	}
	@Override
	public void pay(int amount) {
		System.out.println(amount +" paid with credit/debit card");
	}
}
```

PaypalStrategy.java
```java
public class PaypalStrategy implements PaymentStrategy {

	private String emailId;
	private String password;
	
	public PaypalStrategy(String email, String pwd){
		this.emailId=email;
		this.password=pwd;
	}
	@Override
	public void pay(int amount) {
		System.out.println(amount + " paid using Paypal.");
	}
}
```

Item.java
```java
public class Item {

	private String upcCode;
	private int price;
	
	public Item(String upc, int cost){
		this.upcCode=upc;
		this.price=cost;
	}
	public String getUpcCode() {
		return upcCode;
	}
	public int getPrice() {
		return price;
	}
}
```

ShoppingCart.java
```java
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {

	List<Item> items;
	
	public ShoppingCart(){
		this.items=new ArrayList<Item>();
	}
	public void addItem(Item item){
		this.items.add(item);
	}
	public void removeItem(Item item){
		this.items.remove(item);
	}
	public int calculateTotal(){
		int sum = 0;
		for(Item item : items){
			sum += item.getPrice();
		}
		return sum;
	}
	public void pay(PaymentStrategy paymentMethod){
		int amount = calculateTotal();
		paymentMethod.pay(amount);
	}
}
```

ShoppingCartTest.java
```java
public class ShoppingCartTest {

	public static void main(String[] args) {
		ShoppingCart cart = new ShoppingCart();
		
		Item item1 = new Item("1234",10);
		Item item2 = new Item("5678",40);
		
		cart.addItem(item1);
		cart.addItem(item2);
		
		// pay by paypal
		cart.pay(new PaypalStrategy("myemail@example.com", "mypwd"));
		
		// pay by credit card
		cart.pay(new CreditCardStrategy("Pankaj Kumar", "1234567890123456", "786", "12/15"));
	}
}
```
Output 
```
500 paid using Paypal.
500 paid with credit/debit card
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

#### Q. When do you use Flyweight pattern?
#### Q. What is difference between dependency injection and factory design pattern?
#### Q. Difference between Adapter and Decorator pattern?
#### Q. Difference between Adapter and Proxy Pattern?
#### Q. What is Template method pattern?
#### Q. When do you use Visitor design pattern?
#### Q. When do you use Composite design pattern?
#### Q. Difference between Abstract factory and Prototype design pattern?

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

##Q. What is Facade pattern?
* Facade encapsulates a complex subsystem behind a simple interface.
* It decouples a client implementation from the complex subsystem.
* Instead of calling multiple methods in concrete class, facade encapsulate these methods in one method and share simple methods

**Eg.**
```java
class FacadeClass {
    private Class1 class1 = new Class1();
    private Class2 class2 = new Class2();
    private Class3 class3 = new Class3();
    public void callMethods() { //Encapsulates complex subsystem's methods
        class1.method();
        class2.method();
        class3.method();
    }
}
```