# Backend

## Recommended Reading

- [Node.js Tutorial for Beginners](https://www.youtube.com/watch?v=TlB_eWDSMt4)
- [What is an ORM?](https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/)
- [Typetta Documentation](https://twinlogix.github.io/typetta/)
- [Learn GraphQL](https://graphql.org/learn/)
- [Apollo GraphQL Documentation](https://www.apollographql.com/docs/apollo-server/getting-started/)

## Overview

The backend is built on Node.JS, Typetta, and MongoDB using Typescript. This uses GraphQL for communication with our various frontends, like our website, discord bot, etc. Like all of our other projects, it's written in Typescript.

Tools:

- MongoDB - Our database.
- GraphQL - An alternative communication method to REST, that allows users of the API to query exactly the data they need.
- Apollo GraphQL - A GraphQL client/server library
- Typetta - A Typescript ORM. We use Typetta to connect and interact with our MongoDB database. Typetta automatically creates a GraphQL endpoint, and provides per-column security on queries sent to that endpoint.
- Node.JS - An asynchronous event-driven Javascript runtime that lets you build network applications.
- Express.JS - A web server framework for Node.JS

## Contents

- [Config](config.md)
- [Structure](structure.md)
