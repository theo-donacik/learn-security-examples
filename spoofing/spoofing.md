# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
    The session token is stored as a cookie which can be read and used by malicious programs to 
    spoof your credentials.

2. Briefly explain different ways in which vulnerability can be exploited.
    The session ID can be used to session hijack by reading the token and sending additional 
    requests as if they were you (mal-steal-cookie.html). It can also be used for CSRF where
    a malicious site can perform actions on the original site by redirecting you because
    it knows you are logged in (mal-csrf.html). 

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
    Secure.ts does not have the same vulnerability because it adds additional tags on the 
    session cookie it stores. It sets 'httpOnly' which means the cookie is not readable by javascript
    which helps fix session hijacking, and 'sameSite' which prevents CSRF so a request to the 
    original site from a malicious site cannot use your cookie. 
