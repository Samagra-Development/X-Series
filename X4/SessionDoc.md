
# Expectations
- Understand technical integration documents for APIs
- Drafting requirements for APIs
- API Design and Development process
- Can PT members create APIs?

# API?

## 1. Messaging

   <img width="700" alt="whatsapp" src="https://user-images.githubusercontent.com/19550456/133410813-2dbb957b-44fd-4a1f-983d-e748eab12ba8.jpeg">


## 2. Payments

  ![upi](https://user-images.githubusercontent.com/19550456/133410881-3dd62fc0-ff6c-4b82-8dcb-34aab6f9a37a.png)


## 3. Recognise faces
   
  ![Screenshot 2021-09-15 at 1 10 57 PM](https://user-images.githubusercontent.com/19550456/133410903-d4fb498a-9269-40f4-bef7-2499a3528ed4.png)

  
 ## 4. Monitor disease symptoms
	 
  <img width="819" alt="movement-disorder-api-researchkit-02" src="https://user-images.githubusercontent.com/19550456/133410926-a84f8b71-5cf3-401a-a7ac-6ccf63644ae0.png">

	
## 5. Generate Memes

  ![Screenshot 2021-09-15 at 1 32 25 PM](https://user-images.githubusercontent.com/19550456/133414580-bae2fdaf-e615-403b-b3fd-bdf43c1d2c30.png)

    
## 6. [And even write code](https://openai.com/blog/openai-codex/)


Every software application – from word processors (**MS Word**) to operating systems (**Mac OS**) – exposes an API. 

Thus, there are many, many different forms of APIs . For the scope of today's discussion, we'll limit ourselves to **Web APIs.**

# What is a web API?

 >An **Application Programming Interface** is an intermediary between two separate software applications.

- Let's imagine ourselves at a restaurant.

- You go out to eat. Your intention is to be fed. 

- The food is being prepared in the kitchen, but **customers don't get access to the kitchen.**

- Your access to the kitchen is **via an employee of the restaraunt**.

- It is the job of this employee to ask you what you want and **get you that food from the kitchen.**

- The employee should get it in a way that is easy to consume - **not all at once.**

#### Thus, if the internet is a gigantic restaraunt, APIs are like the waiters.

Tthe principal task of an API on the web is, therefore, to be able to 
- **provide food** (*data*) 
- to **customers** (*external applications*) 
- without letting them into the **kitchen** (*database*)
- not all at once (*pagination*)

# The anatomy of an API

- [Notes](https://whimsical.com/api-JeWzFSeLWqRcTX2a97Kszc)


# Let's build our own API!
## Pre-Requisites: None!
- We'll follow along collaboratively on a playground server and the Postman Web UI.

- [Server](http://143.244.142.42:8080/)
  
  `Password: admin-secret`
  
- [Postman](https://www.postman.com/samagrax/workspace/x-series/)

  `Create an account and "Fork" the given "Collection"`

## *Optional*: Setup
- Install Docker on your system. Please refer this [link](https://github.com/Samagra-Development/X-Series/blob/main/X1/InstallationGuide.md) to setup docker on your machine.
- Install Loopback 4 CLI. Please use this [link](https://loopback.io/doc/en/lb4/Getting-started.html#install-loopback-4-cli) for instructions.
- Install [Postman](https://www.postman.com/downloads/)
-  Run the API server and database locally:
	- Clone this [repository](https://github.com/samagra-development/X-Series.git)
	- On the terminal,
	```
    cd X4 \
	docker-compose up -d --build
    cd api \
    npm run build \
    npm run migrate \
	npm run start
	```
	- Navigate to [http://localhost:3000/explorer](http://localhost:3000/explorer) 

## Challenge
![apiExercise](https://user-images.githubusercontent.com/19550456/133417165-d2a1624f-3c0e-4efb-b598-ed04e3f49ec4.png)


## Design
- [Notes](https://whimsical.com/api-JeWzFSeLWqRcTX2a97Kszc)


| Use Case      | Operation | Summary |
| ----------- | ----------- | ---------- |
| Create a new order      | **POST** `/order`       | creates an `order` entity |
| Delete an order   | **DELETE** `/order/:id`        | deletes `order` entity with id `id`|
| Fetch an order | **GET** `/order:id` | retrieves `order` entity with id `id` |


## Testing APIs: Postman

- **Postman** is a software application built for individuals and teams to be able to test APIs
	- Create **collections** and share them
	- Add **programmatic testing**
	- Import APIs in multiple formats, including **OpenAPI specifications** or even from code
	- Generate **documentation automatically** from a given API or collection

- **Postman Collection**: A set of APIs that are inter-related functionally and can be imported into Postman 


## Challenge: Advanced

Q1. Get all orders that belong to a particular `farmId`

A:

- This essentialy means running an SQL Query with a `WHERE` clause on our database. 

- Try it out: [Link](http://143.244.142.42:8080/console/data/sql)

- Answer: 

- How do we translate that to a REST API?

---
Q2. In the real world, the farm table will have more columns than just an id. 
Let's try and fetch all the farms (and all the columns inside them) which have

  - an order related to them 
  - of status "InProgress" 

in the database.

A:

- This essentialy means running an SQL Query with a `JOIN` clause on our database.

- Try it out: [Link](http://143.244.142.42:8080/console/data/sql)

- Answer: 
	
- Back to the drawing board.

  > ... but does this mean that we begin implementing a new API for every possible SQL query that we may want to run on our table?

### Enter GraphQL
- GraphQL, (**Graph** **Q**uery **L**anguage) is a relatively new-entrant in the world of API development.

- GraphQL relies on the consumer specifying the *query* ("**what they want**"), instead of *separate paths* handling the delivery of separate data.

- Think back to the restaurant example, and compare it to ordering online.

- Instead of asking multiple waiters for multiple different things, an online ordering application lets you **specify exactly what you want**.
 
 
- Let's come back to the question, and try and do it the GraphQL way.
 
 ### Hasura - Instant GraphQL APIs
 
 **Hasura** is a software application that overlays a database and provides instant GraphQL APIs that speak to that database, without having to write code.

### JOINs in GraphQL?

 - A `JOIN` is a concept that belongs to "relational" databases; it doesn't exist in graph-based databases since it doesn't need to. 

 - For a "graph-based" database, each table is a node; and tables are connected together via edges.

 - ![image](https://user-images.githubusercontent.com/19550456/133421643-590ed484-a0ef-463c-a059-f21945a1407b.png)
   
 - Hasura lets us implement GraphQL APIs on top of a "relational" database via  **relationships** between tables in the database

 - A GraphQL API is able to _follow relationships_ between tables, so fetching data from multiple tables is **simpler**.

### Building a relationship

- [What connects our two tables?](https://whimsical.com/api-JeWzFSeLWqRcTX2a97Kszc)  

- Let's [try](http://143.244.142.42:8080/console/data/default/schema/public/tables/order/modify) adding a relationship

## Challenge: Advanced - GraphQL Edition

- Let's write a GraphQL query to solve the question above.

- Answer: 

- Let's test it with Postman


## GraphQL vs REST: In Summary

| GraphQL | REST |
|--------- |----|
| GraphQL is like ordering online | REST is like a being in a restaurant with a buffet in it |
  You specify what you want, and you get exactly that | Everything is available - it's up to you to walk up to whatever you want and take it.
 | You pay for only what you get |  You pay for the whole thing |









