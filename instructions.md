# Spring documentation

### This page will cover
* [Setting Up](#setting-up)
* [Adding classes](#adding-classes)
* [Adding Tables](#adding-classes)
    * [Movie](#movie)
    * [Rating](#rating)
    * [User](#user)
* [In Intellij](#in-application-properties-in-intellij--)
* [In Railway](#in-railway--)

## Setting up
1. To creeate a spring project go to  https://start.spring.io/. Change to maven java 4.02 add description and package name. Maven is equivalent of npm

![alt text](/images/image-1.png)

2. Then add the three dependencies as shown below

![alt text](/images/image-2.png)

3. Open in intellij should see in SqlSpringApiApplication you should see the main

![alt text](/images/image-3.png)

4. Replace pom.xml dependencies with only this dependency and comment the other dependencies out

        <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
                <version>4.0.2</version>
                <scope>compile</scope>
        </dependency>

![alt text](/images/image-5.png)

5. Then right click pom.xml -> Click Maven -> Sync Project (Do this every time you change something in POM)

![alt text](/images/image-4.png)

## Adding classes

6. Now create a new Java class called PingPong

![alt text](/images/image-6.png)

7. Add the following info in PingPong

        package com.example.demo;

        import org.springframework.http.MediaType;
        import org.springframework.web.bind.annotation.GetMapping;
        import org.springframework.web.bind.annotation.ResponseBody;
        import org.springframework.web.bind.annotation.RestController;

        //RESTful API
        // GET /api/customers -> Returns all customers in DB
        // GET /api/customers/:id -> Return Customer with ID (id)

        // POST /api/customers -> Create a new customer

        @RestController
        public class PingPong {

        @GetMapping(value = "/welcome", produces = MediaType.TEXT_HTML_VALUE)
        @ResponseBody
        public String welcomeAsHTML() {
            return """
                    <html>
                    <header><title>Welcome</title></header>
                    <body>
                    Hello world
                    </body>
                    </html>""";
        }

        @GetMapping("/")
        public String homePage() {
            return "Welcome";
        }

        @GetMapping("/ping")
        public String ping() {
            return "pong";
        }
        }

![alt text](/images/image-11.png)

Controller deals with http

8. To see welcome add this to browser

        http://localhost:8080/

![alt text](/images/image-9.png)

9. To see pong add this to browser

        http://localhost:8080/ping

![alt text](/images/image-10.png)



Go to Spring SQL and rerun

Enter http://localhost:8080/welcome in browser

![alt text](/images/image-12.png)

## Adding tables in demo

10. Create a package with the the name model with movie rating and user

![alt text](/images/image-24.png)

### Movie

In the Movie class add : 

    package com.example.demo.models;

    import jakarta.persistence.*;

    import java.util.List;

    @Entity(name = "Movies")
    public class Movie {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY) // generate primary key
        private Long id;
        private String title;
        private int releaseYear;

        //One Movie -> Many Ratings

        @OneToMany(mappedBy = "movie")
        private List<Rating> ratings;

        //Rating cant exist without movie

        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }

        public String getTitle() {
            return title;
        }

        public void setTitle(String title) {
            this.title = title;
        }

        public int getReleaseYear() {
            return releaseYear;
        }

        public void setReleaseYear(int releaseYear) {
            this.releaseYear = releaseYear;
        }

        public List<Rating> getRatings() {
            return ratings;
        }

        public void setRatings(List<Rating> ratings) {
            this.ratings = ratings;
        }
    }


### Rating

In the Rating class add : 

    package com.example.demo.models;

    import jakarta.persistence.*;

    @Entity(name = "Ratings")
    public class Rating {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY) // generate primary key
        private Long id;
        private int score;

        //Ratings -> User
        //Many ratings for one user

        @ManyToOne
        @JoinColumn(name = "user_id") //column called user id inside rating table
        //this will be primary key for user - this will be defined by @id in user
        private User user;
        //link user via user id


        //Rating -> Movie
        //many ratings -> One movie

        @ManyToOne
        @JoinColumn(name = "movie_id")
        private Movie movie;

        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }

        public int getScore() {
            return score;
        }

        public void setScore(int score) {
            this.score = score;
        }

        public User getUser() {
            return user;
        }

        public void setUser(User user) {
            this.user = user;
        }

        public Movie getMovie() {
            return movie;
        }

        public void setMovie(Movie movie) {
            this.movie = movie;
        }
    }



### User

In the User class add:

    package com.example.demo.models;

    import jakarta.persistence.*;

    import java.util.List;

    // Model - class representing each of our entities to th DB
    @Entity(name = "Users")
    public class User {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY) // generate primary key
        private Long id;
        private String name;
        private String email;

        //User -> Rating
        //One User -> Many ratings
        //mapped by owner ratinf cant exist without user
        @OneToMany(mappedBy = "user")
        private List<Rating> ratings;

        //Getters and setters
        //Lombok


        public List<Rating> getRatings() {
            return ratings;
        }

        public void setRatings(List<Rating> ratings) {
            this.ratings = ratings;
        }

        public String getEmail() {
            return email;
        }

        public void setEmail(String email) {
            this.email = email;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }
    }

___


11. Uncomment this dependency

![alt text](/images/image-15.png)

12. Right click pom.xml -> Maven -> Sync project

![alt text](/images/image-16.png)

13. Go to railway and open mySQL folder and open railway. In the new query add

        USE railway
        DROP TABLE 
        DROP TABLE 
        DROP TABLE 

![alt text](/images/image-17.png)

<!-- Go to MySQL, get public networking link -->

<!-- ![alt text](/images/image-18.png)

Go to application properties and add the following 
![alt text](/images/image-19.png) -->

14. In pom.xml uncomment jdbc, uncomment mysql connector depndency

Pom.xml should look like this -

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>4.0.2</version>
            <relativePath/> <!-- lookup parent from repository -->
        </parent>
        <groupId>com.example</groupId>
        <artifactId>demo</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <name>spring-sql-api</name>
        <description>My Sql railway db api</description>
        <url/>
        <licenses>
            <license/>
        </licenses>
        <developers>
            <developer/>
        </developers>
        <scm>
            <connection/>
            <developerConnection/>
            <tag/>
            <url/>
        </scm>
        <properties>
            <java.version>21</java.version>
        </properties>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
                <scope>compile</scope>
                <version>4.0.2</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-data-jdbc</artifactId>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-data-jpa</artifactId>
            </dependency>

            <dependency>
                <groupId>com.mysql</groupId>
                <artifactId>mysql-connector-j</artifactId>
                <scope>runtime</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-data-jdbc-test</artifactId>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-data-jpa-test</artifactId>
                <scope>test</scope>
            </dependency>
        </dependencies>

        <build>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </build>

    </project>


15. Then right click pom.xml -> Click Maven -> Sync Project (Do this every time you change something in POM)

![alt text](/images/image-4.png)

## In application properties in IntelliJ ->

16. Add the following

        spring.application.name=spring-sql-api
        spring.datasource.url=jdbc:mysql://<Hostname>:<port>/railway
        spring.datasource.username = root
        spring.datasource.password =
        spring.jpa.hibernate.ddl-auto = update
        spring.jpa.hibernate.show_sql = true
        spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

## In Railway ->
17. In railway get the domain and port

![alt text](/images/image-20.png)

18. Get the password

![alt text](/images/image-21.png)

19. Use it to populate the application.properties

![alt text](/images/image-22.png)

20. Ensure pom.xml is synced and then rerun SpringSQLDocumentation

21. Check Railway and tables created in Intellij should be shown

![alt text](/images/image-23.png)

Can also do this 

![alt text](/images/image-25.png)

Spring overview

![alt text](/images/image-27.png)

Nothing in database so port is empty

![alt text](/images/image-26.jpg)

user controller
postapping
![alt text](/images/image-29.png)

![alt text](/images/image-30.png)

user service
create on post request
add user
validation
name should be not empty 
emial shouldnt be empty
email shouldnt already be in use


In userpository that will return true if a user exists in a database

![alt text](/images/image-31.png)

![alt text](/images/image-32.png)

user service
Save is method on jpa repository

![alt text](/images/image-33.png)

![alt text](/images/image-34.png)


Postman request should be raw and JSON

You cant send an email to the api if already exists so you get an exception and a 202

![alt text](/images/image-35.png)

![alt text](/images/image-36.png)

Check if same
![alt text](/images/image-37.png)