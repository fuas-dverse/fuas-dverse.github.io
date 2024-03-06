# JSON-LD

> [!QUOTE] Wikipedia
> JSON-LD (Javascript Object Notation for Linked Data) is a method of encoding linked data using JSON.

- It is regular JSON.
- You can take your current JSON and make it JSON-LD.
- Express graph (or tree) structures.
- JSON Context defines the mapping from JSON to the Linked Data model.
- It is the data encoding used by [ActivityPub](ActivityPub.md)


=== "JSON"

	``` json title="people.json"
	{
		"name": "John Smith",
		"homepage": "https://www.example.com"
	}
	```

=== "JSON-LD"

	``` json title="people.jsonld"
	{
		"@context": "context.jsonld",
		"@id": "https://me.example.com",
		"@type": "Person",
		"name": "John Smith",
		"homepage": "https://www.example.com/"
	}
	```

=== "JSON-LD Context"

	``` json title="context.jsonld"
	{
		"name": "http://xmlns.com/foaf/0.1/name",
		 "homepage": {
			 "@id": "http://xmlns.com/foaf/0.1/workplaceHomepage",
			 "@type": "@id"
		 },
		 "Person": "http://xmlns.com/foaf/0.1/Person"
	}
	```

