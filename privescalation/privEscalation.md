# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    The userId is specified in each request to change that user's role. Any userId can be sent
    with this request with no validation.

2. Briefly explain how a malicious attacker can exploit them.
    If a request is sent with userId = 1, the request is executed as admin, allowing privilege
    escalation. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
    Secure.ts uses session cookies to verify that the user executing a request is logged in and their 
    userId is one of an admin before allowing the modification. This prevents privilege escalation
    because only a logged in admin user is allowed, regardless of the submitted userId. 

