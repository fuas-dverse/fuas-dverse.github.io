# Concept Library

[[Activitypub]]

This library of concepts represents our knowledge base and is meant to share the technical and theoretical ideas that are helpful to the development of our projects. They also help guide our future research into Digital Communities.

> [!important]
> Being a library means that there is a lot more stuff than you can consume. This is not a syllabus. It's more like an all-you-can-eat buffet. Take just as much and only what you want. :wink:

Each concept has an introduction and some pointers to other information. They often represent a much larger area of interest and are often related to other concepts which will be indicated by little graphs.

You can contribute your own links via our [Raindrop collection](raindrop.md), provide a [PR](pull-request.md) to suggest your own concepts, or start a discussion by creating an [issue](issues.md) for it.

- [ActivityPub](concepts/activitypub.md)
- [Fediverse](concepts/fediverse.md)
- [Linked Data](concepts/linked-data.md)
- [Databases](concepts/databases.md)
- [Graph Data](concepts/graph-data.md)
- [Large Language Model](concepts/large-language-model.md)
- [Retrieval Augmented Generation](concepts/retrieval-augmented-generation.md)
- [Set-based Design](concepts/set-based-design.md)
- [JSON-LD](concepts/json-ld.md)
- [Multi-agent System](concepts/multi-agent-system.md)
- [Distributed Artificial Intelligence](concepts/distributed-artifical-intelligence.md)
- [Data Mesh](concepts/data-mesh.md)
- [GraphQL](concepts/graphql.md)



``` mermaid
graph TD;
  LD[Linked Data];
  JLD[JSON-LD];
  GR[Graph Data];
  LD-->JLD;
  LD-->GR;
  GR-->JLD;
  JLD-->GR;
```
