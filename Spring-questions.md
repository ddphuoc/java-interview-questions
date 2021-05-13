# Spring and Springboot Interview Questions and Answers


## Q. Bean scope in Spring?

**1. Singleton**  

* The container creates a single instance of bean;
* All requests for that bean name will return the same object, which is cached;
* Any modifications to the object will be reflected in all references to the bean;
* This scope is the default value of bean.

```java
@Bean
@Scope("singleton") //@Scope(value = ConfigurableBeanFactory.SCOPE_SINGLETON)
public Person personSingleton() {
    return new Person();
}
```

**2. Prototype**  

A bean with the prototype scope will return a different instance every time it is requested from the container

```java
@Bean
@Scope("prototype")
public Person personPrototype() {
    return new Person();
}
```
**3. Request**  

The request scope creates a bean instance for a single HTTP request.

```java
@Bean
@RequestScope
//@Scope(value = WebApplicationContext.SCOPE_REQUEST, proxyMode = ScopedProxyMode.TARGET_CLASS)
public HelloMessageGenerator requestScopedBean() {
    return new HelloMessageGenerator();
}
```
The **proxyMode** attribute is Spring creates a proxy to be injected as a dependency, and instantiates the target bean when it is needed in a request

**4. Session**  

The session scope creates a bean instance for an HTTP Session.

```java
@Bean
@SessionScope
//@Scope(value = WebApplicationContext.SCOPE_SESSION, proxyMode = ScopedProxyMode.TARGET_CLASS)
public HelloMessageGenerator sessionScopedBean() {
    return new HelloMessageGenerator();
}
```
The **proxyMode** attribute is Spring creates a proxy to be injected as a dependency, and instantiates the target bean when it is needed in a request

**5. Application**  

The application scope creates the bean instance for the lifecycle of a ServletContext.
```java
@Bean
@ApplicationScope
//@Scope(value = WebApplicationContext.SCOPE_APPLICATION, proxyMode = ScopedProxyMode.TARGET_CLASS)
public HelloMessageGenerator applicationScopedBean() {
    return new HelloMessageGenerator();
}
```
The **proxyMode** attribute is Spring creates a proxy to be injected as a dependency, and instantiates the target bean when it is needed in a request

**6. Websocket**  

The websocket scope creates it for a particular WebSocket session.
```java
@Bean
@Scope(scopeName = "websocket", proxyMode = ScopedProxyMode.TARGET_CLASS)
public HelloMessageGenerator websocketScopedBean() {
    return new HelloMessageGenerator();
}
```
The **proxyMode** attribute is Spring creates a proxy to be injected as a dependency, and instantiates the target bean when it is needed in a request

* When first accessed, WebSocket scoped beans are stored in the WebSocket session attributes.
* The same instance of the bean is then returned whenever that bean is accessed during the entire WebSocket session.
* We can also say that it exhibits singleton behavior, but limited to a WebSocket session only

##Q. What is Spring Boot?
Spring Boot provides a platform to develop a stand-alone and production-grade spring application. You can get started with minimum configurations without the need for an entire Spring configuration setup.

##Q. Advantages of Spring Boot?

* Easy to understand and develop spring applications, avoid complex XML configuration in Spring
* Increases productivity, develop a Spring applications in an easier way
* Reduces the development time
* Offer an easier way of getting started with the application

##Q. Different between @Controller and @RestController

* @RestController is combine @Controller and @ResponseBody
* @Controller need @ResponseBody

##Q. Bean lifecycle?

* Container create bean per request
* Bean destroy when container is closed

##Q. Dependency injection and working?

* We describe how to create objects
* Inversion of Control (IoC) container will instantiate required classes when needed

###The ways to injects bean
* Setter injection
* Constructor injection
* Field injection

##Q. Inversion of Control and working?
Wiring dependencies of various objects

##Q. Different ApplicationContext and BeanFactory
* **BeanFactory** provides and manage bean instance.
* **ApplicationContext** holding information, metadata and beans in application. It also extends **BeanFactory**