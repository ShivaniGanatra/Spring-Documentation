Make a new folder called DTO (Data transfer Object)

In that folder make a class CreateUserRequest

![alt text](/images/image-38.png)

In CreateUserRequest class casic validation on dto?,complex calidation in service

Add package jakarta Validation and add that dependency in pomixml 

    <!-- Source: https://mvnrepository.com/artifact/jakarta.validation/jakarta.validation-api -->
    <dependency>
        <groupId>jakarta.validation</groupId>
        <artifactId>jakarta.validation-api</artifactId>
        <version>4.0.0-M1</version>
        <scope>compile</scope>
    </dependency>

then do pom.xml sync project

Then to CreateUserRequest add the method :

    @NotBlank(message = "Name is required") 
    @Size(min = 3,max = 100, message = "name must be between 3 and 100 char long")
    private String name;

    @NotBlank(message = "Email is required") 
    @Email(message = "email must be valid") 
    private String email;

![alt text](/images/image-39.png)

Then make constructor and getters and setters just make getter and setter manually

![alt text](/images/image-40.png)

Go to user controller and chnage postmapping method
![alt text](/images/image-45.png)

Change user service add user

![alt text](/images/image-41.png)


Create a another DTO class clalled UserResponse in DTO folder 

-chnage image so that there are getters

![alt text](/images/image-42.png)



![alt text](/images/image-43.png)

In service need to get usereee
Go to UserSercive and add this method and change addUserMethod

    private UserResponse mapToResponse(User user) {
        return new UserResponse(user.getId(),user.getName(), user.getEmail());
    }


![alt text](/images/image-44.png)

        public UserResponse addUser(CreateUserRequest newUserRequest) {
    //        if(!StringUtils.hasText(user.getName()) || !StringUtils.hasText(user.getEmail())) {
    //            throw new IllegalArgumentException("Name and email are required");
    //        }
        if (userRepo.existByEmail(newUserRequest.getEmail())) {
            throw new IllegalArgumentException("Email already in user : " + newUserRequest.getEmail());
        }
        User user = new User();
        user.setName(newUserRequest.getName());
        user.setEmail(newUserRequest.getEmail());

        User saved = userRepo.save(user);
        return mapToResponse(saved);
    }

Change PostMapping in UserController

    @PostMapping
    public UserResponse createUser(@Validated @RequestBody CreateUserRequest newUserRequest) {
        return userService.addUser(newUserRequest);
    }

![alt text](/images/image-46.png)

Add this dependency in pom.xml and sync 

    <!-- Source: https://mvnrepository.com/artifact/org.hibernate.validator/hibernate-validator -->
    <dependency>
        <groupId>org.hibernate.validator</groupId>
        <artifactId>hibernate-validator</artifactId>
        <version>9.1.0.Final</version>
        <scope>compile</scope>
    </dependency>

![alt text](/images/image-47.png)

Add this request in Postman

    {   "id": 5,
        "name" : "Remi"
    }
This is a good request

![alt text](/images/image-48.png)

Check a bad request

..

![alt text](/images/image-49.png)
in user contolleer
We just wanna get one user so in user contorller add a new getmappinh mehod. 
say path variable given to use by request 

this long is path vairable that will b coming in endpoint

![alt text](/images/image-50.png)

In userservice

public user response findUserById(Long id) {
    retrun usertRepo
}

get ReferebcebyId is a orxisting methof

![alt text](/images/image-51.png)

![alt text](/images/image-52.png)

![alt text](/images/image-54.png)

//crud create read updat delete

in user services delete

publuc void deleteUser(LongId) {
    if (!userRepo.existsById)
}...

![alt text](/images/image-55.png)

In user controller
@DeletMapping("/{id}")
public void deleteUser(@PathVariable Long id) {
    ...
}

![alt text](/images/image-56.png)

Test in postman delete

![alt text](/images/image-57.png)

Correct this

![alt text](/images/image-58.png)

Movies
controller dont do logic just send requests

make MovieContoller 

in movi controlleer

private final MovieService movieService;

pucluc MovieContoller()

![alt text](/images/image-59.png)

make movie service

![alt text](/images/image-60.png)

![alt text](/images/image-61.png)

show movi repository

mak find movie byid method

![alt text](/images/image-62.png)

create mocie method in service

![alt text](/images/image-63.png)

Make createMovierequest java

![alt text](/images/image-64.png)

Add gettr and stter
![alt text](/images/image-65.png)

create movie method in movie service
![alt text](/images/image-66.png)

Do postmapping in moce controller

![alt text](/images/image-67.png)
![alt text](/images/image-68.png)
![alt text](/images/image-69.png)
![alt text](/images/image-70.png)
![alt text](/images/image-71.png)
![alt text](/images/image-72.png)

In Movie API 
Create a deleteMovie and a getAllMovies methods in the MovieController and add all the required code in the other layer of the application 

