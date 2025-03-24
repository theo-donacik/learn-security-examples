# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    Insecure.ts reads in the 'username' field from the request and uses that to search the 
    database. 

2. Briefly explain how a malicious attacker can exploit them.
    A malicious user can supply a query in the field instead of a real username, in the above
    example setting the username to "username[$ne]=" which when plugged in to the database search, 
    fetches a full user object including their password from the database.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
    Secure.ts verifies that the input is only a string and not a potential script. That way, any 
    text submitted as 'userinfo?' must be a string and treated as a username and cannot be 
    run on the database.
