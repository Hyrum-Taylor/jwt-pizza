# **HTTP OPTIONS requests that I saw after importing .HAR file during Grafana K6 testing**

***Main question, observations, and pre-research predictions:***

When I was importing the .HAR file into Grafana for K6 testing, I saw a number of requests that were not GET, PUSH, DELETE, or PUSH, but instead OPTIONs. It was especially interesting because they made up approximatly 50% of the requests, which seemed like a very significant amount. Also, I never saw or made an OPTIONS endpoint while editing the JWT-Pizza-Service code, so my guess is that they are something that supports the actual GET, PUSH, DELETE, PUSH requests. I don't have a guess yet about why they are needed, or what point in the data transfer they are used.
![HTTP Requests Recorded Screenshot](https://github.com/Hyrum-Taylor/jwt-pizza/blob/main/Curiosity%20Report/HTTP%20Requests%20Recorded%20Screenshot.png)

***Answers:***

To answer this, the first thing I did was record loading the JWT-Pizza page on Burp suite, and from there, looking at at the contents of an OPTIONS request. Here is a screenshot of what I saw when the website was preparing to GET the menu when loading the order page:
![Options Contents Screenshot](https://github.com/Hyrum-Taylor/jwt-pizza/blob/main/Curiosity%20Report/Options%20content.png)

From this, it looks like the body says nothing except "GET,HEAD,PUT", which supports my guess about it existing to support the GET request.

Now, I did a google search for OPTIONS, and found the first two sources below. Both sources agree that the pupose of an OPTIONS request is to see what HTTP methods are available for an endpoint. I found a few new questions after this search:

***Questions - Round 2***

- What is a HEAD request? The response includes this as a valid request type
  - Why does the reponse not say that OPTIONS is available? Both sources showed OPTIONS as being returned as a valid option, but my request in Burp doesn't show that.
    - Maybe because both sources use HTTP/1.1, but my code uses HTTP/2?
- Why is this neccessary? What happens if this isn't sent?
- What happens if a request is sent to an invalid endpoint?

***Answers - Round 2***


- **Head Requests**: HEAD requests essentially get only the header of the resource. This is useful for not transfering large amounts of data if it is not neccessary, and for checking to make sure the resource exists (which appears to be the same purpose as the OPTIONS requests).
  - **Lack of OPTIONS**: I couldn't find anything specifically talking about this, but I think it's just that I didn't directly add any OPTIONS options. This is something I could dig into a bit more, but I have a lot more questions and not much time.
    - **HTTP Versions**: I don't think using HTTP/2 instead of HTTP/1.1 is the cause of OPTIONS not being returned in the OPTIONS response: HTTP appears to be just how things are transported, not related to the endpoints on the server
- To answer this, let's just try it out!


***Conclusion:***

***Sources:***
1) https://http.dev/options
2) https://www.youtube.com/watch?v=snZ0qP79VRM
3) https://dev.to/accreditly/http1-vs-http2-vs-http3-2k1c
4) https://stackoverflow.com/questions/29954037/why-is-an-options-request-sent-and-can-i-disable-it
