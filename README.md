# API Usage Guide: College AI Chat

This document explains how to use the `/generate` API endpoint for the College AI Chat application. This API allows you to send a user's question (prompt) along with a unique college identifier (iid) to generate a response.

## Endpoint

`POST https://prj-onllineeducationexpo.de.r.appspot.com/generate`

## Request Body

The request body must be in JSON format and include the following two fields:

-   `iid`: A unique identifier for the college. This is a string value.
-   `prompt`: The user's question or prompt. This is also a string value.

Here's an example of a request body:

```json
{
  "iid": "1001",
  "prompt": "What courses are offered at Karunya University?"
}
```

### College Identifiers (iid)

Each college is assigned a unique identifier. Here's a list of the available colleges and their corresponding iids:

-   Karunya: `1001`
-   Dhanalakshmi Srinivasan University: `1002`
-   VIT: `1003`
-   KARE: `1004`
-   VelTech: `1005`
-   AVV: `1006`
-   AU: `1007`

## Request Example

Here's an example of how to make a POST request to the `/generate` endpoint using JavaScript's `fetch` API:

```javascript
const iid = "1001"; // College Identifier
const prompt = "Tell me about the engineering programs."; // User's question

fetch('https://prj-onllineeducationexpo.de.r.appspot.com/generate', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ iid, prompt })
})
.then(response => response.json())
.then(data => {
  console.log(data.generatedText); // The generated response from the API
})
.catch(error => {
  console.error('Error:', error);
});
```

## Response

The API returns a JSON response containing the generated text. The response structure is as follows:

```json
{
  "generatedText": "The response from the AI based on the prompt and college ID."
}
```

-   `generatedText`: The generated response from the AI. This is a string value.

## Displaying the Response in the UI

To display the response in the UI, you can use JavaScript to update the content of an HTML element. For example:

```javascript
// Assuming you have an HTML element with the ID 'chatBody'
const chatBody = document.getElementById('chatBody');
chatBody.textContent = data.generatedText; // data is the parsed JSON response
```

Alternatively, you can use the `appendMessage` function from the existing code to display the response in the chat interface:

```javascript
appendMessage(data.generatedText, 'bot'); // 'bot' indicates the message is from the AI
```

## Error Handling

If there is an error processing the request, the API might return an error message or a generic error. Make sure to include error handling in your code to gracefully handle such cases.

```javascript
fetch('https://prj-onllineeducationexpo.de.r.appspot.com/generate', {
  // ...
})
.then(response => {
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  return response.json();
})
.then(data => {
  // ...
})
.catch(error => {
  console.error('There was an error!', error);
});
```

## Summary

1.  Make a `POST` request to `https://prj-onllineeducationexpo.de.r.appspot.com/generate`.
2.  Include `iid` (College Identifier) and `prompt` (User's Question) in the JSON request body.
3.  Parse the JSON response to get the `generatedText`.
4.  Display the `generatedText` in the UI using JavaScript.
5.  Implement error handling to manage potential issues.