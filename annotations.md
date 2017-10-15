# Annotations

## General

* @Required
* @Autowired
* @Qualifier
* @Configuration
* @ComponentScan
* @Bean
* @Lazy
  * only create and initialize upon first request
* @Value
  * supports \#{...} and ${...}
* @Component
* @Controller
* @Service
* @Repository

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
* @RequestMapping
* @CookieValue
  * used at method parameter level
  * used as an argument of a request mapping method
  * ...@CookieValue\("JSESSIONID"\)  String sessionCookie\) { ... }
* @CrossOrigin
  * used at class and method levels
  * enable CORS
* @GetMapping
* @PostMapping
* @PutMapping
* @PatchMapping
* @DeleteMapping
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
* @RequestAttribute
  * bind the request attribute to a handler method parameter



