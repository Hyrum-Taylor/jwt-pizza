# **HTTP OPTIONS requests that I saw after importing .HAR file during Grafana K6 testing**

***Main question, observations, and pre-research predictions:***

When I was importing the .HAR file into Grafana for K6 testing, I saw a number of requests that were not GET, PUSH, DELETE, or PUSH, but instead OPTIONs. It was especially interesting because they made up approximatly 50% of the requests, which seemed like a very significant amount. Also, I never saw or made an OPTIONS endpoint while editing the JWT-Pizza-Service code, so my guess is that they are something that supports the actual GET, PUSH, DELETE, PUSH requests. I don't have a guess yet about why they are needed, or what point in the data transfer they are used.
![HTTP Requests Recorded Screenshot](https://github.com/Hyrum-Taylor/jwt-pizza/blob/main/Curiosity%20Report/HTTP%20Requests%20Recorded%20Screenshot.png)

***Answers:***

To answer this, the first thing I did was record loading the JWT-Pizza page on Burp suite, and from there, looking at at the contents of an OPTIONS request. Here is a screenshot of what I saw when the website was preparing to GET the menu when loading the order page:
![Options Contents Screenshot](https://github.com/Hyrum-Taylor/jwt-pizza/blob/main/Curiosity%20Report/Options%20content.png)

From this, it looks like the body says nothing except "GET,HEAD,PUT", which supports my guess about it existing to support the GET request.

Now, I did a google search for OPTIONS, and found the first two sources below. Both sources agree that the pupose of an OPTIONS request is to see what HTTP methods are available for an endpoint. There are a few questions I have at this point:
- What is a HEAD request? The response includes this as a valid request type
  - Why does the reponse not say that OPTIONS is available? Both sources showed OPTIONS as being returned as a valid option, but my request in Burp doesn't show that. Maybe because both sources use HTTP/1.1?
- Why is this neccessary? What happens if this isn't sent?
- What happens if a request is sent to an invalid endpoint?



***Conclusion:***

***Sources:***
- https://http.dev/options
- https://www.youtube.com/watch?v=snZ0qP79VRM
