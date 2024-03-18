---
tags:
  - a/Article
aliases:
  - Talking ActivityPub
status: Draft
---


# Talking ActivityPub

How can we make digital and human agents talk with each other? How can we build digital communities that can be linked together into a larger landscape? It is time to get familiar with the [[Fediverse]] and brush up on the [[ActivityPub]] protocols. All messages is described using the [[JSON-LD]] format for [[Linked Data]].

In this article I will sketch out some scenarios translated into these protocols. Concepts referenced: [[Fediverse]], [[ActivityPub]], [[JSON-LD]], [[Linked Data]].

## Introducing ActivityPub

ActivityPub consists of two layers: a federation protocol to share information between information servers and a client-server protocol. The latter is discussed here.

The basic concepts use a familiar metaphor: email. A user is called an "actor". Actors communicate by sending messages to their **outbox** and receiving messages through their **inbox**. In this project we deal with both human and digital actors. The latter are, infamously, called bots.



![[activitypub-overview.png]]

The ActivityPub protocol provides a standardised wrapper for transporting messages (Activity Stream messages) between actors. These messages are not limited to just content but can also express certain activities. We first need to discuss Activity Streams when we want to start exchanging meaningful messages.

%% [[2024-03-12-activitypub-talk 2024-03-12 15.21.59.excalidraw]] %%


![[2024-03-12-activitypub-talk 2024-03-12 15.21.59.excalidraw.svg]]

## Introducing the vocabulary 


An activity is a semantic description of an past, present or future action.

Here is a simple note object.

``` json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "summary": "A note",
  "type": "Note",
  "content": "My dog has fleas."
}
```

The `@context` tells a processor of this JSON that this is actually a JSON-LD document that uses the [Activity Streams vocabulary](https://www.w3.org/TR/activitystreams-vocabulary).

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

> [!note] YAML syntax
> For the remainder of this article I will write examples as YAML and leave out the `@context` line. This makes these JSON messages easier to read.

``` yaml
to:
  - https://dverse.fontys.nl/ben
attributedTo: https://dverse.fontys.nl/marc
summary: A note
type: Note
content: My dog has fleas.
```

Describing objects is fine, but in order to share it with others we need to add some information and wrap it in a `Create` activity.

``` yaml hl_lines="1 2"
type: Create
object: 
  type: Note
  attributedTo: https://dverse.fontys.nl/marc
  to:
    - https://dverse.fontys.nl/ben
  content: My dog has fleas.
```

Given the note above I now want to actually send it. For this I will POST it to some ActivityPub endpoint. This endpoint will notice the sender and recipient fields and create an ActivityPub wrapper around this message. It will also add IDs for traceability. This will then be send off to my outbox. When using an ActivityPub server you won't have to create this wrapper yourself.

``` yaml hl_lines="2 3 4 7"
type: Create
id: https://dverse.fontys.nl/marc/activity/12345
to: https://dverse.fontys.nl/ben
actor: https://dverse.fontys.nl/marc
object: 
  type: Note
  id: ttps://dverse.fontys.nl/marc/note/12346
  attributedTo: https://dverse.fontys.nl/marc
  to:
    - https://dverse.fontys.nl/ben
  content: My dog has fleas.
```

## Back to ActivityPub

The server will take messages from every outbox on the server and deliver it to the recipients inboxes.

- [Client to Server Interactions](https://www.w3.org/TR/activitypub/#client-to-server-interactions)
- [Server to Server Interactions](https://www.w3.org/TR/activitypub/#server-to-server-interactions)


> [!note] Chatty protocol
> One of the issues that servers face is that when they get more users the amount of work it has to do to keep up with all the activities results in a lot of messages being sent around. Suppose that I have 100 followers. This means that a message will go to 100 people's inbox. When 100 users each with 100 followers send out a single message the server will have to deal with 100 x 100 actions. Of course this can be alleviated by smart programming. In fact, an ex-Twitter engineer, Nathan Marz, has recently created a proof of concept Mastodon clone using a [data processing framework he developed](https://redplanetlabs.com/mastodon-clone) during the last 10 years and that demonstrates that it could, in principle, scale to Twitter scale.

## Actions

On most social networks users can perform other actions besides sending notes back and forth. These actions spell out the types of actions that can be performed. Not all servers support all of these. In theory we may also extend the vocabulary by adding new types of actions. Also, when designing a different type of social network server you could, for example, consider to not provide Likes, to get rid of the competitive elements and make the network less addictive[^maven]

But for now we will consider only these standard activities as most other servers probably implement them.

**Create**

: Create the activity in the actor's inbox

**Update**

: Update an object based on its ID.

**Delete**

: Delete an object  based on its ID.

**Follow**

: Generates an **Accept** or **Reject** depending if the other actor accepts the follow or not.

**Accept**

: Accepting a **Follow** object adds that user to my **Following collection**.

**Reject**

: Rejecting a **Follow** object with not add that user to my **Following collection** but it may result in some sort of notification.

**Add**

: Adds an object to a collection.

**Remove**

: Removes an object from a collection.

**Like**

: Increments the likes count by adding to the **Likes collection**.

**Announce**

: Increment the shares count by adding to the **Shares collection** (this is like sharing, reposting, boosting or retweeting).

**Undo**

: Undo the side effects of previous activities.

[^maven]: ex-OpenAI researcher and professor [Kenneth Stanley](https://www.kenstanley.net/home) recently started such a different type of Social Media Network called [Maven](https://www.heymaven.com). He deliberately tries to make it less addictive by letting people follow interesting content rather than other people.

To be continued

> [!NOTE] @context
> From here on I will leave the `@context` out of the examples. We assume it's set to `https://www.w3.org/ns/activitystreams`.


## Questions and Answers

When talking to chatbots it is often in the question and answer style. Let's represent that in ActivityPub.

``` yaml
id: http://dverse.fontys.nl/question/1
type: Question
content: Can I talk to you about my cat?
```

``` yaml
id: http://dverse.fontys.nl/question/1
type: Question
content: I would like to build a robot to feed my cat. Should I use Arduino or Raspberry Pi?
oneOf:
  - name: Arduino
  - name: Raspberry Pi
```

There is no Answer activity type. If you would allow multiple answers you can replace `oneOf` with `anyOf`.

This is how an answer would look.

``` yaml
attributedTo: http://dverse.fontys.nl/bot/sally
inReplyTo: http://dverse.fontys.nl/question/1
name: Arduino
```

It is better to keep question and answers together though.

``` yaml
id: http://dverse.fontys.nl/question/1
type: Question
content: I would like to build a robot to feed my cat. Should I use Arduino or Raspberry Pi?
oneOf:
  - Arduino
  - Raspberry Pi
replies:
  type: Collection
  totalItems: 3
  items:
    - attributedTo: http://dverse.fontys.nl/bot/sally
      inReplyTo: http://dverse.fontys.nl/question/1
      name: Arduino
    - attributedTo: http://dverse.fontys.nl/bot/joe
      inReplyTo: http://dverse.fontys.nl/question/1
      name: Arduino
    - attributedTo: http://dverse.fontys.nl/bot/john
      inReplyTo: http://dverse.fontys.nl/question/1
      name: Raspberry Pi
result:
  type: Note
  content: 33% of the bots selected Rasberry Pi.
```

Note that some of these examples do have some redundancy. This is to allow unpacking and still containing a full object.

- ! How to visualise inboxes.

- Email analogy
- HTTP verbs -> Activity types

## Getting started with Python and ActivityPub

Most of the code you need to write is working with [JSON-LD messages](https://github.com/digitalbazaar/pyld) and transforming them. Other than that you will need a basic [ActivityPub library](https://github.com/dsblank/activitypub). 

There are also [ActivityPub server related repos](https://github.com/topics/activitypub-server?l=python) that you can use to learn how to make a full, working server and a [full-fledged server](https://github.com/jointakahe/takahe).
