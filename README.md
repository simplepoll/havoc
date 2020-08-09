# havoc
Havoc is a plumbing service that sits in between Slack and your Slack app

_README Driven Development_


## Purpose

The overall purpose of havoc is to take on the vast majority of plumbing work that most Slack apps need to currently deal with as they do various interactions with the Slack APIs.

In a world where havoc works, Slack developers can focus more of their energy on building value-providing business logic, as opposed to on the Slack API plumbing work around that logic.

## Principles
- Abstract client-side complexity
- Speed matters
  - P99 latency must stay under 200ms
- Open source, run by yourself on your own infrastructure


## Who is this for?

Advanced, state-storing Slack apps which do many complex interactions with the Slack API


## Architecture

havoc sits in between the Slack API and your Slack application. Any communication between your Slack application and the Slack API passes through Havoc

![architecture sketch](https://user-images.githubusercontent.com/7718702/89741521-e7a5d100-da89-11ea-9f25-d0fbeb3033f4.jpeg)


## Features
- Store Slack entities that your app may need to keep track of (users, workspaces, bots, channels, etc.) and their relation to your tables
  - Keep track of every message sent with chat.postMessage in case you ever need to update or delete that message in the future
  - Based on the data in each event (block_actions, view_submission, etc. etc), help you understand which user took the action, which workspace they're a member of, etc.
- Log everything by default (incoming events, outgoing API calls)
- Working OAuth implementation
- Validation of incoming message legitimacy



## Ownership

In a perfect world Slack would build, develop, and own this service

Doing this would actually be quite beneficial in giving the right teams insight into the challenges faced by Slack developers in building on top of the Slack platform. Especially those challenges around data modelling, working around inconsistencies, novel Slack features (enterprise grid & shared channels), and other client side complexity.

This would be useful not just in learning about potential improvements to make on the server (API/platform) side but also better help the community deal with any complexity that necessarily needs to live in the client (Slack app) implementation



## Deployment

Two deployment modes

**In-network**
- Faster, more secure
- Should be default for production-grade applications (like Simple Poll)
- Uses RPC to make requests from Havoc to App
- Downside: More complex setup, doesn’t work on Heroku

**Hosted**
- Less performant
- Required to work on Heroku
- Uses HTTPS to make requests from Havoc to App
- Maybe default on local?

