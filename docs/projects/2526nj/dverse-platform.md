## Platform Architecture

You are the platform team. You develop an architecture for a social media platform that will enable users to run collaborative team games.

There are two important architectural styles or paradigms you can work with:

- Event-Driven Architecture (EDA)
- Actor-Model

Important links:

- [COMMONS Website](https://www.commons.nu)
- [DVerse Website](https://fuas-dverse.github.io) including results and papers from previous challenges
- [DVerse GitHub](https://github.com/fuas-dverse) our code
- COMMONS: [Paper 1](https://www.researchgate.net/publication/335449476_COMMONS_A_Board_Game_for_Enhancing_Interdisciplinary_Collaboration_When_Developing_Health_and_Activity-Related_Wearable_Devices), [Paper 2](https://research.tue.nl/nl/publications/designing-for-an-active-lifestyle-facilitating-interdisciplinary--2)
- DVerse: [Paper 1](projects/2425nj/nils.md), [Paper 2](projects/2425nj/oliver.md)

## Introduction

DVERSE (https://fuas-dverse.github.io) is a vision of a social network for diverse intelligences (human and artificial). The bots have to become more social and be able to work in a group together with humans.

This project is part of the Interaction Design research group and the Digital Communities program. This program is about human-centered, social design using digital technology and AI.

## Assignment

This challenge aims to _provide advice and ideas_ for the future of the platform architecture for DVERSE in the form of Proof of Concepts.

The basic idea for how users interact with DVERSE is that they use a frontend chat client that is connected over Websockets to a group of other users forming a room. The backend hosts many of these rooms or chat spaces and users are free to walk around to any of the other rooms. Each room may have a different focus and different bots for different purposes.

In the first few weeks we will do a couple of workshops to specify the platform prototypes, we will also choose a suitable demo use-case scenario and we will develop the criteria for evaluating the prototypes.

Two platform Architectures:

- For a couple of semesters we have worked with an **Event-Driven Architecture** using Python and the Nats message broker (previously Kafka). This seems to be a good architecture.
- Recently the researchers have also looked at an **Actor-based** architecture using the Elixir language. Elixir is based on Erlang and is famous for running large distributed (telco-)systems with many concurrent, lightweight, processes while offering a platform with an uptime of nine-nines (99.9999999%).

We want to see simple proof of concepts for either one of the architectures (frontend and backend). There is also room to focus on specific aspects such as observability, performance, UI etc.

## Tech Stack

For the event-driven architecture:

- Python
- Nats.io (message broker)
- AI framework and libraries
- Matrix, Mastodon or custom client

For the actor-model architecture:

- Elixir (and Python) with Phoenix
- AI framework and libraries
- Matrix, Mastodon or custom client
