# Database

## Recommended Reading

-   [What is a Database?](https://www.oracle.com/database/what-is-database)
-   [Introduction to MongoDB](https://www.mongodb.com/docs/manual/introduction/)
    -   Explains the overall structuring of MongoDB a NoSQL database
    -   Ex. documents make up collections, which make up databases.
-   [SQL Tutorial - Full Database Course for Beginners](https://www.youtube.com/watch?v=HXV3zeQKqGY)
    -   Despite using MongoDB, a NoSQL database, we are still using the database like a traditional SQL one. We use collections as tables, and documents with fixed fields.

## Overview

We use MongoDB as our database. Specifically, we use MongoDB's cloud database service called MongoDB Atlas. MongoDB Atlas provides a cluster of databases, so it adds a layer of redundancy in case one database fails. We have a `RUCOGS` organization on Atlas. Underneath Atlas we have a `rucogs.github.io` project, and within that is `MainDB` -- our entire database. We currently use the free-tier of MongoDB, which gives us 512 MB of free storage.

Files are not stored on databases, since that would be wasteful. Instead, files are often uploaded to dedicated servers, with database entries only containing a link that can fetch the file from the server. The files for our backend are stored within the backend. See [backend section](../backend/index.md) for more information.

## Database Schema

![Database Schema](../images/dbschema.png)

!!! note

    It's important to pass on access of the database as new Webmasters replace old ones.

    Members with access to Database as of **4/2/24**:

    - Nihal Pinto (Discord: `illuminoeye_gaming`)
