# Springboot Restful API

## Starting your Spring Boot Application Build

In any Spring Boot Restful API you will need to start following some simple steps to get your project started. Performing these below steps will help you build your initial Springboot Restful API.
- [Table of Contents](#starting-your-spring-boot-application-build)
    - [Spring Boot Application Initializing](#spring-boot-application-initializing)
    - [Spring Boot Packaging Structure](#spring-boot-packaging-structure)
    - [MySQL Connection Setup](#mysql-connection-setup)
    - [Model Creation](#model-creation)
    - [Repository Creation](#repository-creation)
    - [Exception Creation](#exception-creation)
    - [Controller Creation](#controller-creation)
    - [Conclusion](#conclusion)

### Spring Boot Application Initializing
- Initializing a Spring Boot Application(We will walk through two different ways to initialize a project)
    - Spring Initializr
        1. Navigate to [https://start.spring.io](https://start.spring.io)

        ![Spring Boot Initializr Application](https://user-images.githubusercontent.com/96712943/234622225-8274780a-c4a0-486a-92d7-358bf292f8bb.png)

        2. Choose either Gradle or Maven
        3. Choose Java
        4. Choose Spring Boot Version
        5. Name your Group Id for your project
        6. Name your Artifact Id for your project
        7. Type Description for your project
        8. Choose Package type
        9. Choose Java version
        10. Click Dependencies
        11. Add dependencies:
            - Spring Web
            - Spring Data JPA
            - MySQL Driver
            **These are the basic dependencies for our project**
        12. Click Generate
            - This will generate a project in a zip folder
            - Unzip folder in any directory on your machine
        13. Open Project in your selected IDE

    or

    - IDE Initialized Spring Boot Application
        - Prerequisites if using VS Code
            - Install these VS Code Extensions
                - Extension Pack for Java
                - Spring Boot Extension Pack
            - Initalize our Java Development Kit (JDK) in our IDE environment

        1. Open your selected IDE (We will be using VS Code)
        2. Navigate to the Command Palette
        3. Search "Spring Initializr"
        4. Select "Spring Initializr: Create a Maven Project"
        5. Select Spring Boot Version (We will be using 3.0.6)
        6. Select Java
        7. Name your Group Id for the project (Typical standard is your selected url backwards ex: com.myproject)
        8. Name your Artifact Id
        9. Select your packaging type (We will be using Jar)
        10. Select your Java version (We will be using version 17)
        11. Add dependencies:
            - Spring Web
            - Spring Data JPA
            - MySQL Driver
            **These are the basic dependencies for our project**
        12. Press Enter or Return to continue
        13. Select destination for your project

### Spring Boot Packaging Structure
[Go to the top](#starting-your-spring-boot-application-build)
- When we initialize a Spring Boot application chances are that there will be some starting packages and files in our project. Let's clean our structure up so that it meets typical standards.
    - Typical Spring Boot Application Structure
    ```java
    example
        src
            main    
                java
                    controller
                    exception
                    model
                    repository
                    ExampleApplication.java
                resources
                    application.properties
            test
                java
                    example
                        ExampleApplicationTest.java
        target
        .gitignore
        mvnw
        mvnw.cmd
        pom.xml
    ```
    **The above structure is most likely what your basic Spring Boot project will look like but it is dependant on your specific IDE you are using**

### MySQL Connection Setup
[Go to the top](#starting-your-spring-boot-application-build)
- We will now setup our connection to a MySQL Database in our Spring Boot Application
    1. Navigate to `src/main/resources`
    2. Open the `application.properties` file
    2. Type the following code:
        ```
        spring.datasource.url=jdbc:mysql://localhost:3306/example?useSSL=false
        spring.datasource.username=root
        spring.datasource.password=password

        # Hibernate properties
        spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLInnoDBDialect
        spring.jpa.hibernate.ddl-auto=update
        ```
        **Here is a break down of each of these lines**
        
        ![application.properties file](https://user-images.githubusercontent.com/96712943/234959736-f281c9ae-f147-47c2-abd4-b4b863f965d5.png)

### Model Creation
[Go to the top](#starting-your-spring-boot-application-build)
- Now let's look at how we can create a model for us to use throughout our service and controller layers
    1. Navigate to `src/main/java/model`
    2. Create new file for the model you want to create
        - `Ex: MyModel.java`
    3. Now we will add our code to turn this file into an appropriate Spring Boot Model
        - Initial model class creation
            - We use the `@Entity` annotation to tell Spring Boot this is an Entity class
            - We use the `@Table` annotation to tell Spring Boot what table this model represents 
        ```
        @Entity
        @Table(name="myModel")
        public class MyModel {
            
        }
        ```
        - Add our fields assigning them to columns
            - We use the `@Id` annotation to tell JPA this will be our primary key for this table and it will be the identifier for each entity added to our table
            - We use the `@GenerateValue(strategy = GenerationType.IDENTITY)` to auto generate a unique value for a specific field in a Java class when a new entity is created
            - We use the `@Column(name="columnName", nullable = false)` to tell our Java program that this field will belong to the specified column in our table. 
                - **The `nullable = false` is the same as using `NOT NULL` in our SQL statement**
                - **This means that any field annotated with `nullable = false` must always have a value**
        ```
        @Entity
        @Table(name = "myModel")
        public class MyModel {

            @Id
            @GenerateValue(strategy = GenerationType.IDENTITY)
            private long id;

            @Column(name = "firstName", nullable = false)
            private String firstName;

            @Column(name = "lastName", nullable = false)
            private String lastName;

        }
        ```
        - Add our constructor for all of our fields
            - This is a basic Java constructor that initializes all of our fields for object creation
        ```
        @Entity
        @Table(name = "myModel")
        public class MyModel {

            @Id
            @GenerateValue(strategy = GenerationType.IDENTITY)
            private long id;

            @Column(name = "firstName", nullable = false)
            private String firstName;

            @Column(name = "lastName", nullable = false)
            private String lastName;

            public myModel(long id, String firstName, String lastName) {
                this.id = id;
                this.firstName = firstName;
                this.lastName = lastName;
            }

        }
        ```
        - Now we can add our Getters and Setters for our fields
            - These are standard Java Getters and Setters we use to access or modify our fields
        ```
        @Entity
        @Table(name = "myModel")
        public class MyModel {

            @Id
            @GenerateValue(strategy = GenerationType.IDENTITY)
            private long id;

            @Column(name = "firstName", nullable = false)
            private String firstName;

            @Column(name = "lastName", nullable = false)
            private String lastName;

            public myModel(long id, String firstName, String lastName) {
                this.id = id;
                this.firstName = firstName;
                this.lastName = lastName;
            }

            public long getId() {
                return id;
            }

            public void setId(long id) {
                this.id = id;
            }

            public String getFirstName() {
                return firstName;
            }

            public void setFirstName(String firstName) {
                this.firstName = firstName;
            }

            public String getLastName() {
                return lastName;
            }

            public void setLastName(String lastName) {
                this.lastName = lastName;
            }

        }
        ```
        - Now let's add our toString, hashCode and equals methods
            - We override the inherited toString, hashCode and equals methods to fit the fields in our class
        ```
        @Entity
        @Table(name = "myModel")
        public class MyModel {

            @Id
            @GenerateValue(strategy = GenerationType.IDENTITY)
            private long id;

            @Column(name = "firstName", nullable = false)
            private String firstName;

            @Column(name = "lastName", nullable = false)
            private String lastName;

            public myModel(long id, String firstName, String lastName) {
                this.id = id;
                this.firstName = firstName;
                this.lastName = lastName;
            }

            public long getId() {
                return id;
            }

            public void setId(long id) {
                this.id = id;
            }

            public String getFirstName() {
                return firstName;
            }

            public void setFirstName(String firstName) {
                this.firstName = firstName;
            }

            public String getLastName() {
                return lastName;
            }

            public void setLastName(String lastName) {
                this.lastName = lastName;
            }

            @Override
            public int hashCode() {
                final int prime = 31;
                int result = 1;
                result = prime * result + (int) (id ^ (id >>> 32));
                result = prime * result + ((firstName == null) ? 0 : firstName.hashCode());
                result = prime * result + ((lastName == null) ? 0 : lastName.hashCode());
                return result;
            }

            @Override
            public boolean equals(Object obj) {
                if (this == obj)
                    return true;
                if (obj == null)
                    return false;
                if (getClass() != obj.getClass())
                    return false;
                myModel other = (myModel) obj;
                if (id != other.id)
                    return false;
                if (firstName == null) {
                    if (other.firstName != null)
                        return false;
                } else if (!firstName.equals(other.firstName))
                    return false;
                if (lastName == null) {
                    if (other.lastName != null)
                        return false;
                } else if (!lastName.equals(other.lastName))
                    return false;
                return true;
            }

            @Override
            public String toString() {
                return "myModel [id=" + id + ", firstName=" + firstName + ", lastName=" + lastName + "]";
            }
        }
        ```
    ### Repository Creation
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have our `model` created we can create a `repository` for our `model` which will enable `JPA` to handle all the `SQL statements` for us
        1. Navigate to `src/main/java/repository`
        2. Create a repository file for our created model
            - Ex: `MyModelRepository.java`
        3. Now we will add our code to make this a proper JPA repository
            - Jpa Repository Interface Creation
                - We inherit all the `C.R.U.D.` methods from the `JpaRepository interface` to be used on our `myModel entity`
                - We pass in our model and id data type as arguments to the `JpaRepository interface`
            ```
            public interface MyModelRepository extends JpaRepository<myModel, long>{
                
            }
            ```

    ### Exception Creation
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have our `model` and our `repository`, let's create a `custome exception` to handle a specific exception we might get in our program
        1. Navigate to `src/main/java/exception`
        2. Create a exception file for our custom exception
            - Ex: `ResourceNotFoundException.java` 
        3. Now we will add our code to make this a proper custom exception class
            - ResourceNotFoundException Class Creation
                - We use the `@ResponseStatus(value = HttpStatus.NOT_FOUND)` annotation to specify the HTTP response for our custom exception which in this case will throw a 404 status code
                - We extend the `RuntimeException class` to create a unchecked exception that will allow us to handle unexpected or unrecoverable errors in our code 
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

            }
            ```
            - Add our fields for our exception class
                - The `serialVersionUID` field is used to make sure that the class remains compatible with its serialized form across different versions of the software
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

                private static final long serialVersionUID = 1L;

            }
            ```
            - Add our constructorto initialize all of our fields
                - This constructor calls the constructor from the `RuntimeException class` using the `super method` with the provided string
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

                private static final long serialVersionUID = 1L;

                public ResourceNotFoundException(String message) {
                    super(message);
   
                }
            }
            ```

    ### Controller Creation
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have our `model`, `repository`, a `custom exception` to handle Resource not found exceptions, a `service interface`, and a `service implementation class`, we can create a controller for our `model service class`
        1. Navigate to `src/main/java/controller`
        2. Create a file for our model service implementation
            - Ex: `MyModelController.java`
        3. Now we will add our code to make this a proper model service controller class
            - MyModelController Class Initial Creation
                - We use the `@RestController` annotation to let our Java program know that this class is a `Rest Controller` that will be used to control the actions between the service layer and the database
                - We use the `@RequestMapping("/api/v1/")` annotation to tell our program how to handle incoming HTTP requests from our client 
            ```
            @RestController
            @RequestMapping("/api/v1/")
            public class MyModelController {

            }
            ```

            - Add our fields for our `model controller class`
                - We use the `@Autowired` annotation to automatically `inject` an `object instance` of our `UserRepository interface` into our `private field`
                - The `myModeRepository` field is used to store our repository for our model so we can call methods to handle requests sent from the client
            ```
            @RestController
            @RequestMapping("/api/v1/")
            public class MyModelController {

                @Autowired
                private MyModelRepository myModeRepository;

            }
            ```

            - Add our `HTTP POST route` method
                - We use the `@PostMapping` annotation to tell our Java program that this is how we will control the `POST` route requests for this model
                - We create the `saveMyModel` method which calls the `myModelRepository save` method to `save` the new model to our `repository`
            ```
            @RestController
            @RequestMapping("/api/v1/")
            public class MyModelController {

                @Autowired
                private MyModelRepository myModelRepository;

                @PostMapping("/myModel")
                public MyModel saveMyModel(@RequestBody MyModel myModel) {
                    return myModelRepository.save(myModel);
                }
                
            }
            ```

            - Add our `HTTP GET ALL route` method
                - We use the `@GetMapping("/myModel")` annotation to tell our Java program that this is how we will control the `GET ALL` route requests for this model
                - We create the `getAllMyModels` method which calls the `myModelRepository findAll` method which returns a all of our `objects` in our `repository`
            ```
            @RestController
            @RequestMapping("/api/v1")
            public class MyModelController {

                @Autowired
                private MyModelRepository MyModelRepository;

                @PostMapping("/myModel")
                public MyModel saveMyModel(@RequestBody MyModel myModel) {
                    return myModelRepository.save(myModel);
                }

                @GetMapping("/myModel")
                public List<User> getAllMyModels() {
                    return this.myModelRepository.findAll();
                }
                
            }
            ```

            - Add our `HTTP GET ONE route` method
                - We use the `@GetMapping("/myModel/{id}")` annotation to tell our Java program that this is how we will control the `GET ONE` route requests for this model
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `myModelId`
                - We create the `getMyModel` method which calls our `MyModelRepository findById` method to `get` the `object` we are looking for by its `id`. If it does not exist we return a new custom exception
                - We return the `ResponseEntity class` with a `response object` and a `HTTP status code`
            ```
            @RestController
            @RequestMapping("/api/v1")
            public class MyModelController {

                @Autowired
                private MyModelRepository MyModelRepository;

                @PostMapping("/myModel")
                public MyModel saveMyModel(@RequestBody MyModel myModel) {
                    return myModelRepository.save(myModel);
                }

                @GetMapping("/myModel")
                public List<User> getAllMyModels() {
                    return this.myModelRepository.findAll();
                }

                @GetMapping("/myModel/{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    MyModel myModel = this.myModelRepository.findById(myModelId).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));
                    return ResponseEntity.ok(myModel);
                }
                
            }
            ```
            - Add our `HTTP PUT route` method
                - We use the `@PutMapping("/myModel/{id}")` annotation to tell our Java program that this is how we will control the `PUT` route requests for this model
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `myModelId`
                - We use the `@RequestBody` annotation to tell our method where this object we are using is coming from we assign it to a new variable called `myModel`
                - We create the `updateMyModel method` which calls the  `myModelRepository findById` method to get the `object` we want to `put` the changes from the passed in `object` into. If it is not found we throw our custom exception
                - We modify the data in our `existingMyModel object` using `setter` methods and the passed in `objects data`
                - We get the data from the passed in `object` by using its `getter` methods
                - We use the `myModelRepository save` method to `save` the changes we made to our `existingMyModel object` into our `repository`
                - We return a `ResponseEntity` back to our `client` telling them the process was successful
            ```
            @RestController
            @RequestMapping("/api/v1")
            public class MyModelController {

                @Autowired
                private MyModelRepository MyModelRepository;

                @PostMapping("/myModel")
                public MyModel saveMyModel(@RequestBody MyModel myModel) {
                    return myModelRepository.save(myModel);
                }

                @GetMapping("/myModel")
                public List<User> getAllMyModels() {
                    return this.myModelRepository.findAll();
                }

                @GetMapping("/myModel/{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    MyModel myModel = this.myModelRepository.findById(myModelId).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));
                    return ResponseEntity.ok(myModel);
                }

                @PutMapping("/myModel/{id}")
                public ResponseEntity<MyModel> updateMyModel(@PathVariable("id") long id, @RequestBody MyModel myModel) {

                    MyModel existingMyModel = this.myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));

                    existingMyModel.setFirstName(myModel.getFirstName());
                    existingMyModel.setLastName(myModel.getLastName());

                    MyModel updatedMyModel = this.myModelRepository.save(existingMyModel);
                    return ResponseEntity.ok(updatedMyModel);
                }
                
            }
            ```

            - Add `HTTP DELETE route` method
                - We use the `@DeleteMapping("/myModel/{id}")` annotation to tell our Java program that this is how we will control the `DELETE` route requests for this model
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `id`
                - We create the `deleteMyModel method` which calls the  `myModelRepository findById` method to get the `object` we want to `delete`. If it is not found we throw our custom exception
                - We `delete` the `myModel object` using the `myModelRepository delete` method
                - We return a `ResponseEntity` back to our `client` telling them the process was successful
            ```
            @RestController
            @RequestMapping("/api/v1")
            public class MyModelController {

                @Autowired
                private MyModelRepository MyModelRepository;

                @PostMapping("/myModel")
                public MyModel saveMyModel(@RequestBody MyModel myModel) {
                    return myModelRepository.save(myModel);
                }

                @GetMapping("/myModel")
                public List<User> getAllMyModels() {
                    return this.myModelRepository.findAll();
                }

                @GetMapping("/myModel/{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    MyModel myModel = this.myModelRepository.findById(myModelId).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));
                    return ResponseEntity.ok(myModel);
                }

                @PutMapping("/myModel/{id}")
                public ResponseEntity<MyModel> updateMyModel(@PathVariable("id") long id, @RequestBody MyModel myModel) {

                    MyModel existingMyModel = this.myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));

                    existingMyModel.setFirstName(myModel.getFirstName());
                    existingMyModel.setLastName(myModel.getLastName());

                    MyModel updatedMyModel = this.myModelRepository.save(existingMyModel);
                    return ResponseEntity.ok(updatedMyModel);
                }

                @DeleteMapping("/myModel/{id}")
                public ResponseEntity<String> deleteMyModel(@PathVariable("id") long id) {
                    MyModel myModel = this.myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel does not exist with the Id: " + myModelId));

                    this.myModelRepository.delete(myModel);
                    return ResponseEntity.ok("My Model with Id: " + id + " has been deleted");
                }
                
            }
            ```

    ### Conclusion
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have successfully built a basic Spring Boot REST API for our single model class, we can scale our API by building all the same code for each model we want to have in our program
    - I hope this tutorial has helped walk you through the process and visualize the process used to build a REST API and connect it to a MySQL database
    - Happy Coding!
