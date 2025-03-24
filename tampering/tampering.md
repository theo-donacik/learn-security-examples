# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    Insecure.ts takes a user's input and redners it, which allows for cross-site
    scripting attacks.

2. Briefly explain how a malicious attacker can exploit them.
    If a malicious user submits script code instead of just a string, it will be executed
    when loaded by the browser, so if viewed by other users, they will load and run the
    malicious script.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
    Secure.ts sanitizes the input, so the HTML script tag submitted is just treated 
    as a string and cannot be executed by the browser. 
