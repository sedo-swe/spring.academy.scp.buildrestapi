# Building a REST API with Spring Boot
from Spring Academy / Spring Certified Professional

## Module 1
### Creating RESTful Endpoints
1. Spring & Spring Boot
2. API Contracts & JSON
3. Testing First
4. Implementing GET
5. Repositories & Spring Data
    1. Controller-Repository Architecture
       * **Separation of Concerns** principle states that well-designed software should be modular, with each module having distinct and separate concerns from any other module.
    2. **Repository** pattern
    3. Layered Architecture
       * API Clients : Web browsers, smartphone apps, other applications
       * <table>
            <tr><td> Controller (Communications Interface Layer) </td><td> HTTP; Spring example: @RestController </td></tr>
            <tr><td> Other Layers*</td><td> Business logic, algorithms, calculators</td></tr>
         </table>
       * Data Store : Relational DB (e.g. MySQL)
   4. Auto Configuration
   5. Spring Data's CrudRepository
      ```
        interface CashCardRepository extends CrudRepository<CashCard, Long> {
        }
      
        cashCard = cashCardRepository.findById(99);
      ```


## Module 2
### Developing a Secure App
1. Implementing POST
   * Idempotence and HTTP : For each method, the HTTP standard specifies whether it is idempotent or not. GET, PUT, and DELETE are idempotent, whereas POST and PATCH are not.
   * The POST Request and Response
2. Returning a list with GET
   * Requesting a List of Cash Cards
   * Pagination and Sorting
   * Regarding Unordered Queries
     - Minimize cognitive overhead: Other developers (not to mention users) will probably appreciate a thoughtful ordering when developing it.
     - Minimize future errors: What happens when a new version of Spring, or Java, or the database, suddenly causes the “random” order to change overnight?
   * Test Interaction and @DirtiesContext
     - @DirtiesContext causes Spring to start with a clean slate, as if those other tests hadn't been run. However, you shouldn't use it indiscriminately; you should have a good reason.

3. Simple Spring Security
   * What Is Security? 
     - HTTP Authentication and Authorization work
     - Prevent unauthorized access to our Family Cash Card service.
   * Authentication
     - Principal: A user of an API can actually be a person or another program
     - Authentication is the act of a Principal proving its identity to the system
     - Authentication Session (or Auth Session, or just Session) 
     - Session Token (a string of random characters) that is generated, and placed in a Cookie
   * Spring Security and Authentication
     - implements authentication in the Filter Chain
     - a sequence of methods that get called prior to the Controller
     - Each filter decides whether to allow request processing to continue, or not
     - Spring Security inserts a filter which checks the user’s authentication and returns with a 401 UNAUTHORIZED response if the request is not authenticated.
   * Authorization
     - Authorization happens after authentication, and allows different users of the same system to have different permissions.
     - Spring Security provides Authorization via Role-Based Access Control (RBAC).
   * Same Origin Policy
     - This policy states that only scripts which are contained in a web page are allowed to send requests to the origin (URI) of the web page.
   * Cross-Origin Resource Sharing (CORS)
     - a way that browsers and servers can cooperate to relax the SOP
     - “allowed origins” of requests coming from an origin outside the server’s.
     - @CrossOrigin
   * Common Web Exploits
     * Cross-Site Request Forgery (CSRF), Session Riding
       + A CSRF Token is different from an Auth Token because a unique token is generated on each request.
       + --> When should you use CSRF protection? Our recommendation is to use CSRF protection for any request that could be processed by a browser by normal users. If you are only creating a service that is used by non-browser clients, you will likely want to disable CSRF protection.
     * Cross-Site Scripting (XSS)
       + This occurs when an attacker is somehow able to “trick” the victim application into executing arbitrary code.
       + The main way to guard against XSS attacks is to properly process all data from external sources (like web forms and URI query strings).

## Module 3
### Rounding Out CRUD
1. Implementing PUT
   * PUT and PATCH
     - PUT: create or replace the complete record
     - PATCH: update only some fields of th existing record (partial update which can have a non-trivial impact on performance if the record is large enough)
   * Surrogate and Natural Keys
     - Why want to use a PUT to create a resource?
       * Natural Key : supplied by the client to the API &nbsp; ==> PUT
       * Surrogate Key: generated by the server  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ==> POST
         * If you need the server to return the URI of the created resource (or the data you use to construct the URI), then POST
   * Resources and Sub-Resources
     - URIs and collections of sub-resources
   * Response Body and Status Code

2. Implementing DELETE
   * Return 204 NO CONTENT or 404 NOT FOUND
   * Additional Options
     * Hard and Soft delete
       * Hard : Remove a record from database
       * Soft : Mark a record as deleted in database. ex) IS_DELETED (boolean) or DELETED_DATE (date)
         * Need to refactor Read by filtering out soft deleted records
     * Audit Trail and Archiving

### Summary
1. You built the API using a layered architecture. You understand how Spring Security sits at the “front” of the API, Spring Web enables HTTP communications between the API and its clients, and Spring Data handles reading and writing to/from the relational data store.
2. You used a test-first approach to provide confidence that your application works as designed while driving out your app's functionality.
3. You drove your implementation using a Steel Thread - exercising all the integration points and validating your architecture early on to de-risk your functionality.
4. You used the Red, Green, Refactor process to improve your code (and tests!) throughout the application development.