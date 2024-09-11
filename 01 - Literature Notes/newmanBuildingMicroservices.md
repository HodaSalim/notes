Title: Building Microservices-Error: `format` can only be applied to dates. Tried for format object
Author: Sam Newman
Zotero Link: [PDF](zotero://select/library/items/NNBMMSLM)

> [!NOTE]- Abstract
> 

%% begin annotations %%


**Imported: 2024-09-03**
# Chapter 1
## "Microservices at a Glance"  [Page29](zotero://open-pdf/library/items/NNBMMSLM?page=3&annotation=FXV8F6AB)



 "Microservices are independently releasable services that are modeled around a business domain. A service encapsulates functionality and makes it accessible to other  services via networks—you construct a more complex system from these building  blocks. One microservice might represent inventory, another order management, and  yet another shipping, but together they might constitute an entire ecommerce system."  [Page29](zotero://open-pdf/library/items/NNBMMSLM?page=3&annotation=JL2PNJEB)



 "They are a type of service-oriented architecture, albeit one that is opinionated about  how service boundaries should be drawn, and one in which independent deployability is key."  [Page29](zotero://open-pdf/library/items/NNBMMSLM?page=3&annotation=84NM8GA9)



 "a single microservice is treated as a black box. It hosts business  functionality on one or more network endpoints"  [Page29](zotero://open-pdf/library/items/NNBMMSLM?page=3&annotation=VUAML9AJ)



 "Consumers, whether they’re other microservices or other sorts of programs, access this  functionality via these networked endpoints."  [Page30](zotero://open-pdf/library/items/NNBMMSLM?page=4&annotation=GH878H7C)



 "This means microservice architectures avoid the use of  shared databases in most circumstances; instead, each microservice encapsulates its  own database where required"  [Page30](zotero://open-pdf/library/items/NNBMMSLM?page=4&annotation=CKR3GFVX)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-30-x68-y236.png]] [Page30](zotero://open-pdf/library/items/NNBMMSLM?page=4&annotation=9NT4W428)



 "Microservices embrace the concept of information hiding.1 Information hiding means  hiding as much information as possible inside a component and exposing as little as  possible via external interfaces"  [Page30](zotero://open-pdf/library/items/NNBMMSLM?page=4&annotation=2R3FKY9X)



 "the Hexagonal Architecture pattern"  [Page31](zotero://open-pdf/library/items/NNBMMSLM?page=5&annotation=TKP6XXLL)



 "This pattern describes the importance of keeping the internal implementation separate from its external interfaces, with the idea that you might want to  interact with the same functionality over different types of interfaces."  [Page31](zotero://open-pdf/library/items/NNBMMSLM?page=5&annotation=GINHLQ9P)



## "Key Concepts of Microservices"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=TG87XGN4)



### "Independent Deployability"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=EZW92RHN)



 "Independent deployability is the idea that we can make a change to a microservice,  deploy it, and release that change to our users, without having to deploy any other  microservices"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=FANKK34C)



 "It’s a discipline you adopt as  your default release approach. This is a simple idea that is nonetheless complex in  execution"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=AERCZUSM)



 "To ensure independent deployability, we need to make sure our microservices are  loosely coupled"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=GGVNJDXI)



 "This means we need explicit, well-defined, and stable contracts between  services. Some implementation choices make this difficult—the sharing of databases,  for example, is especially problematic"  [Page32](zotero://open-pdf/library/items/NNBMMSLM?page=6&annotation=TIPCSZIA)



### "Modeled Around a Business Domain"  [Page33](zotero://open-pdf/library/items/NNBMMSLM?page=7&annotation=SFU3VNMD)



 "Techniques like domain-driven design can allow you to structure your code to better  represent the real-world domain that the software operates in.3 With microservice  architectures, we use this same idea to define our service boundaries"  [Page33](zotero://open-pdf/library/items/NNBMMSLM?page=7&annotation=47WW92UJ)



 "Rolling out a feature that requires changes to more than one microservice is expensive. You need to coordinate the work across each service (and potentially across separate teams) and carefully manage the order in which the new versions of these  services are deployed"  [Page33](zotero://open-pdf/library/items/NNBMMSLM?page=7&annotation=CKPAQTBI)



 "By making our services end-to-end slices of business functionality, we ensure that  our architecture is arranged to make changes to business functionality as efficient as  possible"  [Page33](zotero://open-pdf/library/items/NNBMMSLM?page=7&annotation=5XV43HJZ)



 "with microservices we have made a decision to prioritize high  cohesion of business functionality over high cohesion of technical functionality."  [Page33](zotero://open-pdf/library/items/NNBMMSLM?page=7&annotation=ISTRGLXJ)



### "Owning Their Own State"  [Page34](zotero://open-pdf/library/items/NNBMMSLM?page=8&annotation=6MFDG72M)



 "microservices should avoid the use of shared databases. If a microservice wants to access data  held by another microservice, it should go and ask that second microservice for the  data."  [Page34](zotero://open-pdf/library/items/NNBMMSLM?page=8&annotation=5IS3T5HV)



 "If we want to make independent deployability a reality, we need to ensure that we  limit backward-incompatible changes to our microservices. If we break compatibility  with upstream consumers, we will force them to change as well."  [Page34](zotero://open-pdf/library/items/NNBMMSLM?page=8&annotation=KPI7MJQW)



 "Hiding internal state in a microservice is analogous to the practice of encapsulation  in object-oriented (OO) programming. Encapsulation of data in OO systems is an  example of information hiding in action."  [Page34](zotero://open-pdf/library/items/NNBMMSLM?page=8&annotation=RCAYMUT3)



 "we want to think of our services as end-to-end  slices of business functionality that, where appropriate, encapsulate user interface  (UI), business logic, and data."  [Page35](zotero://open-pdf/library/items/NNBMMSLM?page=9&annotation=PT458L5A)



### "Size"  [Page35](zotero://open-pdf/library/items/NNBMMSLM?page=9&annotation=CBEG5PNS)



 "However, when you get into what makes microservices work as a type of architecture,  the concept of size is actually one of the least interesting aspects"  [Page35](zotero://open-pdf/library/items/NNBMMSLM?page=9&annotation=48MP5HG9)



 "microservice should be kept to the size at which it can be easily understood"  [Page35](zotero://open-pdf/library/items/NNBMMSLM?page=9&annotation=YHNHF7DC)



 "An experienced team may be able to better manage a larger  codebase than another team could. So perhaps it would be better to read James’s  quote here as “a microservice should be as big as your head.”"  [Page35](zotero://open-pdf/library/items/NNBMMSLM?page=9&annotation=BWT9C5TD)



 "When you are first starting out, it’s much more  important that you focus on two key things. First, how many microservices can you  handle? As you have more services, the complexity of your system will increase, and  you’ll need to learn new skills (and perhaps adopt new technology) to cope with this."  [Page36](zotero://open-pdf/library/items/NNBMMSLM?page=10&annotation=5VN8T22E)



 "Second, how do you define microservice  boundaries to get the most out of them, without everything becoming a horribly coupled mess? These topics are much more important to focus on when you start your  journey."  [Page36](zotero://open-pdf/library/items/NNBMMSLM?page=10&annotation=RDDWUYII)



### "Flexibility"  [Page36](zotero://open-pdf/library/items/NNBMMSLM?page=10&annotation=BCTF3DJ7)



 "Another quote from James Lewis is that “microservices buy you options.” Lewis was  being deliberate with his words—they buy you options. They have a cost, and you  must decide whether the cost is worth the options you want to take up."  [Page36](zotero://open-pdf/library/items/NNBMMSLM?page=10&annotation=LU4Z6NBK)



### "Alignment of Architecture and Organization"  [Page36](zotero://open-pdf/library/items/NNBMMSLM?page=10&annotation=LHDUKA5T)



This quote was also mentioned in code complete2 book. Needs more reflecting on as I think this is a general law and not limited to Engineering teams. Back in Digitree I believe the role of account managers was shaped by Waleed's marketing expertise as in other companies that account managers didn't have that much say and authority so in a way the service/product was shaped by the communication structure "The now famous Conway’s law states the following:  Organizations which design systems...are constrained to produce designs which are  copies of the communication structures of these organizations."  [Page37](zotero://open-pdf/library/items/NNBMMSLM?page=11&annotation=6CLCE7VU)



 "Our aspirations around our software have changed. We  now group people in poly-skilled teams to reduce handoffs and silos. We want to ship  software much more quickly than ever before. That is driving us to make different  choices about the way we organize our teams, so that we organize them in terms of  the way we break our systems apart."  [Page38](zotero://open-pdf/library/items/NNBMMSLM?page=12&annotation=D64K2LQN)



 "If we want to make it easier to make changes, instead we  need to change how we group code, choosing cohesion of business functionality  rather than technology. Each service may or may not end up containing a mix of  these three layers, but that is a local service implementation concern."  [Page38](zotero://open-pdf/library/items/NNBMMSLM?page=12&annotation=J6875FHE)



 "A stream-aligned team is a team aligned to a single, valuable stream of work...[T]he  team is empowered to build and deliver customer or user value as quickly, safely, and  independently as possible, without requiring hand-offs to other teams to perform parts  of the work."  [Page40](zotero://open-pdf/library/items/NNBMMSLM?page=14&annotation=KHG5UQRK)



## "The Monolith"  [Page40](zotero://open-pdf/library/items/NNBMMSLM?page=14&annotation=DJDA8LRQ)



### "The Single-Process Monolith"  [Page41](zotero://open-pdf/library/items/NNBMMSLM?page=15&annotation=EYZNGP2G)



 "You may  have multiple instances of this process for robustness or scaling reasons, but fundamentally all the code is packed into a single process. In reality, these single-process  systems can be simple distributed systems in their own right because they nearly  always end up reading data from or storing data into a database, or presenting information to web or mobile applications"  [Page41](zotero://open-pdf/library/items/NNBMMSLM?page=15&annotation=KBIMNBAY)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-41-x68-y270.png]] [Page41](zotero://open-pdf/library/items/NNBMMSLM?page=15&annotation=GYKVUK5F)



### "The Modular Monolith"  [Page42](zotero://open-pdf/library/items/NNBMMSLM?page=16&annotation=CSCBZJX4)



 "As a subset of the single-process monolith, the modular monolith is a variation in  which the single process consists of separate modules. Each module can be worked  on independently, but all still need to be combined together for deployment"  [Page42](zotero://open-pdf/library/items/NNBMMSLM?page=16&annotation=8Q7AVSFH)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-42-x66-y335.png]] [Page42](zotero://open-pdf/library/items/NNBMMSLM?page=16&annotation=9H49P49A)



https://www.youtube.com/watch?v=ISYKx8sa53g "If the  module boundaries are well defined, it can allow for a high degree of parallel work,  while avoiding the challenges of the more distributed microservice architecture by  having a much simpler deployment topology. Shopify is a great example of an  organization that has used this technique as an alternative to microservice decomposition, and it seems to work really well for that company"  [Page42](zotero://open-pdf/library/items/NNBMMSLM?page=16&annotation=MQSF3JJX)



 "One of the challenges of a modular monolith is that the database tends to lack the  decomposition we find in the code level, leading to significant challenges if you want  to pull apart the monolith in the future."  [Page42](zotero://open-pdf/library/items/NNBMMSLM?page=16&annotation=INDQBJV2)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-43-x66-y450.png]] [Page43](zotero://open-pdf/library/items/NNBMMSLM?page=17&annotation=F828IAD7)



### "The Distributed Monolith"  [Page43](zotero://open-pdf/library/items/NNBMMSLM?page=17&annotation=CUXGEQN8)



SOA = Service-oriented architecture "A distributed monolith is a system that consists of multiple services, but for whatever  reason, the entire system must be deployed together. A distributed monolith might  well meet the definition of an SOA, but all too often, it fails to deliver on the promises  of SOA"  [Page43](zotero://open-pdf/library/items/NNBMMSLM?page=17&annotation=MPU93QTN)



 "Distributed monoliths typically emerge in an environment in which not enough  focus was placed on concepts like information hiding and cohesion of business  functionality. Instead, highly coupled architectures cause changes to ripple across  service boundaries, and seemingly innocent changes that appear to be local in scope  break other parts of the system."  [Page43](zotero://open-pdf/library/items/NNBMMSLM?page=17&annotation=6PHYV2TK)



### "Monoliths and Delivery Contention"  [Page43](zotero://open-pdf/library/items/NNBMMSLM?page=17&annotation=IMGVMHH4)



 "Having a monolith doesn’t mean you will definitely face the challenges of delivery  contention any more than having a microservice architecture means that you won’t  ever face the problem. But a microservice architecture does give you more concrete  boundaries around which ownership lines can be drawn in a system, giving you  much more flexibility when it comes to reducing this problem."  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=EXBIFRQM)



## "Advantages of Monoliths"  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=4SHAX4CD)

 "Their much simpler deployment topology can avoid many of the  pitfalls associated with distributed systems. This can result in much simpler developer workflows, and monitoring, troubleshooting, and activities like end-to-end testing can be greatly simplified as well."  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=FCNXRHRR)



 "Monoliths can also simplify code reuse within the monolith itself. If we want to reuse  code within a distributed system, we need to decide whether we want to copy code,  break out libraries, or push the shared functionality into a service."  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=DEK5FBLM)



Which aligns with Ahmed Farghal's first video in his distributed systems series "I’ve met multiple people for whom the term  monolith is synonymous with legacy. This is a problem. A monolithic architecture is a  choice, and a valid one at that. I’d go further and say that in my opinion it is the sensible default choice as an architectural style. In other words, I am looking for a reason  to be convinced to use microservices, rather than looking for a reason not to use  them"  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=KEC3BK7Z)



## "Enabling Technology"  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=D79CYW8U)



 "I don’t think you need to adopt lots of new technology when  you first start using microservices."  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=2PK4TBWH)



 "Instead, as you ramp up your microservice architecture, you should constantly be looking for issues caused by your increasingly distributed system, and then for technology that  might help."  [Page44](zotero://open-pdf/library/items/NNBMMSLM?page=18&annotation=3CDVXMDB)



 "That said, technology has played a large part in the adoption of microservices as a  concept. Understanding the tools that are available to help you get the most out of  this architecture is going to be a key part of making any implementation of microservices a success."  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=NQMTHLFN)



 "I would go as far to say that microservices require an understanding of the supporting technology to such a degree that previous distinctions  between logical and physical architecture can be problematic—if you are involved in  helping shape a microservice architecture, you’ll need a breadth of understanding of  these two worlds."  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=QJ39CW7U)



### "Log Aggregation and Distributed Tracing"  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=ISG6JJVC)



 "I strongly advocate the implementation  of a log aggregation system as a prerequisite for adopting a microservice architecture."  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=ANWS5T7B)



 "These systems allow you to collect and aggregate logs from across all your services,  providing you a central place from which logs can be analyzed, and even made part of  an active alerting mechanism."  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=82LITQNR)



 "You can make these log aggregation tools even more useful by implementing correlation IDs, in which a single ID is used for a related set of service calls—for example,  the chain of calls that might be triggered due to user interaction. By logging this ID as  part of each log entry, isolating the logs associated with a given flow of calls becomes  much easier, which in turn makes troubleshooting much easier."  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=63R6ATSS)



 "As your system grows in complexity, it becomes essential to consider tools that allow  you to better explore what your system is doing, providing the ability to analyze  traces across multiple services, detect bottlenecks, and ask questions of your system"  [Page45](zotero://open-pdf/library/items/NNBMMSLM?page=19&annotation=62Q4K5ZT)



 "products like Lightstep and Honeycomb (shown in Figure 1-9) take these ideas  further. They represent a new generation of tools that move beyond traditional monitoring approaches, making it much easier to explore the state of your running system."  [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=EABCDTNT)



 "They’ve been built from the ground up to  solve the sorts of problems that operators of microservice architectures have to deal  with."  [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=3TSIETBL)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-46-x70-y219.png]] [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=SWGZUEBY)



### "Containers and Kubernetes"  [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=FIWL9HMF)



 "Ideally, you want to run each microservice instance in isolation. This ensures that  issues in one microservice can’t affect another microservice"  [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=KEVUKZBY)



 "Virtualization is one way to create isolated execution environments on existing hardware, but normal virtualization techniques can be quite heavy  when we consider the size of our microservices. Containers, on the other hand, provide a much more lightweight way to provision isolated execution for service instances, resulting in faster spin-up times for new container instances, along with being  much more cost effective for many architectures"  [Page46](zotero://open-pdf/library/items/NNBMMSLM?page=20&annotation=NZAGJ3UB)



 "After you begin playing around with containers, you’ll also realize that you need  something to allow you to manage these containers across lots of underlying  machines. Container orchestration platforms like Kubernetes do exactly that"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=I4U4NAFU)



 "Don’t feel the need to rush to adopt Kubernetes, or even containers for that matter.  They absolutely offer significant advantages over more traditional deployment techniques, but their adoption is difficult to justify if you have only a few microservices.  After the overhead of managing deployment begins to become a significant headache,  start considering containerization of your service and the use of Kubernetes"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=PAKJEXUT)



 "Running your own Kubernetes cluster can be a significant amount of  work!"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=642QCVDK)



### "Streaming"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=RZYZW69J)



 "Although with microservices we are moving away from monolithic databases, we still  need to find ways to share data between microservices"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=JELTMZ7B)



 "Products  that allow for the easy streaming and processing of what can often be large volumes  of data have therefore become popular with people using microservice architectures.  For many people, Apache Kafka has become the de facto choice for streaming data in  a microservice environment"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=J6VU3S8T)



### "Public Cloud and Serverless"  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=9DSDD28H)



 "As your microservice architecture grows, more and more work will be pushed into the operational  space."  [Page47](zotero://open-pdf/library/items/NNBMMSLM?page=21&annotation=6V8AA93R)



 "By making use of these managed services, you are offloading a large amount of  this work to a third party that is arguably better able to deal with these tasks"  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=FZEFKKX7)



 "Of particular interest among the public cloud offerings are the products that sit under  the banner of serverless. These products hide the underlying machines, allowing you  to work at a higher level of abstraction"  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=4MQUQMB6)



 "Rather than worrying about how many servers you need to run your service,  you just deploy your code and let the underlying platform handle spinning up instances of your code on demand."  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=7ILC9JN9)



## "Advantages of Microservices"  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=CXXV7VKR)



### "Technology Heterogeneity"  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=WK9EH7QY)



 "With a system composed of multiple, collaborating microservices, we can decide to  use different technologies inside each one. This allows us to pick the right tool for  each job rather than having to select a more standardized, one-size-fits-all approach  that often ends up being the lowest common denominator."  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=CWKQU2WC)



 "For example, for a social network, we might store our users’  interactions in a graph-oriented database to reflect the highly interconnected nature  of a social graph, but perhaps the posts the users make could be stored in a  document-oriented data store"  [Page48](zotero://open-pdf/library/items/NNBMMSLM?page=22&annotation=4X9F3679)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-49-x66-y437.png]] [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=K5QBYYST)



 "With a monolithic application, if I want to try a new programming language, database, or  framework, any change will affect much of my system. With a system consisting of  multiple services, I have multiple new places to try out a new piece of technology. I  can pick a microservice with perhaps the lowest risk and use the technology there,  knowing that I can limit any potential negative impact"  [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=VWUJF4JY)



 "Embracing multiple technologies doesn’t come without overhead, of course. Some  organizations choose to place some constraints on language choices. Netflix and  Twitter, for example, mostly use the Java Virtual Machine (JVM) as a platform  because those companies have a very good understanding of the reliability and performance of that system"  [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=D34EILS2)



 "The fact that internal technology implementation is hidden from consumers can also  make upgrading technologies easier. Your entire microservice architecture might be  based on Spring Boot, for example, but you could change JVM version or framework  versions for just one microservice, making it easier to manage the risk of upgrades."  [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=KZJH7PIH)



### "Robustness"  [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=VD4X2MJC)



 "A  component of a system may fail, but as long as that failure doesn’t cascade, you  can isolate the problem, and the rest of the system can carry on working."  [Page49](zotero://open-pdf/library/items/NNBMMSLM?page=23&annotation=8ZSV8UWV)



 "In a monolithic service, if the service  fails, everything stops working. With a monolithic system, we can run on multiple  machines to reduce our chance of failure, but with microservices, we can build systems that handle the total failure of some of the constituent services and degrade  functionality accordingly."  [Page50](zotero://open-pdf/library/items/NNBMMSLM?page=24&annotation=MKVH7MLK)



 "To ensure that our microservice systems can  properly embrace this improved robustness, we need to understand the new sources  of failure that distributed systems have to deal with. Networks can and will fail, as will  machines. We need to know how to handle such failures and the impact (if any)  those failures will have on the end users of our software. I have certainly worked with  teams who have ended up with a less robust system after their migration to microservices due to their not taking these concerns seriously enough."  [Page50](zotero://open-pdf/library/items/NNBMMSLM?page=24&annotation=L4X3VU8G)



### "Scaling"  [Page50](zotero://open-pdf/library/items/NNBMMSLM?page=24&annotation=7TGFBSCQ)



 "With a large, monolithic service, we need to scale everything together. Perhaps one  small part of our overall system is constrained in performance, but if that behavior is  locked up in a giant monolithic application, we need to handle scaling everything as a  piece"  [Page50](zotero://open-pdf/library/items/NNBMMSLM?page=24&annotation=TXEMHHIF)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-50-x70-y76.png]] [Page50](zotero://open-pdf/library/items/NNBMMSLM?page=24&annotation=698P7DDH)



 "When embracing on-demand provisioning systems like those provided by AWS, we  can even apply this scaling on demand for those pieces that need it. This allows us to  control our costs more effectively. It’s not often that an architectural approach can be  so closely correlated to an almost immediate cost savings."  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=F25SGDQR)



### "Ease of Deployment"  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=3YZFMCL4)



 "A one-line change to a million-line monolithic application requires the entire application to be deployed in order to release the change."  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=QYWKMS6T)



 "In practice, deployments such as these end up happening  infrequently because of understandable fear. Unfortunately, this means that our  changes continue to build up between releases, until the new version of our application entering production has masses of changes."  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=G8Y8DURK)



 "With microservices, we can make a change to a single service and deploy it independently of the rest of the system. This allows us to get our code deployed more quickly.  If a problem does occur, it can be quickly isolated to an individual service, making  fast rollback easy to achieve"  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=RVUX2TJF)



 "This is one of the main reasons organizations like Amazon and Netflix use these architectures—to ensure that they remove as many impediments as possible to getting software out the door."  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=C8TY7L7D)



### "Organizational Alignment"  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=35XMEV2H)



I think the rise of microservices align with the agile work management methodology "Microservices allow us to better align our architecture to our organization, helping us  minimize the number of people working on any one codebase to hit the sweet spot of  team size and productivity. Microservices also allow us to change ownership of services as the organization changes—enabling us to maintain the alignment between  architecture and organization in the future."  [Page51](zotero://open-pdf/library/items/NNBMMSLM?page=25&annotation=YJZZTQ8B)



### "Composability"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=8BQHKR8P)



 "One of the key promises of distributed systems and service-oriented architectures is  that we open up opportunities for reuse of functionality. With microservices, we  allow for our functionality to be consumed in different ways for different purposes."  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=HCT25XAX)



 "Now we need to think of the myriad ways that we might want  to weave together capabilities for the web, native application, mobile web, tablet app,  or wearable device"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=9ZAVUG23)



## "Microservice Pain Points"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=X87ZX6E3)



 "In reality,  most microservice points can be laid at the door of distributed systems and  thus would just as likely be evident in a distributed monolith as in a microservice  architecture"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=QMDMH4KT)



 "I’d argue that the bulk of this book is about dealing with the pain, suffering, and  horror of owning a microservice architecture."  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=WU2ZCL56)



### "Developer Experience"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=BNRV6WGP)



 "As you have more and more services, the developer experience can begin to suffer.  More resource-intensive runtimes like the JVM can limit the number of microservices that can be run on a single developer machine"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=NB5LM5S3)



 "Even with less taxing runtimes, there is a limit to the number of  things you can run locally, which inevitably will start conversations about what to do  when you can’t run the entire system on one machine"  [Page52](zotero://open-pdf/library/items/NNBMMSLM?page=26&annotation=EEBL23IR)



 "Extreme solutions can involve “developing in the cloud,” where developers move  away from being able to develop locally anymore. I’m not a fan of this, because feedback cycles can suffer greatly. Instead, I think limiting the scope of which parts of a  system a developer needs to work on is likely to be a much more straightforward  approach"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=6EPEJ5NA)



### "Technology Overload"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=MT9JXWWI)



 "The sheer weight of new technology that has sprung up to enable the adoption of  microservice architectures can be overwhelming."  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=9YTQM3KJ)



 "There is a danger, though, that this wealth of new toys can lead to a form of  technology fetishism. I’ve seen so many companies adopting microservice architecture who decided that it was also the best time to introduce vast arrays of new and  often alien technology"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=5UYI93QN)



 "these are options, not requirements. You have to carefully balance the  breadth and complexity of the technology you use against the costs that a diverse  array of technology can bring"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=YZ65TD86)



 "When you start adopting microservices, some fundamental challenges are inescapable: you’ll need to spend a lot of time understanding issues around data consistency,  latency, service modeling, and the like. If you’re trying to understand how these ideas  change the way you think about software development at the same time that you’re  embracing a huge amount of new technology, you’ll have a hard time of it"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=JSMC832T)



 "As you (gradually) increase the complexity of your microservice architecture, look to  introduce new technology as you need it."  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=UP3QK85U)



 "this gradual increase has the added benefit of allowing  you to gain new and better ways of doing things that will no doubt emerge over time"  [Page53](zotero://open-pdf/library/items/NNBMMSLM?page=27&annotation=75KGCFI3)



### "Cost"  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=K37VE3TT)



 "It’s highly likely that in the short term at least you’ll see an increase in costs from a  number of factors."  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=VJJSSMKM)



 "Firstly, you’ll likely need to run more things—more processes,  more computers, more network, more storage, and more supporting software"  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=JGG4WBL9)



 "Secondly, any change you introduce into a team or an organization will slow you  down in the short term"  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=NICI96I8)



 "In my experience, microservices are a poor choice for an organization primarily concerned with reducing costs, as a cost-cutting mentality—where IT is seen as a cost  center rather than a profit center—will constantly be a drag on getting the most out  of this architecture"  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=FFF7KHBU)



 "microservices can help you make more  money if you can use these architectures to reach more customers or develop more  functionality in parallel."  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=GRMZW599)



 "So are microservices a way to drive more profits? Perhaps.  Are microservices a way to reduce costs? Not so much."  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=5ZXMYH2B)



### "Reporting"  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=LJSHSYT3)



 "With a monolithic system, you typically have a monolithic database. This means that  stakeholders who want to analyze all the data together, often involving large join  operations across data, have a ready-made schema against which to run their reports."  [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=3497T697)



 ![[99 - Meta/Attachements/newmanBuildingMicroservices/image-54-x69-y73.png]] [Page54](zotero://open-pdf/library/items/NNBMMSLM?page=28&annotation=RQMAMFRN)



 "With a microservice architecture, we have broken up this monolithic schema. That  doesn’t mean that the need for reporting across all our data has gone away; we’ve just  made it much more difficult, because now our data is scattered across multiple logically isolated schemas"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=V5LCNPTZ)



 "More modern approaches to reporting, such as using streaming to allow for real-time  reporting on large volumes of data, can work well with a microservice architecture  but typically require the adoption of new ideas and associated technology"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=QKY967V7)



 "you might simply need to publish data from your microservices into central  reporting databases (or perhaps less structured data lakes) to allow for reporting use  cases."  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=N6DJSKVV)



### "Monitoring and Troubleshooting"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=MX35QSJG)



 "With a standard monolithic application, we can have a fairly simplistic approach to  monitoring."  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=F5ADKMEU)



 "the application is often either all up or  all down"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=4PA8EM8D)



 "With a microservice architecture, do we understand the impact if just a single instance of a service goes down"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=5HTBRTUQ)



 "With a monolithic system, if our CPU is stuck at 100% for a long time, we know it’s a  big problem. With a microservice architecture with tens or hundreds of processes,  can we say the same thing? Do we need to wake someone up at 3 a.m. when just one  process is stuck at 100% CPU?"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=XUMEJYJI)



### "Security"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=2V3T8YFM)



 "With a single-process monolithic system, much of our information flowed within  that process. Now, more information flows over networks between our services. This  can make our data more vulnerable to being observed in transit and also to potentially being manipulated as part of man-in-the-middle attacks"  [Page55](zotero://open-pdf/library/items/NNBMMSLM?page=29&annotation=2CF3RX2Q)



### "Testing"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=NJDKZ75L)



 "With any type of automated functional test, you have a delicate balancing act. The  more functionality a test executes—i.e., the broader the scope of the test—the more  confidence you have in your application. On the other hand, the larger the scope of  the test, the harder it is to set up test data and supporting fixtures, the longer the test  can take to run, and the harder it can be to work out what is broken when it fails."  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=I3K7CCBY)



 "End-to-end tests for any type of system are at the extreme end of the scale in terms of  the functionality they cover, and we are used to them being more problematic to  write and maintain than smaller-scoped unit tests. Often this is worth it, though,  because we want the confidence that comes from having an end-to-end test use our  systems in the same way a user might"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=BIX5EXIW)



 "But with a microservice architecture, the scope of our end-to-end tests becomes very  large. We would now need to run tests across multiple processes, all of which need to  be deployed and appropriately configured for the test scenarios"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=EBSZSC5A)



 "These forces mean that as your microservice architecture grows, you will get a diminishing return on investment when it comes to end-to-end testing."  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=EXU4FKSS)



 "This will drive you toward new forms of testing, such as contract-driven testing  or testing in production, as well as the exploration of progressive delivery techniques  such as parallel runs or canary releases"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=ARBRTTPA)



### "Latency"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=FAITNG7I)



 "With a microservice architecture, processing that might previously have been done  locally on one processor can now end up being split across multiple separate microservices. Information that previously flowed within only a single process now needs  to be serialized, transmitted, and deserialized over networks that you might be exercising more than ever before. All of this can result in worsening latency of your  system"  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=SYP3LNZD)



 "it can be difficult to measure the exact impact on latency of operations at  the design or coding phase, this is another reason it’s important to undertake any  microservice migration in an incremental fashion."  [Page56](zotero://open-pdf/library/items/NNBMMSLM?page=30&annotation=MFNYNP59)



 "Sometimes making an operation slower is perfectly  acceptable, as long as it is still fast enough"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=ELVLNFKL)



### "Data Consistency"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=6YCUWH5U)



 "Shifting from a monolithic system, in which data is stored and managed in a single  database, to a much more distributed system, in which multiple processes manage  state in different databases, causes potential challenges with respect to consistency of  data."  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=9M7AWHXN)



 "The use of distributed transactions in most cases proves to be  highly problematic in coordinating state changes."  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=BVHZQ9BI)



 "Instead, you might need to start using concepts like sagas (something I’ll detail at  length in Chapter 6) and eventual consistency to manage and reason about state in  your system."  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=IBBL7H3V)



 "this is another good reason to be cautious in how quickly  you decompose your application. Adopting an incremental approach to decomposition, so that you are able to assess the impact of changes to your architecture in production, is really important"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=LCWNECNA)



## "Should I Use Microservices?"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=V7J54YYP)



 "Despite the drive in some quarters to make microservice architectures the default  approach for software, I feel that because of the numerous challenges I’ve outlined,  adopting them still requires careful thought."  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=U226J8X6)



 "They are an architectural  approach, not the architectural approach. Your own context should play a huge part  in your decision whether to go down that path"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=Z9GTCSGK)



### "Whom They Might Not Work For"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=Q39747BU)



 "Given the importance of defining stable service boundaries, I feel that microservice  architectures are often a bad choice for brand-new products or startups. In either  case, the domain that you are working with is typically undergoing significant change  as you iterate on the fundamentals of what you are trying to build"  [Page57](zotero://open-pdf/library/items/NNBMMSLM?page=31&annotation=6U4CKEXN)



 "I do see a temptation for startups to go microservice first, the reasoning being, “If  we’re really successful, we’ll need to scale!” The problem is that you don’t necessarily  know if anyone is even going to want to use your new product."  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=QD97AF8S)



 "Uber initially focused on limos, and Flickr spun out of attempts to create a multiplayer online game. The process of finding product market fit means that  you might end up with a very different product at the end than the one you thought  you’d build when you started."  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=DKPATJK4)



 "Startups also typically have fewer people available to build the system, which creates  more challenges with respect to microservices."  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=HUV5IL94)



 "The smaller  the team, the more pronounced this cost will be."  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=AFQ63ZXK)



 "For a small team, a microservice architecture can be  difficult to justify because there is work required just to handle the deployment and  management of the microservices themselves."  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=QGZC2CXQ)



 "It’s much easier to  move to microservices later, after you understand where the constraints are in your  architecture and what your pain points are—then you can focus your energy on using  microservices in the most sensible places"  [Page58](zotero://open-pdf/library/items/NNBMMSLM?page=32&annotation=JD9P78QI)



### "Where They Work Well"  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=MTL569NP)



 "In my experience, probably the single biggest reason that organizations adopt microservices is to allow for more developers to work on the same system without getting  in each other’s way"  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=Z795KEXB)



 "A five-person startup is likely to find a microservice architecture a drag. A  hundred-person scale-up that is growing rapidly is likely to find that its growth is  much easier to accommodate with a microservice architecture properly aligned  around its product development efforts."  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=FJLNCGIM)



 "The technology-agnostic nature of microservices ensures that you can get the most  out of cloud platforms. Public cloud vendors provide a wide array of services and  deployment mechanisms for your code."  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=TB5MQU7T)



 "Although it’s worth noting that adopting a wide range of technology can often be a  problem, being able to try out new technology easily is a good way to rapidly identify  new approaches that might yield benefits"  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=NBR5JZ9Y)



 "For the appropriate workloads, an FaaS platform can drastically  reduce the amount of operational overhead, but at present, it’s not a deployment  mechanism that would be suitable in all cases"  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=CG5AYF8N)



 "Above all, a microservice architecture is one that can give you a lot of flexibility as  you continue to evolve your system. That flexibility has a cost, of course, but if you  want to keep your options open regarding changes you might want to make in the  future, it could be a price worth paying."  [Page59](zotero://open-pdf/library/items/NNBMMSLM?page=33&annotation=KHNIIICC)




%% end annotations %%

%% Import Date: 2024-09-03T17:00:41.529+03:00 %%
