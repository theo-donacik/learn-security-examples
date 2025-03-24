# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
    In message send requests, the user id can be specified in the request so a malicious
    user can send a request with an user id with no way of knowing who actually sent the 
    message. 
    
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
    secure.ts includes robust logging of every POST and GET including the user who sent the message,
    current time, and their IP address, identifying each request to an individual.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
    The secure version uses a middleware in the "chain of responsibility" design pattern
    runs on every GET and POST action to write the logs. The logger is part of the chain so
    before the request is fulfilled, the request is passed through the logging middleware which
    adds the time, request type, endpoint, and IP address to the log file, then passes on to the
    request handler.
