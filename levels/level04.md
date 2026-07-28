# Natas Level 4 - What I Learned

In this level, I learned about HTTP request headers and how the `Referer` header works.

I used Burp Suite to intercept the request sent from my browser before it reached the server. By modifying the `Referer` header and forwarding the request, I was able to understand that the server was trusting information sent by the client.

### Key Takeaways

* Burp Suite can intercept traffic between the browser and the server.
* HTTP headers can be modified before the request is sent.
* The `Referer` header tells the server which page the user came from.
* Client-side data should never be fully trusted because users can modify it.
* Many web security challenges involve analyzing and changing requests to see how the server behaves.

### Skills Practiced

* Using Burp Suite's Proxy and Intercept features.
* Inspecting and modifying HTTP requests.
* Understanding the importance of request headers in web applications.
* Thinking like a security tester by asking: "What happens if I change this value?"

