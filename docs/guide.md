---
layout: page
title: "Getting and Keeping a Joke"
permalink: /docs/guide
---

# Getting and Keeping a Joke

This guide will show you how to get a random joke, then retrieve it again later as a .png file using multiple endpoints of the API. You can use the same workflow to retrieve jokes as text or json with simple tweaks.

Code examples are provided using C# and curl commands.

## Get the Joke

**Step 1:** A random joke is the default response to calling the base endpoint. So, to get a random joke, we will call the base endpoint without any parameters.

### Code Example

Here's an example of how to get a random joke using the C# `HttpClient` to call our API:

```csharp
public static async Task<string> GetDadJokeAsync()
{
  string url = "https://icanhazdadjoke.com/";
  HttpClient client = new HttpClient();
  client.DefaultRequestHeaders.Add("Content-Type", "application/json");
  client.DefaultRequestHeaders.Add("User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)")
  HttpResponseMessage response = await client.GetAsync(url);
  return response;
}
```

Below is the same request formatted as a curl command:

`curl -X GET -H "Content-Type: application/json" -H "User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)" https://icanhazdadjoke.com/`

**Step 2:** Look at the response. Here is an example of a random joke response you could receive:

```csharp
{
  "id": "R7UfaahVfFd",
  "joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike away.",
  "status": 200
}
```

In order to retrieve the joke again, you will need the `id` of your joke from this response.

**Step 3:** Call the endpoint for a specific joke, the `j` endpoint. We will request a photo of the joke this time.

Use the joke's id and add the `.png` file extension as your path parameter following the `j` segment of the URL, as shown in the example below:

### Code Example

Here's an example of how to get a specific joke as a png image using the C# `HttpClient` to call our API:

```csharp
public static async Task GetSpecificDadJokeImageAsync()
{
  string jokeId = "8USSSfVn3ob";
  string fileName = fileName + ".png";
  string url = "https://icanhazdadjoke.com/" + fileName;
  HttpClient client = new HttpClient();
  client.DefaultRequestHeaders.Add("User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)")

  // Download the png and save it as a file.
  var imageBytes = await client.GetByteArrayAsync(uri);
  await File.WriteAllBytesAsync(appDomain.CurrentDomain.BaseDirectory + fileName, imageBytes);
  return;
}
```

Below is the same request, formatted as a curl command:

`curl -X GET -H "User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)" https://icanhazdadjoke.com/j/<joke_id>.png`

You can get a text version of this joke from the same endpoint by removing `.png` from the end of the URL.

## Search for the Joke Later

If you've lost the joke's id, but you want to find it again, you can search for it using words in the joke.

You can use either the REST API or the GraphQL endpoint. 

This guide will show you how to search for a joke using the REST API endpoint and C# code.

**Step 1:** Find the endpoint for the REST API search function, `/search/`. 

`https://icanhazdadjoke.com/search`

**Step 2:** Add your search word or phrase as the `term` parameter in the query string of the request URL. In this example, the term parameter is "momentum".

`https://icanhazdadjoke.com/search?term=momentum`

**Step 3:** Send the request to the endpoint, making sure to request `application/json` as the response type so that the joke's id is supplied with any matches.

### Code Example

```csharp
public static async Task SearchDadJokesAsync(string searchTerm)
{
  string url = "https://icanhazdadjoke.com/";
  // Add the query string to the URL
  string urlWithQuery = url + "?term=" + searchTerm
  HttpClient client = new HttpClient();
  client.DefaultRequestHeaders.Add("User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)")
  client.DefaultRequestHeaders.Add("Content-Type: application/json");
  // Return the response, which will contain a SearchResult object as .json
   HttpResponseMessage response = await client.GetAsync(url);
}
```

Below is the same request, formatted as a curl command.

`curl -X GET -H "Accept: application/json" -H "User-Agent: Cuyahoga Library (https://cuyahogalibrary.org/)" https://icanhazdadjoke.com/search?term=momentum`

**Step 4:** The request will return any jokes which have text matching your `term`, along with their id. If you got a result, find the id of the joke you're searching for.

Here is an example response from `search` as json, containing a single result:

`{"current_page":1,"limit":20,"next_page":1,"previous_page":1,"results":[{"id":"8USSSfVn3ob","joke":"I've been trying to come up with a dad joke about momentum . . . but I just can't seem to get it going."}],"search_term":"momentum","status":200,"total_jokes":1,"total_pages":1}`

The id will be located in the `results` property of the response with the joke's text. In this example, the `id` is `8USSSfVn3ob`.

**Step 5:** You can call the `j` endpoint for the joke using its `id`. Here is an example using curl and the joke we just retrieved:

`GET https://icanhazdadjoke.com/j/8USSSfVn3ob`