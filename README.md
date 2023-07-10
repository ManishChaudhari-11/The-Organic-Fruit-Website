

# Social Media Rest API

This project consist of two collection of API namely User and Post. Each User and Post has some APIs which are given as follows : 

#### o Users :
    
• Create Register User API

• Login User API

• Get User API
    
    ※ If authorized then all information of all users
    ※ If not, then only limited information of all users
    ※ If specific id or ids are given, then only information of those users
    ※ Optional paging
    ※ Optional sorting

#### o Posts :

• Create/Update Post API (Common endpoint, if post exist then update else create) (protected route)

• Get Post by User API (protected route) (should include total likes, dis-likes, recently liked & disliked top 5 users with their basic information)

    ※ Optional filter for likes, dislikes, title, content, created_at, updated_at
    ※ Optional paging
    ※ Optional sorting

• API to like/dislike post (protected route)

• API to get top 10/50 liked/disliked posts (protected route)

    ※ Optional filter to get it for specific user


### Software Requirements : 
    1. Spring Tool Suite 4.19.0.RELEASE
    2. MySQL Database 8.0 
    3. MySQL Workbench 8.0
    4. Postman


### Steps For Creating Spring Boot Project : 
    1. Open STS and navigate to "File" -> "New" -> "Spring Starter Project".
    2. Provide a project name and location.
    3. Choose Spring Boot version, language, packaging, and Java version.
    4. Select desired project dependencies.
    5. Configure project settings like group, artifact, and package names.
    6. Click "Finish" to create the project.
    7. Start coding your application logic in the generated project structure.


### Steps to Configure with Database :
    1. Add database dependencies
    2. Configure database connection details in the application.properties file , such as : 
        a. Database URL
        b. Database Username
        c. Database Password


### Project Structure : 
    1. Main -> Contains the Main File which is the starting point of the application for its execution.
    2. Entities -> Contains entity classes that represents the database tables.
    3. Services -> Contains all the service interfaces of the application.
    4. Repositories -> Contains all the repository classes to perform crud operations.
    5. Controllers -> contains all the controller classes that handles the HTTP requests
    6. DTOs -> contains all the (Data Transfer Object) classes for mapping data between the database and APIs.
    7. Config -> contains all the spring security configuration classes for filtering the HTTP requests and encrypt the password,etc.
    8. Security -> contains all the classes that manages all the operation regarding JWT token such as token generation, validation and handling unauthorized attempts, etc.
    9. Models -> contains the classes such as JwtRequest to generate a token and JwtResponse to get the generated token.

### Deployment :
To run this project 

    • Right click the SpringBootSocialMediaApplication.java file.
    • click Run option -> Click Run as Spring Boot App.
    • The application will be executed successfully.















## API Reference

### User
    All the endpoints of user API are public for all the users. 

#### Register User

```http
  POST /api/users/register
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `userDTO` | `UserDTO(Object)` | **Required**. This object contains various attributes of user such as name, email, password, role to register a user. |


#### Login User 

```http
  POST /api/users/login
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `loginDTO` | `LoginDTO(Object)` | **Required**. This object contains various attributes of user login such as email, password, role to authenticate a user. |


#### Get user data based on Authorization with optional sorting and optional pagination

```http
  GET /api/users/get-data
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `pageNumber` | `Integer` | **Optional**. Page Number for pagination _(Default Value = "1")_ |
| `pageSize` | `Integer` | **Optional**. Page Size to limit records per page _(Default Value = "5")_ |
| `sort` | `String` | **Optional**. Field name to sort data _(Default Value = "id")_|

#### Get data of specific user based on id

```http
  GET /api/users/get-data/{id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `long` | **Required**. Id of the user to get data of specific user. |

### Post 
    All the endpoints of Post API are protected which are not accesible without a proper authentication (i.e. JWT token).

#### Create Authentication Token 

```http
  POST /auth/create-authentication-token
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `jwtRequest` | `JwtRequest(Object)` | **Required**. This object contains attributes such as email and password to to authenticate a user and create JWT token for the user to access the endpoints of Post API. |


#### Create or Update a Post 

```http
  POST /api/posts/add-post
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `postDTO` | `PostDTO(Object)` | **Required**. This object contains various attributes of post such as title, content, userId to create or update a post. |

#### Save user response such as like or dislike

```http
  POST /api/posts/add-response
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `likeDislike` | `LikeDislike(Object)` | **Required**. This object contains various attributes such as postId, userId, userResponse to like or dislike a post. |

#### Get posts created by a user with numerous optional filters , optional sorting and optional paging

```http
  GET /api/posts/user/{id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `Long` | **Required**. Id of the user whose posts to be fetched |
| `pageNumber` | `Integer` | **Optional**. Page Number for pagination _(Default Value = "1")_ |
| `pageSize` | `Integer` | **Optional**. Page Size to limit records per page _(Default Value = "5")_ |
| `sort` | `String` | **Optional**. Field name to sort data _(Default Value = "id")_|
| `filterType` | `String` | **Optional**. Filter type such as greater than, less than, not equal to, like, etc. to filter fetched data |
| `filterBy` | `String` | **Optional**. Field name to sort data |
| `stringFilter` | `String` | **Optional**. String value to filter string data such as title, content, createdDate, updatedDate, etc. |
| `numericFilter` | `Long` | **Optional**. Numeric value to filter numeric data such as total_likes, total_dislikes, etc. |

#### Get specific number of top liked or disliked posts and optional for a specific user 

```http
  GET /api/posts/top-posts/{response}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `response` | `String` | **Required**. Response of user either like or dislike to get top liked or top disliked posts |
| `limit` | `Integer` | **Optional**. Limit to fetch specific number of liked or disliked posts |
| `userId` | `long` | **optional**. User id of user to get top liked or top disliked posts of a specific user|


## Screenshots

#### Register a User 
[![Screenshot-18.png](https://i.postimg.cc/05BnXSLT/Screenshot-18.png)](https://postimg.cc/w3DD71x2)

#### Login a User
[![Screenshot-19.png](https://i.postimg.cc/BnHjD899/Screenshot-19.png)](https://postimg.cc/mPZZWgg8)
