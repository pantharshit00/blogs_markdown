The official documentation of [PassportJS](http://passportjs.org) is quite confusing for SQL based database system as its documentation contains the model function of mongoDB's ORM mongoose. Once it took me a while to implement it in a postgreSQL project using only node [pg](http://npmjs.org/package/pg) package. Then I came across with a awesome npm package called [Sequelize](http://sequelizejs.com) which is a Object Relation Mapper for SQL based databases like MySQL ,Postgres, SQLite, msSQL etc. It provide functions for SQL queries which is quite handy. I recommend to watch this [playlist](http://bit.ly/2ox7hId) to learn more about sequelize.

<hr>

### Lets code a auth system with passport using postgreSQL

#### Prerequisites

1. You have to be familiar with passport and its local strategy.
2. Obviously you need to know node and some basics of db handling.

<hr>

#### Our user model

<script src="https://gist.github.com/pantharshit00/c7f977a50f07e930fb9652340349fb45.js"></script>

In this example we are first bringing in `sequelize` using node `require`. Then we are defining the `connection` variable and setting it to the `Sequelize constructor`. The constructor takes 4 parameters first one is `database name`, second one is `username`, third one is `password` and last one is an object of `options`. In options we had defined the `dialect` to be postgres and `host` which is the address where the server of database is located. Then we are defining the `User` model which is equivalent to table in the database. We are using the `define` function for it which takes `name` and a object of `columns` as parameters. Each member of the object is a column in the table of DB. We can define column type by using sequelize. It also provide all options like `primary key`, `auto increment` etc. Then after we are connecting and syncing with the database. It will create the table if it doesn't exists in the database. At last we are exporting the `User model` for our use in the application.

<hr>

#### Our express server

<script src="https://gist.github.com/pantharshit00/f9b5c41844bfbfe7df3d1bdb25d1e004.js"></script>  

In this example we are first just importing some `dependencies` and setting up some `middlewares`. That stuff should be familiar to you. We are using `express-session` and `body-parser` middlewares. Come to the part where we are setting up our passport strategy. We are calling `passport.use()` which takes a passport strategy object. In this case `localStrategy`. `LocalStrategy` take a function with all the fields required and a `callback` function done. Then we are using the `sequelize model` function `findOne()` which takes an object of options . Here in options we are specifying `where` email = provided email. SQL query it makes is `SELECT * FROM <tablename> WHERE email= <provided email> LIMIT 1;` It returns a `promise` with the data retrieved. Then we are checking for the user if it is null. If null so we are sending no user and no error in the callback. Then we are checking the password. You should use hashed password checking logic here for security. Some of password hashing libraries are `bcrypt, crypto etc`. If password do not match we will return no user. At last if all goes right we are return user with no error in the callback. Then there is standered passport `serialize and deserialize function`. But in `deserialize` we are using sequelize `findOne()` function as we have done above. Then there is a `post`request handler of express using passport middleware for authentication. Then we have a middleware function for `auth guard`. This function take `request, response and call next middleware` as parameters. In this we are checking if request contains the user then we are going to call next middleware else we are responding with `forbidden status`(**403**) with a unauthorised message. Then we have a protected route using this middleware. Then we have a logout route calling `request.logout()` when executed to log the user out and then send a success message. At last we are starting the app the to listen on `port` 3000._**Tip:-** Use [Postman](http://bit.ly/1HCOCwF) to test the apis._

<hr>

#### Package.json file if anyone needs it

<script src="https://gist.github.com/pantharshit00/bbacc39b6bc25c3755707b47e195a1ba.js"></script>

<hr>

#### I recommend to watch this [playlist](http://bit.ly/2ogl7zx) if you don't know how to use passport.
