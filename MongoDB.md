# MongoDB

**Definition**  
A NoSQL database application (non-relational document database). It stores data records as structured or unstructured objects called documents,described in BSON (a binary representation of data) and retrieved by applications in a JSON format. These documents are grouped in collections - similar to tables in relationship databases. A database stores one or more collections of documents.

One document can have other documents embedded in it. New documents are assigned a UUID unique to that collection. Inside the document, the fields are defined and can be a variety of data types. Field are equivalent to columns in a SQL database - can be indexed to increase search performance.  
```json
{
  "_id": 1,
  "name": {
    "first": "Ada",
    "last": "Lovelace"
  },
  "title": "The First Programmer",
  "interests": ["mathematics", "programming"]
}
```
- use QueryAPI for operations such as basic READ/WRITE and complex transformations across the database.  
- use secondary indexes to optimise performance (make common queries faster).
- use geo-spatial queries to find documents near a geographic location.
- use aggregation pipelines to group documents together and return a single result.

Unlike a relational table, a predefined schema for a collection is optional => can change data structure without complex database migrations and allows frequently accessed data to be stored in the same place => READ operations are quicker since no joins are required.

Supports Horizontal Scaling (divide dataset and load over multiple servers) via 'sharding' - a method for distributing data across multiple machines to support deployments with large datasets and high throughput operations.

MongoDB Atlas - free to use, scales automatically and provides a UI to interact with data - https://www.mongodb.com/docs/guides/

## Setup
1. Make account on MongoDB Atlas - platform to spin up MongoDB servers on the cloud.  
i. Create organisation > project > build a database > choose free one (closest/lowest ping), cluster0. Note down username and password!  
ii. once you set up a new database, you need to allow a set number of IP addresses that can access that server. Use your own IP address.  
iii. replace `<password>` with your password > Name > Save and connect.

2. Admin and local are default and come with all clusters - we can ignore them. Next to database click the + > Database Name > Collection name

3. In `application.properties` add this. We leave it to be populated since it has sensitive information.
    ```properties
    # match it to the name of your db
    spring.data.mongodb.database=${MONGO_DATABASE}
    #uri to your mongo cluster
    spring.data.mongodb.uri=mongodb+srv://${MONGO_USER}:${MONGO_PASSWORD}@$ {MONGO_CLUSTER}
    ```
4. Create a `.env` file under resources. Fill in your details.
    ```properties
    MONGO_DATABASE=""
    MONGO_USER=""
    MONGO_PASSWORD=""
    MONGO_CLUSTER=""
    ```
5. Add `.env` file to `gitignore` - to make sure you don't accidentally commit and open your database to the world.

NOTE - spring doesn't support `.env` files out of the box, so get the Spring Dotenv from https://mvnrepository.com/, add to pom.xml and reload maven.