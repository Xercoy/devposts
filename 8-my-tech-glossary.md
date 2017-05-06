_Last edited on 05/04/2017_

I'm so bad at giving definitions in interviews that it makes me cringe every time I think about it. I can't tell you what an API is on the spot, but I can prove through projects and work experience that I'm proficient in building them. 

It's also a good exercise to place thoughts into words, in my opinion. If you can teach someone something, you know that content well. Thus, I'll try to make this resource good enough to teach from. I'll try...

This post will be used in interviews to answer definitions that I've spent a good chunk of my life learning and defining, time of which will finally do some good and result in less cringeworthy moments. I have never, ever used any resource other than my noggin unless explicitly allowed to, and I think I'll probably ask for permission to use this post during interviews just in case. 

**All definitions are in my own words unless noted.**

---

### <u>Continuous Delivery</u>
**An approach to software development in which changes to a codebase occur in short and reliable increments; the state of the codebase is always production ready.**

###### Benefits
Allowing code to be pushed to production more frequently uncovers bugs that may or not have a large impact on the code. This practice also creates a quicker feedback loop, which is one of the most important influences in code development. One more useful but mostly overlooked reason reveals design/architectural changes that need to be made, further ensuring that the code base is high quality and saving resources. 

Sources:
[Wiki](https://en.wikipedia.org/wiki/Continuous_delivery)

---

### <u>Continuous Deployment</u>
An approach to software development in which every modification to a codebase is deployed to production. It's different from Continuous Delivery in that deploying to production on every incremental change is not necessary for CD. 

---

### <u>Continuous Integration</u>
An approach to software development in which changes to the codebase are frequently tested and merged, ideally automatically.

###### Benefits
Error, risk, and resource minimization.

---

### <u> API (Application Programming Interface) </u>
From Wikipedia (such a good response): 
```
In computer programming, an Application Programming Interface (API) is a set of subroutine definitions, protocols, and tools for building application software. In general terms, it is a set of clearly defined methods of communication between various software components.
```

---

### <u>REST API (REpresentational State Transfer)</u>
A specific protocol of interoperability for communication between web systems; operations of which communication is both stateless and predefined. The operations are based closely on the HTTP verbs GET, POST, PUT, DELETE. 



###### Explanation
Stateless ([source](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm))- each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client.

Stateless ([source](http://searchcloudstorage.techtarget.com/definition/RESTful-API)) - Nothing can be retained by the RESTful service between executions. Because the calls are stateless, REST is useful in cloud applications. Stateless components can be freely redeployed if something fails, and they can scale to accommodate load changes. This is because any request can be directed to any instance of a component; there can be nothing saved that has to be remembered by the next transaction.

---

###### Changelog
05/04/17 - Created document