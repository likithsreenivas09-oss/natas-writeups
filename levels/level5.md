# Natas Level 5 - What I Learned

In this level, I learned that the website stored the user's login state inside a cookie named `loggedin`.

The cookie had the value:

loggedin=0

which indicated that the user was not logged in. Since cookies are stored on the client side, I was able to modify the value to:

loggedin=1


After changing the cookie and refreshing the page, the server treated me as a logged-in user.

## Key Takeaways

* Cookies are stored in the user's browser and can be modified.
* Applications should not blindly trust client-side data such as cookies.
* Authentication and authorization decisions should be properly validated on the server side.
* Storing sensitive information or security decisions only in client-side cookies can lead to unauthorized access.

## Skills Practiced

* Inspecting browser cookies using Developer Tools.
* Understanding how cookies are used to maintain login state.
* Identifying insecure trust in client-side data.
* Thinking like a security tester by asking: "What happens if I modify this value?"

