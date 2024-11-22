# Developer Experience Assessment

Welcome to this assessment!

You will find below the instructions to complete for your work assessment:  you will have to develop a Python library that interacts with a ReST API, keeping in mind to offer a great developer experience to whoever uses it.

## Understanding the API

You can find the OpenAPI Specification for this API in YAML at the following location: ./docs/openapi.yaml

Typically, such YAML file is not meant to be read by an API user but rather to be processed by a specification viewer such as SwaggerUI or Redocly. You're in luck, we have prepared both tools for you!

### Browsing the API

1. Clone this repository
2. Navigate to the root of the cloned repository on your local machine
3. If not yet installed, install Docker on your machine
4. Execute the command `docker compose up`

This command will start 3 servers locally:
 - http://localhost:8080 => Swagger UI
 - http://localhost:8090 => Redocly
 - http://localhost:3000 => the API server, using a local database

Up to you to choose which UI to use to browse the API.

### API explanations

The API is a very simple messaging API where a user can:
 - manage contacts (`create`, `update`, `get`, `list` and `delete`)
 - `send` a message to a contact (this is just a simulation, no real message will be sent)
 - `get` details about a sent message, `list` all the sent messages

### Authentication

All the endpoints are protected by an API Key: your recruiter will give it to you.

When sending a message to the API, all requests must contain the following header: `Authorization: Bearer YOUR_API_KEY`

## Your tasks

### Implement a SDK in Python

With the developer experience in mind, create a Python library that can be used to interact with the API. With this library:
 - a user should not care about specifying the authentication header for every requests
 - a user should be able to “auto-discover” the API parameters thanks to the auto-completion in the IDE
 - a user should be able to use all the API methods without having to know their path or their HTTP method

### Test your SDK

Make sure to include some tests in your submission! We would love to discuss with you how you make sure your code is working.

## Bonus tasks

You may have noticed that when you send a message, the status is set to `queued` but after a while, the status becomes `failed`. This API simulates a sending queue and will considered that the message is properly delivered if there is a server that acknowledges the delivery.

In order to do so, you will need to use the last section of the API: the webhooks. When you send a message, the API server will send a request to a WEBHOOK_URL(default http://localhost:3010) and include an `Authorization` header with the message signature (signed by default with the WEBHOOK_SECRET `mySecret`).

You will have to:
 - implement an application server that will receive the event notifications
 - add a method in your SDK to validate the `Authorization` header is valid
 - handle the event (Printing the body in the console will be enough)

## Submission

All your code has to be pushed to a GitHub repository. When you are done, share it with your recruiter, we will review your submission and discuss about it with you in your next interview. Good luck!
