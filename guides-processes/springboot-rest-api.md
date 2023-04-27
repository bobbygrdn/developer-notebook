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
    - [Service Creation](#service-creation)
    - [Service Implementation Creation](#service-implementation-creation)
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
        - Prerequisites
            - Install these VS Code Extensions
                - Extension Pack for Java
                - Spring Boot Extension Pack
            - Initalize our Java Development Kit (JDK) in our IDE environment

        1. Open you selected IDE (We will be using VS Code)
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
                    service
                        impl
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
        
        ![application.properties file](https://user-images.githubusercontent.com/96712943/234928832-32134f70-d10a-461f-986d-379e429b05c6.png)

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
                - The other fields are used to identify what resource we are talking about by its name, value and specific field name
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

                private static final long serialVersionUID = 1L;
                private String resourceName;
                private String fieldName;
                private Object FieldValue;

            }
            ```
            - Add our constructorto initialize all of our fields
                - This constructor calls the constructor from the `RuntimeException class` using the `super method` with the provided string we have formatted
                - Then as always it initializes the fields for the class when we create an object instance
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

                private static final long serialVersionUID = 1L;
                private String resourceName;
                private String fieldName;
                private Object FieldValue;

                public ResourceNotFoundException(String resourceName, String fieldName, Object fieldValue) {
                    super(String.format("%s not found with %s : '%s'", resourceName, fieldName, fieldValue));
                    this.resourceName = resourceName;
                    this.fieldName = fieldName;
                    this.fieldValue = fieldValue;
                }
            }
            ```
            - Add our Getters and Setters for our fields
                - These are standard Java Getters and Setters for our fields
            ```
            @ResponseStatus(value = HttpStatus.NOT_FOUND)
            public class ResourceNotFoundException extends RuntimeException {

                private static final long serialVersionUID = 1L;
                private String resourceName;
                private String fieldName;
                private Object FieldValue;

                public ResourceNotFoundException(String resourceName, String fieldName, Object fieldValue) {
                    super(String.format("%s not found with %s : '%s'", resourceName, fieldName, fieldValue));
                    this.resourceName = resourceName;
                    this.fieldName = fieldName;
                    this.fieldValue = fieldValue;
                }

                public static long getSerialversionuid() {
                    return serialVersionUID;
                }

                public String getResourceName() {
                    return resourceName;
                }

                public void setResourceName(String resourceName) {
                    this.resourceName = resourceName;
                }

                public String getFieldName() {
                    return fieldName;
                }

                public void setFieldName(String fieldName) {
                    this.fieldName = fieldName;
                }

                public Object getFieldValue() {
                    return fieldValue;
                }

                public void setFieldValue(Object fieldValue) {
                    this.fieldValue = fieldValue;
                }
            }
            ```
    ### Service Creation
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have our `model`, `repository` and a `custom exception` to handle Resource not found exceptions, let's create a `service interface` for our model
        1. Navigate to `src/main/java/service`
        2. Create a file for our model service
            - Ex: `MyModelService.java`
        3. Now we will add our code to make this a proper model service interface
            - MyModelService Interface Creation
                - We create a method for each of our `C.R.U.D.` functions we want to perform on our model
                    - `Create` -> `MyModel saveMyModel(MyModel myModel);`
                        - We use this method to create a new `object instance` of our `model class` and `store` it as an `entity` in our `MySQL database`
                    - `Get All` -> `List<MyModel> getAllMyModel();`
                        - We use this method to get all the `entities` in our `MySQL database` and return them as a `list of object instances` of our `model class`
                    - `Get One` -> `MyModel getMyModelById(long id);`
                        - We use this method to get one `entity` from our `MySQL database` by it's `id` and return it as a `object instance` of our `model class`
                    - `Put` -> `MyModel updateMyModel(MyModel, long id);`
                        - We use this method to replace an `existing entity` with a `new entity` with `updated information` in our `MySQL database` by it's `id`
                    - `Delete` -> `void deleteMyModel(long id);`
                        - We use this method to delete an `entity` from our `MySQL database` by it's `id`

            ```
            public interface MyModelService {
                
                MyModel saveMyModel(MyModel myModel);

                List<MyModel> getAllMyModel();

                MyModel getMyModelById(long id);

                MyModel updateMyModel(MyModel, long id);

                void deleteMyModel(long id);
            
            }
            ```
    ### Service Implementation Creation
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have our `model`, `repository`, a `custom exception` to handle Resource not found exceptions, and a `service interface`, let's create a `service implementation class` for our `model service interface`
        1. Navigate to `src/main/java/service/impl`
        2. Create a file for our model service implementation
            - Ex: `MyModelServiceImpl.java`
        3. Now we will add our code to make this a proper model service interface implementation
            - MyModelServiceImpl Class Initial Creation
                - We use the `@Service` annotation to let our Java program know that this class is a `service component` that can be used by other components in the application
                - We implements the `MyModelService interface` so we can override it's methods for all of our `C.R.U.D.` functions we want this service to execute
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

            }
            ```
            - Add our fields for our `model Service Interface Implementation class`
                - The `myModelRepository` field is used to store our repository for our model so we can use it's methods and properties
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

            }
            ```
            - Add our constructor to initialize all of our fields
                - We call the `constructor` of the `MyModelService interface` using the `super method`
                - We initialize the `myModelRepository field` for the class when we create an object instance
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

            }
            ```
            - Add our `Create method` for our `HTTP POST route`
                - We use the `@Override` annotation to tell our Java program that we are overriding a parent method from our `myModelService interface`
                - We input our `object instance` of our `MyModel class` as a parameter
                - We return the response to calling our `MyModelRepository save` method which saves our object instance to our `MyModelRepository` field
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

                @Override
                public MyModel saveMyModel(MyModel myModel) {
                    return myModelRepository.save(myModel);
                }

            }
            ```

            - Add our `Read method` for our `HTTP Get All Route`
                - We use the `@Override` annotation to tell our Java program that we are overriding a parent method from our `myModelService interface`
                - We return a list of our `object instances` of our `MyModel class` by calling the `myModelRepository` `findAll method`
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

                @override
                public MyModel saveMyModel(MyModel myModel) {
                    return myModelRepository.save(myModel);
                }
            
                @override
                public List<MyModel> getAllMyModels() {
                    return MyModelRepository.findAll();
                }

            }
            ```

            - Add our `Read method` for our `HTTP Get One Route`
                - We use the `@Override` annotation to tell our Java program that we are overriding a parent method from our `MyModelService interface`
                - We pass in an `id` of the object we are looking for into our `myModelRepository` `findById method`
                - We return an object instance of our MyModel class by calling the myModelRepository findById method using the passed in id
                - We use the `orElseThrow method` to `throw` our `custom exception class` if the object we are trying to find does not exist
                - We pass in the `resourceName`, `fieldName` and `id` of the resource that we are trying to find
                
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

                @Override
                public MyModel saveMyModel(MyModel myModel) {
                    return myModelRepository.save(myModel);
                }
            
                @Override
                public List<MyModel> getAllMyModels() {
                    return MyModelRepository.findAll();
                }

                @Override
                public MyModel getMyModelById(long id) {
                    return myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel", "Id", id));
                }
            }
            ```
            
            - Add our `Update method` for our `HTTP Put Route`
                - We use the `@Override` annotation to tell our Java program that we are overriding a parent method from our `MyModelService interface`
                - We pass in the new object instance of our model class and the id of the object we are changing using the properties of our passed in object instance
                - We check to see if the `object` we are referencing by `id` exists and if it does not we throw our custom `ResourceNotFoundException`
                - Once we have verified it exists, we use `setter methods` to set the fields on the `existing object` with `getter methods` used to get the fields from our `passed in object` 
                - We use the `myModelRepository` `save method` to save our newly changed object into our `repository`
                - We return the `object` as a response to calling our `update method`
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

                @Override
                public MyModel saveMyModel(MyModel myModel) {
                    return myModelRepository.save(myModel);
                }
            
                @Override
                public List<MyModel> getAllMyModels() {
                    return MyModelRepository.findAll();
                }

                @Override
                public MyModel getMyModelById(long id) {
                    return myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel", "Id", id));
                }

                @Override
                public MyModel updateMyModel(MyModel myModel, long id) {

                    MyModel existingMyModel = myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("My Model", "Id", id));

                    existingMyModel.setFirstName(myModel.getFirstName());
                    existingMyModel.setLastName(myModel.getFirstName());

                    myModelRepository.save(existingMyModel);
                    return existingMyModel;
                }

            }
            ```

            - Add our `Delete method` for our `HTTP Delete Route`
                - We use the `@Override` annotation to tell our Java program that we are overriding a parent method from our `MyModelService interface`
                - We pass in the `id` of the `object` we are wanting to `delete`
                - We check to see if the `object` we are referencing by `id` exists and if it does not we throw our custom `ResourceNotFoundException`
                - Once we have verified it exists, we use the `myModelRepository class` method `deleteById` to `delete` the `object` referencing it by the passed in `id`
            ```
            @Service
            public class MyModelServiceImpl implements MyModelService {

                private MyModelRepository myModelRepository;

                public MyModelServiceImpl(MyModelRepository myModelRepository) {
                    super();
                    this.myModelRepository = myModelRepository;
                }

                @Override
                public MyModel saveMyModel(MyModel myModel) {
                    return myModelRepository.save(myModel);
                }
            
                @Override
                public List<MyModel> getAllMyModels() {
                    return MyModelRepository.findAll();
                }

                @Override
                public MyModel getMyModelById(long id) {
                    return myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("MyModel", "Id", id));
                }

                @Override
                public MyModel updateMyModel(MyModel myModel, long id) {

                    MyModel existingMyModel = myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("My Model", "Id", id));

                    existingMyModel.setFirstName(myModel.getFirstName());
                    existingMyModel.setLastName(myModel.getFirstName());

                    myModelRepository.save(existingMyModel);
                    return existingMyModel;
                }

                @Override
                public void deleteMyModel(long id) {

                    myModelRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("My model", "Id", id));

                    myModelRepository.deleteById(id);
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
                - We use the `@RequestMapping("/api/myModel")` annotation to tell our program how to handle incoming HTTP requests from our frontend 
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

            }
            ```

            - Add our fields for our `model service controller class`
                - The `myModelService` field is used to store our service for our model so we can call methods to handle requests sent from the frontend
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

            }
            ```

            - Add our constructor to initialize all of our fields
                - We call the `constructor` of the `Object Java class` using the `super method`
                - We initialize the `myModelService field` for the class when we create an object instance
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }
                
            }
            ```

            - Add our `HTTP POST route` method
                - We use the `@PostMapping` annotation to tell our Java program that this is how we will control the `POST` route requests for this model
                - We use the `ResponseEntity class` to create a `response object` with the `HTTP status code` and the `response body`
                - We call the `saveMyModel method` from our `MyModelService class` to `save` the new model
                - We return a `ResponseEntity` back to our `client` telling them the `object` was successful created
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }

                @PostMapping
                public ResponseEntity<MyModel> saveMyModel(@RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.saveMyModel(myModel), HttpStatus.CREATED);
                }
                
            }
            ```

            - Add our `HTTP GET ALL route` method
                - We use the `@GetMapping` annotation to tell our Java program that this is how we will control the `GET ALL` route requests for this model
                - We call the `getAllMyModels method` from our `MyModelService class` to `get` all the models as a `List`
                - We return the `list` back to our `client`
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }

                @PostMapping
                public ResponseEntity<MyModel> saveMyModel(@RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.saveMyModel(myModel), HttpStatus.CREATED);
                }

                @GetMapping
                public List<MyModel> getAllMyModels() {
                    return myModelService.getAllMyModels();
                }
                
            }
            ```

            - Add our `HTTP GET ONE route` method
                - We use the `@GetMapping("{id}")` annotation to tell our Java program that this is how we will control the `GET ONE` route requests for this model
                - We use the `ResponseEntity class` to create a `response object` with the `HTTP status code` and the `response body`
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `myModelId`
                - We call the `getMyModelById method` from our `MyModelService class` to `get` the `object` we are looking for by its `id` 
                - We return a `ResponseEntity` back to our `client` telling them the process was successful
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }

                @PostMapping
                public ResponseEntity<MyModel> saveMyModel(@RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.saveMyModel(myModel), HttpStatus.CREATED);
                }

                @GetMapping
                public List<MyModel> getAllMyModels() {
                    return myModelService.getAllMyModels();
                }

                @GetMapping("{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    return new ResponseEntity<MyModel>(myModelService.getMyModelById(myModelId), HttpStatus.OK);
                }
                
            }
            ```
            - Add our `HTTP PUT route` method
                - We use the `@PutMapping("{id}")` annotation to tell our Java program that this is how we will control the `PUT` route requests for this model
                - We use the `ResponseEntity class` to create a `response object` with the `HTTP status code` and the `response body`
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `id`
                - We use the `@RequestBody` annotation to tell our method where this object we are using is coming from we assign it to a new variable called `myModel`
                - We call the `updateMyModel method` from our `MyModelService class` to `put` the changes from the passed in `object` into the `object` we are looking for by its `id` 
                - We return a `ResponseEntity` back to our `client` telling them the process was successful
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }

                @PostMapping
                public ResponseEntity<MyModel> saveMyModel(@RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.saveMyModel(myModel), HttpStatus.CREATED);
                }

                @GetMapping
                public List<MyModel> getAllMyModels() {
                    return myModelService.getAllMyModels();
                }

                @GetMapping("{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    return new ResponseEntity<MyModel>(myModelService.getMyModelById(myModelId), HttpStatus.OK);
                }

                @PutMapping("{id}")
                public ResponseEntity<MyModel> updateMyModel(@PathVariable("id") long id, @RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.updateMyModel(myModel, id), HttpStatus.OK);
                }
                
            }
            ```

            - Add `HTTP DELETE route` method
                - We use the `@DeleteMapping("{id}")` annotation to tell our Java program that this is how we will control the `DELETE` route requests for this model
                - We use the `ResponseEntity class` to create a `response object` with the `HTTP status code` and the `response body`
                - We use the `@PathVariable("id")` to tell our method we are using the `url path id parameter` and we will assign it to a new variable called `id`
                - We call the `deleteMyModel method` from our `MyModelService class` to `delete` the `object` we are looking for by its `id` 
                - We return a `ResponseEntity` back to our `client` telling them the process was successful
            ```
            @RestController
            @RequestMapping("/api/myModel")
            public class MyModelController {

                private MyModelService myModelService;

                public MyModelController(myModelService) {
                    super();
                    this.myModelService = myModelService;
                }

                @PostMapping
                public ResponseEntity<MyModel> saveMyModel(@RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.saveMyModel(myModel), HttpStatus.CREATED);
                }

                @GetMapping
                public List<MyModel> getAllMyModels() {
                    return myModelService.getAllMyModels();
                }

                @GetMapping("{id}")
                public ResponseEntity<MyModel> getMyModel(@PathVariable("id") long myModelId) {
                    return new ResponseEntity<MyModel>(myModelService.getMyModelById(myModelId), HttpStatus.OK);
                }

                @PutMapping("{id}")
                public ResponseEntity<MyModel> updateMyModel(@PathVariable("id") long id, @RequestBody MyModel myModel) {
                    return new ResponseEntity<MyModel>(myModelService.updateMyModel(myModel, id), HttpStatus.OK);
                }

                @DeleteMapping("{id}")
                public ResponseEntity<String> deleteMyModel(@PathVariable("id") long id) {
                    myModelService.deleteMyModel(id);
                    return new ResponseEntity<String>("My Model deleted successfully!", HttpStatus.OK);
                }
                
            }
            ```

    ### Conclusion
    [Go to the top](#starting-your-spring-boot-application-build)
    - Now that we have successfully built a basic Spring Boot REST API for our single model class, we can scale our API by building all the same code for each model we want to have in our program
    - I hope this tutorial has helped walk you through the process and visualize the process used to build a REST API and connect it to a MySQL database
    - Happy Coding!
