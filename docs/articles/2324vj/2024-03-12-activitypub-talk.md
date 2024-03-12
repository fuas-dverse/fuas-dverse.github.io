# Talking ActivityPub

How can we make digital and human agents talk with each other? How can we build digital communities that can be linked together into a larger landscape? It is time to get familiar with the [[Fediverse]] and brush up on the [[ActivityPub]] protocols. All messages is described using the [[JSON-LD]] format for [[Linked Data]].

In this article I will sketch out some scenarios translated into these protocols. Concepts referenced: [[Fediverse]], [[ActivityPub]], [[JSON-LD]], [[Linked Data]].

## Introducing ActivityPub

ActivityPub consists of two layers: a federation protocol to share information between information servers and a client-server protocol. The latter is discussed here.

The basic concepts use a familiar metaphor: email. A user is called an "actor". Actors communicate by sending messages to their **outbox** and receiving messages through their **inbox**. In this project we deal with both human and digital actors. The latter are, infamously, called bots.

The ActivityPub protocol provides a standardised wrapper for transporting messages (Activity Stream messages) between actors. These messages are not limited to just content but can also express certain activities. We first need to discuss Activity Streams when we want to start exchanging meaningful messages.

![[2024-03-12-activitypub-talk 2024-03-12 15.21.59.excalidraw.svg]]

## Introducing Activity Streams

An action is a semantic description of an action.

Here is a simple note.

``` json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "summary": "A note",
  "type": "Note",
  "content": "My dog has fleas."
}
```

The `@context` tells a processor of this JSON that this is actually a JSON-LD document that uses the Activity Streams vocabulary.

In order to send the note we have to add sender (`attributedTo`) and recipient (`to`).

``` json hl_lines="3 4"
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "to": ["https://dverse.fontys.nl/ben"],
  "attributedTo": "https://dverse.fontys.nl/marc",
  "summary": "A note",
  "type": "Note",
  "content": "My dog has fleas."
}
```

For the remainder of this article I will write examples as YAML which makes them more easy to read.

``` yaml
"@context": https://www.w3.org/ns/activitystreams
to:
  - https://dverse.fontys.nl/ben
attributedTo: https://dverse.fontys.nl/marc
summary: A note
type: Note
content: My dog has fleas.
```

## Back to ActivityPub

Given the note above I now want to actually send it. For this I will POST it to some ActivityPub endpoint. This endpoint will notice the sender and recipient fields and create an ActivityPub wrapper around this message. It will also add IDs for traceability. This will then be send off to my outbox. When using an ActivityPub server you won't have to create this wrapper yourself.


``` yaml
"@context": https://www.w3.org/ns/activitystreams
type: Create
id: https://dverse.fontys.nl/marc/posts/12345
to: https://dverse.fontys.nl/ben
actor: https://dverse.fontys.nl/marc
object: 
  type: Note
  id: ttps://dverse.fontys.nl/marc/posts/12346
  attributedTo: https://dverse.fontys.nl/marc
  to:
    - https://dverse.fontys.nl/ben
  content: My dog has fleas.
```

The server will take messages from every outbox on the server and deliver it to the recipients inboxes.

> [!note] Chatty protocol
> One of the issues that servers face is that when they get more users the amount of work it has to do to keep up with all the activities results in a lot of messages being sent around. Suppose that I have 100 followers. This means that a message will go to 100 people's inbox. When 100 users each with 100 followers send out a single message the server will have to deal with 100 x 100 actions. Of course this can be alleviated by smart programming. In fact, an ex-Twitter engineer, Nathan Marz, has recently created a proof of concept Mastodon clone using a [data processing framework he developed](https://redplanetlabs.com/mastodon-clone) during the last 10 years and that demonstrates that it could, in principle, scale to Twitter scale.

## Actions

On most social networks users can perform other actions besides sending notes back and forth. These actions spell out the types of actions that can be performed. Not all servers support all of these. In theory we may also extend the vocabulary by adding new types of actions. Also, when designing a different type of social network server you could, for example, consider to not provide Likes, to get rid of the competitive elements and make the network less addictive[^maven]

But for now we will consider only these standard activities as most other servers probably implement them.

- Create
- Update
- Delete
- Follow
- Accept
- Reject
- Add
- Remove
- Like
- Announce
- Undo

[^maven]: ex-OpenAI researcher and professor [Kenneth Stanley](https://www.kenstanley.net/home) recently started such a different type of Social Media Network called [Maven](https://www.heymaven.com). He deliberately tries to make it less addictive by letting people follow interesting content rather than other people.

To be continued

