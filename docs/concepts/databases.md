# Databases

The database landscape is continuously changing, there are hundreds of different database systems. Different types of data and use cases require different ways of storing it. When looking around there are some that offer quite amazing functionality.

> [!tip]
> Especially in the beginning stages of the project don't obsess over details, especially not over performance. Details are important but can slow your exploration down. You can always change your mind later, once you know more about what you need to store and which functionals or non-functionals are important for your particular use case. Do a quick scan of a product that looks suitable, maybe there are USPs that you may latch onto, but then go .... try them it. And you may also want to try something different.

Databases may be categorized in various ways. Here's one. A specific database may fit in multiple categories.

- Relational
- NoSQL
- In-memory
- Columnar
- Time Series
- NewSQL
- Object-Oriented
- Graph
- Search Engines
- Spatial
- Document
- Distributed
- Cloud

For this project, here are some personal picks and why I like them. But don't take my word for it, do your own experimentation.

| Affordance | Databases |
| ---- | ---- |
| Store graphs, social graphs, knowledge graphs. | Neo4j, Datomic |
| Never delete/loose data, like Git does. | Datomic, XTDB |
| Superflexible schema. Add any data you like, with or without schema. | Neo4j, Datomic, XTDB, SpaceTimeDb |
| Concept of time built in? Time-travel.  | Datomic, XTDB |
| Proven massively scalable, like MOOC-size and games. | SpaceTimeDb |

