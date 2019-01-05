# Tiny Url Service
Tiny Url web application with Java and Spring Boot.


To run it using maven (http://maven.apache.org):
```sh
$ mvn spring-boot:run
```

Then navigate to http://localhost:8080/ in your browser.

## Components

### [YourlApplication.java]
This is the main class of the application that initializes the Spring context including all the Spring components in this project and starts the web application inside an embedded Apache Tomcat (http://tomcat.apache.org) web container.

### [UrlController.java]
This class serves as the Controller that processes HTTP requests. HTTP endpoints defined:
- showForm(): displays the home screen where users can enter url and expiration time in milliseconds to create tiny url
- redirectToUrl(): redirects from shortened url to the original url location
- shortenUrl():  creates a short version of the provided url
- processValidationResponse(BindingResult bindingResult,String url, ErrorResponse errorResponse) - checks if any errors

- Rest methods only used by rest clients
- ResponseEntity generateTinyUrl(@RequestBody TinyUrlRequest request) - POST, endpoint = "/createTinyUrl" consumes = "json", produces = "json"
- ResponseEntity getOriginalUrl(@PathVariable String id, HttpServletRequest request) - GET, endpoint = "/getOriginalUrl/{id}" consumes = "json", produces = "json"


### [UrlService.java]
- TinyUrlResponse generateTinyUrl(String url,Long expireAfterAccess) - creates and returns tiny url
- OriginalUrlResponse getOriginalUrl(String id) - gets original url

### [Validator.java]
- ErrorResponse validateUrl(String url) - validation of incoming URL
- ErrorResponse validateId(String id)  - validation of Id

### [CommonUtils.java]
- ErrorResponse generateErrorResponse(String name, List<Error> errors) 
- String generateIdFromUrl(String url)
- String buildTinyUrl(HttpServletRequest httpRequest)

### [StaticDataUtil.java]
- common constants used

### [HttpTinyUrlRequest.java]
The shorten url request has validations defined by the annotations on the fields.

### [RestTinyUrlRequest.java]
This request used to process Spring REST clients

### [RestOriginalUrlResponse.java]
This response used to process Spring REST clients GET and returns original url

### [RestTinyUrlUrlResponse.java]
Returns tiny url to Spring REST clients POST and returns tiny url

### [shortener.html]
This is a Thymeleaf-based (http://www.thymeleaf.org/) template that uses Twitter Bootstrap (http://getbootstrap.com/) to render the home screen's HTML code. It renders the data (Model) provided by the request mappings in the UrlController class.

### [LocalStorageImpl.java]
This class persists shortened urls into an in-memory persistence layer: hashmap. 
Implements the [ILocalStorageIntf] 



