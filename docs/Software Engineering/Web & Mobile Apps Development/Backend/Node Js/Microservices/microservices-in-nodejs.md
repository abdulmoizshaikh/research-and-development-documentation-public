# Learn microservices in nodejs

**monolithic server**

![image](./images/image17.png)

Conventional way for building servers

In monolithic server we have all our code needed to implement our application inside of one single codebase and we deploy that code base as one discrete units

![image](./images/image5.png)

**Where as micro services ?**

A single microservice contains all of the routing all the middlewares, all the business login and database access required to implement one feature of our application that is the big difference

So a monolithic has all the code needed to implement every feature of our application
A microservice has the coded needed to implement just one feature

![image](./images/image16.png)

### Microservice architecture

![image](./images/image2.png)

Each of these services are entirely self contained

A microservice has all things which includes separate database as well
Nice thing about this approach is that if for some reason if every other feature or every other service inside of our application crashes a portion of our app is still going to work just fine

A service A is 100% stand alone and doesn’t necessarily require for any other service to work correctly

Big problem.

**Data management between services .**

Example.

![image](./images/image4.png)

![image](./images/image15.png)

**Database per service (one database on service only architecture)**

E.g

![image](./images/image3.png)

![image](./images/image8.png)

![image](./images/image14.png)

![image](./images/image12.png)

![image](./images/image10.png)

Point 5 e.g

![image](./images/image11.png)

Point 6 eg

Web of dependencies

![image](./images/image6.png)

**Async communication: (not recommended)**

E.g

![image](./images/image13.png)

Not best solution because all these issues coming in sync communication persist in Event bus method we got an other solution which we will often and cover in next lecture

![image](./images/image10.png)

![image](./images/image9.png)

![image](./images/image1.png)

![image](./images/image7.png)
