---
layout: page
title: "API Summary"
permalink: /docs/general
---

Use this API to get dad jokes from the icanhazdadjoke database.

You can get a random joke, a specific joke, or you can search for jokes containing a term or phrase.

To test the search endpoint, you can use our [API explorer](https://handoniumumumum.github.io/icanhazdoctest/swagger).

## What is a dad joke?

A dad joke is an obvious pun. Here is an example: "I used to be a banker, but I lost interest."

They are often told by dads, but they *can* be enjoyed by anyone.

## What type of responses can the database give me?

You can ask the API for HTML, plain text or .json-formatted jokes, as well as .png images of joke text and Slack-compatible json-formatted jokes.

### Random Joke in JSON

```bash
curl -X GET -H "Content-Type: application/json" https://icanhazdadjoke.com/
```

### Specific Joke in Plain Text

```bash
curl -X GET -H "Content-Type: text/plain" https://icanhazdadjoke.com/j/5oWLeFdxkjb
```

### Specific Joke as an Image

This returns a .png image of the joke's text.

```bash
curl -X GET https://icanhazdadjoke.com/j/<joke_id>.png`
```

### Random Joke for Slack

This endpoint returns a random joke in a .json format which Slack easily understands. 

```bash
curl -X GET https://icanhazdadjoke.com/slack
```

## User agent

Please set the `User-Agent` header when sending requests to the API. This should include a way to contact you if necessary.

`Tutorial User (https://handoniumumumum.github.io/icanhazdoctest/`

```bash
curl -X GET -H "Content-Type: application/json" -H "Tutorial User (https://handoniumumumum.github.io/icanhazdoctest/" https://icanhazdadjoke.com/graphql`
```

## Authentication

This API doesn't have an authentication requirement.