# Springboot Restful API

## Starting your Spring Boot Application Build

In any Spring Boot Restful API you will need to start following some simple steps to get your project started. Performing these below steps will help you build your initial Springboot Restful API.

### Spring Boot Application Initializing
- Initializing a Spring Boot Application(We will walk through two different ways to initialize a project)
    - Spring Initializr
        1. Navigate to [https://start.spring.io](https://start.spring.io)

        ![Spring Boot Initializr Application]("")

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
        
        ![application.properties file]()