# Annotations

## General

* @Required
  * applied to bean setter methods
  * indicates that the affected bean must be populated at configuration time, otherwise a BeanInitializationException will be thrown
* @Autowired
  * applied to fields, setters and constructors
  * injects a dependency
  * using it on private fields is a poor practice
  * when used on setter methods, Spring tries to perform injection by type
  * with Spring 4.3+, @Autowired is optional if there's a single constructor
* @Qualifier
  * help Spring determine what to inject when there are multiple possibilities
* @Configuration
  * alternative to XML configuration
* @ComponentScan
  * allows Spring to know the packages to scan for annotated components
  * basePackageClasses or basePackage attributes
* @Bean
  * works with @Configuration
* @Lazy
  * only create and initialize upon first request
* @Value
  * supports \#{...} and ${...}

## Stereotype

* @Component
  * marks the class as a bean or component so that the component-scanning can add it to the application context
* @Controller
  * identify controllers for MVC or WebFlux
* @Service
  * marks a class as a service
* @Repository
  * for DAOs
  * has an automatic translation feature
    * e.g., when an exception occurs in the @Repository there's a handler for that exception and there's no need for a try-catch block

## Spring Boot

* @EnableAutoConfiguration
  * define a base "search package"; tells Spring Boot to start adding beans based on classpath settings, other beans and property settings
* @SpringBootApplication
  * class annotated with this should be in the base package
  * does a component scan but only scans sub-packages
  * adds the following
    * @Configuration
    * @EnableAutoConfiguration
    * @ComponentScan

## Spring MVC and REST

* @Controller
  * allows autodetection of component classes in the classpath and auto-registering bean definitions for them
  * can handle multiple request mappings
  * can also be used with WebFlux
* @RequestMapping
  * used at class and method level
  * used to map Web requests to specific handler classes/methods
  * at class level: base path
* @CookieValue
  * used at method parameter level
  * used as an argument of a request mapping method
  * ...@CookieValue\("JSESSIONID"\)  String sessionCookie\) { ... }
* @CrossOrigin
  * used at class and method levels
  * enable CORS
* @Get\|Post\|Put\|Patch\|DeleteMapping
  * method-level variant of @RequestMapping
  * acts as wrapper for @RequestMapping
  * can be used with MVC and WebFlux
  * = @RequestMapping\(method= RequestMethod.GET\|POST\|PUT\|PATCH\|DELETE\)
* @PostMapping
  * method-level variant of @RequestMapping
  * acts as wrapper for @RequestMapping
  * can be used with MVC and WebFlux
  * = @RequestMapping\(method= RequestMethod.POST\)
* @ExceptionHandler
  * handle exceptions at the controller level
  * used to define the class of exception it will catch
  * use on methods that should be invoked to handle some exception type\(s\)

* @InitBinder
  * method-level
  * identifies methods that initialize the WebDataBinder -- a DataBinder that binds the request parameter to JavaBean objects
* @Mappings and @Mapping
  * used on fields
* @MatrixVariable
  * used to annotate request handler method arguments so that Spring can inject the relevant bits of a matrix URI
* @PathVariable
  * handle dynamic changes in the URI where a certain URI value acts as a parameter
  * can be specified using a regex
* @RequestAttribute
  * bind the request attribute to a handler method parameter
* @RequestBody
  * annotate request handler method arguments
  * indicates that a method parameter should be bound to the value of the HTTP request body
  * HttpMessageConverter is responsible for converting from the HTTP request message to object
* @RequestHeader
  * map controller parameter to request header value
* @RequestParam
  * along with @RequestMapping to retrieve URL parameters and map them to the method arguments
* @RequestPart
  * can be used instead of @RequestParam to get the contents of a specific multipart and bind it to the method argument
  * takes the Content-Type into consideration
* @ResponseBody
  * similar to @RequestBody
  * indicates that the result type should be written straight in the response body in whatever format you specify
* @ResponseStatus
  * used on methods and exception classes
  * marks a method or exception class with a status code and a reason that must be returned
  * overrides the status information provided by any other means
  * can also be put on a controller class \(then inherited by all @RequestMapping methods
* @ControllerAdvice
  * used at class level
  * base issue: @ExceptionHandler annotated methods are _only_ called for exceptions thrown within the controller in which it is defined
  * with @ControllerAdvice you can define @ExceptionHandler, @InitBinder, @ModelAttribute methods that apply to _all_ @RequestMapping methods
* @RestControllerAdvice
  * used at class level
  * combines @ControllerAdvice and @ResponseBody
  * used along with the @ExceptionHandler annotation to handle exceptions that occur within the controller
* @SessionAttribute
  * used at method parameter level
  * bind the method parameter to a session attribute
* @SessionAttributes
  * used at class level for a specific handler
  * used when you want to add a JavaBean object into a session
  * used when you want to keep the object in session for a short duration
  * used in conjunction with @ModelAttribute

## Spring Cloud

* @EnableConfigServer
  * used at class level
  * centralized manner to configure and retrieve the configurations of all the services
  * starts a config server that the other applications can talk to
* @EnableEurekaServer
  * Netflix's Eureka: discovery server
  * easy integration in Spring thanks to Spring Boot
* @EnableDiscoveryClient
  * used at class level
  * tells any application to register itself with Eureka
  * added to the application entry point
* @EnableCircuitBreaker
  * used at class level
  * allows a microservice to continue working when a related service fails, preventing the failure from cascading
  * also gives the failed service time to recover
  * the class annotated with this will monitor, open and close the circuit breaker
* @HystrixCommand
  * used at method level
  * Netflix's Hystrix library provides an implementation of the Circuit Breaker pattern
  * when applied to a method, Hystrix watches for the failure of the method
  * once failures build up to a threshold, Hystrix opens the circuit so that the subsequent calls also fail
  * then Hystrix redirects calls to the method and they are passed to the specified fallback methods
  * Hystrix looks for any method annotated with the @HystrixCommand annotation and watches it

## Data Access

* @Transactional
  * placed before an interface definition, a method on an interface, a class or a public method of a class
  * does not by itself enable transactional behavior
  * simply metadata that can be consumed by some runtime infrastructure
  * allows configuration like
    * the propagation type of the transaction
    * the isolation level of the transaction
    * a timeout
    * a read-only flag: hint for the persistence provider that the transaction must be read-only
    * rollback rules for the transaction

## Caching

* @Cacheable
  * used on methods
  * specifies the name of the cache where results of the method call should be stored
* @CachePut
  * used on methods
  * whenever you need to update the cache without interfering the method exectution
  * the method will always be executed and the result cached
* @CacheEvict
  * used on methods
  * remove cached data
* @CacheConfig
  * used at class level
  * helps streamline some of the cache information in one place
  * allows you to store the cache configuration at the class level to only declare it once

## Task execution and scheduling

* @Scheduled
  * used at method level
  * provided with the trigger metadata
  * annotated methods should have a void return type and should not accept parameters
  * can define a fixedDelay, a fixedRate, and initialDelay, ...
* @Async
  * used at method level
  * execute  in a separate thread \(asynchronously\)
  * annotated methods can take arguments
  * can be used on void return type methods and methods that return a value
    * if there is a return value, it should be Future-typed

## Testing

* @BootstrapWith
  * used at class level
  * used to configure how the Spring TestContext Framework is bootstrapped
  * used as metadata to create custom composed annotations and reduce the configuration duplication in a test suite
* @ContextConfiguration
  * used at class levels
  * indicates which configuration files to load to initialize the application context for the test
* @WebAppConfiguration
  * used at class level
  * used to declare that the application context loaded for an integration test should be a WebApplicationContext
  * must be used with the @ContextConfiguration annotation
  * the default path for the root of the web application is src/main/webapp
    * you can override it by passing a different path
* @Timed
  * used at method level
  * indicates that the annotated test method must finish its execution within a specific time frame
* @Repeat
  * used at method level
  * run a test method several times in a row automatically
* @Commit
  * used at class or method level
  * after the execution of a test, the transaction can be committed using @Commit
  * explicitly conveys the intent of the code
  * when used at class level, it defines the commit for all test methods
* @Rollback
  * ...
* @DirtiesContext
  * used at class or method level
  * indicates that the Spring application context has been modified or corrupted in some manner and should be closed
  * triggers the context reloading before executing the next test
* @BeforeTransaction
  * annotate void methods in the test class
  * methods annotated with this should be executed before any transaction starts executing
* @AfterTransaction
  * ...
* @Sql
  * used at class or method level
  * runs SQL scripts against a database
  * configures the resource path to SQL scripts that should be executed before or after an integration test method
* @SqlConfig
  * used along with @Sql
  * defines the metadata used to determine how to parse and execute SQL scripts configured via @Sql
* @SqlGroup
  * used at method level
  * container annotation that can hold multiple @Sql annotations
* @SpringBootTest
  * start the Spring context for integration tests
  * will bring up the full auto-configuration context \(with either a fake or a real container\)
* @DataJpaTest
  * provides auto



