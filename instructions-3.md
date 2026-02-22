Get getter and setter as well 

![alt text](/images/image-73.png)

![alt text](/images/image-74.png)

![alt text](/images/image-75.png)

![alt text](/images/image-76.png)

method to get all movies

![alt text](/images/image-77.png)

make find all movies method

![alt text](/images/image-78.png)

![alt text](/images/image-79.png)

Make new class calld RatingContrpller
make post mapping createRating method

private final RatingService ratingService
public Rating createRating(@Requestparam Long movieId, LonguserId, int movieScore) {
    return ratingService.

}

![alt text](/images/image-80.png)

Create RatingService with method that will take into considerating movie table

Check if movie exists before adding rating to movie

private Final Movie repository moviRepo;
private final UserRepository userRepo;
public Rating createRating(Long movieId, LonguserId, int movieScore) {
    Movie movie = movieRepo.findById(movieId).orElseeThrow(() -> {
        new EntityNotFoundException(String.format("movie with id: %id wasnot found",
    mocieId))
    });

return 
}


ADD IMAGE

Make RatingRepository
@Repository
public interfave RatingRepository extends JpaRepository<Rating,Long> {
    boolean existsByUserAndMovie(User user Movie movie)
}

![alt text](/images/image-81.png)
![alt text](/images/image-82.png)

![alt text](/images/image-83.png)

![alt text](/images/image-84.png)

![alt text](/images/image-85.png)

Check adding a rating in postman
![alt text](/images/image-86.png)

To fix this issue chnage movie.java
and add json ignore

Check adding a rating in postman
![alt text](/images/image-87.png)

![alt text](/images/image-88.png)

Can make new class RatingResponse

public class RatingResponse {
    private Long if:
    private int 
}
and add constructors and getters
![alt text](/images/image-89.png)

![alt text](/images/image-90.png)

![alt text](/images/image-91.png)

private RatingResponse mapToResponse
get image
then get all ratings

![alt text](/images/image-92.png)
![alt text](/images/image-93.png)

make rating request class in dto
![alt text](/images/image-94.png)


Add methods
![alt text](/images/image-95.png)

Add constucors and getters
![alt text](/images/image-96.png)

chnage function createRating  in rating service

![alt text](/images/image-97.png)

see bottom part

chnage postmapping in rest controler

![alt text](/images/image-98.png)

![alt text](/images/image-99.png)

![alt text](/images/image-100.png)

![alt text](/images/image-100.png)

![alt text](/images/image-101.png)

Check in postman
![alt text](/images/image-102.png)

What is purpose of respinse entity

chnage postmapping createRating

![alt text](/images/image-103.png)

![alt text](/images/image-104.png)


Create update userRequest in DTO

![alt text](/images/image-105.png)

![alt text](/images/image-106.png)

usrReSPONSE update user method
user may not= have enail

![alt text](/images/image-107.png)
 
 putt completly rewrites
 patch updates bits of it 

 git-acp "did something"
 acp means add commit push


 in featute branch git pull origin main

 push to feature branch

 then make pull request