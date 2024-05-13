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
3. Simple Spring Security