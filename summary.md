# icanhazdadjoke REST API

Use this API to get dad jokes from our database.

You can get a random joke, a specific joke, or you can search for jokes containing a specific term/phrase.

## What type of responses can the database give me?

You can ask the API for HTML, plain text or .json jokes, as well as .png images of joke text and Slack-compatible .json-formatted jokes.

### Random Joke in JSON

`curl -X GET -H "Content-Type: application/json" https://icanhazdadjoke.com/`

### Specific Joke in Plain Text

`curl -X GET -H "Content-Type: text/plain" https://icanhazdadjoke.com/j/5oWLeFdxkjb`

### Specific Joke as an Image

This returns a .png image of the joke's text.

`GET https://icanhazdadjoke.com/j/<joke_id>.png`

### Random Joke for Slack

This endpoint returns a random joke in a .json format which Slack easily understands. 

`GET https://icanhazdadjoke.com/slack`

## User agent

Please set the `User-Agent` header when sending requests to the API. This should include a way to contact you if necessary.

`"User-Agent: My Library (https://github.com/username/repo)"`

`curl -X GET -H "Content-Type: application/json"  https://icanhazdadjoke.com/graphql`