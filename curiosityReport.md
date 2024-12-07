# **HTTP OPTIONS requests that I saw after importing .HAR file during the Grafana K6 testing**

**Main question, observations, and pre-research predictions:**

When I was importing the .HAR file into Grafana for K6 testing, I saw a number of requests that were not GET, PUSH, DELETE, or PUSH, but instead OPTIONS. It was especially interesting because they made up approximatly 50% of the requests, which seemed like a very significant amount. Also, I never saw or made an OPTIONS endpoint, so my guess is that they are something that supports the actual GET, PUSH, DELETE, PUSH requests. I don't have a guess yet about why they are needed, or what point in the data transfer they are used
