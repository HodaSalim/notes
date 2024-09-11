Title: Designing Data-Intensive Applications-Error: `format` can only be applied to dates. Tried for format object
Author: Martin Kleppmann
Zotero Link: [PDF](zotero://select/library/items/74Y7IY96)

> [!NOTE]- Abstract
> Data is at the center of many challenges in system design today. Difficult issues need to be figured out, such as scalability, consistency, reliability, efficiency, and maintainability. In addition, we have an overwhelming variety of tools, including relational databases, NoSQL datastores, stream or batch processors, and message brokers. What are the right choices for your application? How do you make sense of all these buzzwords?

In this practical and comprehensive guide, author Martin Kleppmann helps you navigate this diverse landscape by examining the pros and cons of various technologies for processing and storing data. Software keeps changing, but the fundamental principles remain the same. With this book, software engineers and architects will learn how to apply those ideas in practice, and how to make full use of data in modern applications.

%% begin annotations %%


**Imported: 2024-09-08**
# Chapter 1

 "Many applications today are data-intensive, as opposed to compute-intensive. Raw  CPU power is rarely a limiting factor for these applications—bigger problems are  usually the amount of data, the complexity of data, and the speed at which it is  changing"  [Page25](zotero://open-pdf/library/items/74Y7IY96?page=3&annotation=GP8QXEZE)



 "A data-intensive application is typically built from standard building blocks that provide commonly needed functionality. For example, many applications need to: 
• Store data so that they, or another application, can find it again later (databases) 
• Remember the result of an expensive operation, to speed up reads (caches) 
• Allow users to search data by keyword or filter it in various ways (search indexes) 
• Send a message to another process, to be handled asynchronously (stream processing) 
• Periodically crunch a large amount of accumulated data (batch processing)"  [Page25](zotero://open-pdf/library/items/74Y7IY96?page=3&annotation=YP9QS6Q3)



## "Thinking About Data Systems"  [Page26](zotero://open-pdf/library/items/74Y7IY96?page=4&annotation=L55PY5TF)



 "a database and a message queue have some superficial similarityboth store data for some time—they have very different access patterns, which means  different performance characteristics, and thus very different implementations. So why should we lump them all together under an umbrella term like data systems?"  [Page26](zotero://open-pdf/library/items/74Y7IY96?page=4&annotation=B6PVZNPI)



 "They are optimized for a variety of different use cases, and they no longer neatly fit into traditional categories as argued in [[stonebrakerOneSizeFits2005]]. For example, there are datastores that are also used as message queues (Redis), and there are message queues with database-like durability guarantees (Apache Kafka). The boundaries between the categories are becoming blurred."  [Page26](zotero://open-pdf/library/items/74Y7IY96?page=4&annotation=Y2TZ4YP6)



 "Secondly, increasingly many applications now have such demanding or wide-ranging  requirements that a single tool can no longer meet all of its data processing and storage needs"  [Page26](zotero://open-pdf/library/items/74Y7IY96?page=4&annotation=73WP3SWH)



 "you have an application-managed caching layer (using Memcached  or similar), or a full-text search server (such as Elasticsearch or Solr) separate from  your main database, it is normally the application code’s responsibility to keep those  caches and indexes in sync with the main database."  [Page26](zotero://open-pdf/library/items/74Y7IY96?page=4&annotation=W2UVF5NF)



 ![[99 - Meta/Attachements/kleppmannDesigningDataIntensiveApplications/image-27-x66-y320.png]] [Page27](zotero://open-pdf/library/items/74Y7IY96?page=5&annotation=HKBBQ6Z3)



 "Reliability  The system should continue to work correctly (performing the correct function at  the desired level of performance) even in the face of adversity (hardware or software faults, and even human error)"  [Page28](zotero://open-pdf/library/items/74Y7IY96?page=6&annotation=WVD57SV5)



 "Scalability  As the system grows (in data volume, traffic volume, or complexity), there should  be reasonable ways of dealing with that growth."  [Page28](zotero://open-pdf/library/items/74Y7IY96?page=6&annotation=CTHBZMD3)



 "Maintainability  Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use  cases), and they should all be able to work on it productively."  [Page28](zotero://open-pdf/library/items/74Y7IY96?page=6&annotation=CQNEIJ3Q)



## "Reliability"  [Page28](zotero://open-pdf/library/items/74Y7IY96?page=6&annotation=ZNBNZIJG)



 "For software, typical expectations include:  • The application performs the function that the user expected.  • It can tolerate the user making mistakes or using the software in unexpected  ways.  • Its performance is good enough for the required use case, under the expected  load and data volume. • The system prevents any unauthorized access and abuse.  If all those things together mean “working correctly,” then we can understand reliability as meaning, roughly, “continuing to work correctly, even when things go  wrong.”"  [Page28](zotero://open-pdf/library/items/74Y7IY96?page=6&annotation=8V7BWRFN)



 "Note that a fault is not the same as a failure [2]. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a  whole stops providing the required service to the user."  [Page29](zotero://open-pdf/library/items/74Y7IY96?page=7&annotation=YM7EEF86)



discussed in [[yuanSimpleTestingCan2014]] "Counterintuitively, in such fault-tolerant systems, it can make sense to increase the  rate of faults by triggering them deliberately—for example, by randomly killing individual processes without warning. Many critical bugs are actually due to poor error  handling"  [Page29](zotero://open-pdf/library/items/74Y7IY96?page=7&annotation=64C5CUCQ)



 "The Netflix Chaos  Monkey [4] is an example of this approach."  [Page29](zotero://open-pdf/library/items/74Y7IY96?page=7&annotation=ZFR6KJ5R)



### "Hardware Faults"  [Page29](zotero://open-pdf/library/items/74Y7IY96?page=7&annotation=7H4V3MW4)



 "Disks may be set up in a RAID  configuration, servers may have dual power supplies and hot-swappable CPUs, and  datacenters may have batteries and diesel generators for backup power. When one  component dies, the redundant component can take its place while the broken component is replaced. This approach cannot completely prevent hardware problems  from causing failures, but it is well understood and can often keep a machine running  uninterrupted for years"  [Page29](zotero://open-pdf/library/items/74Y7IY96?page=7&annotation=G52BBH3S)



 "as data volumes and applications’ computing demands have increased,  more applications have begun using larger numbers of machines, which proportionally increases the rate of hardware faults. Moreover, in some cloud platforms such as  Amazon Web Services (AWS) it is fairly common for virtual machine instances to  become unavailable without warning [7], as the platforms are designed to prioritize  flexibility and elasticityi over single-machine reliability.  Hence there is a move toward systems that can tolerate the loss of entire machines, by  using software fault-tolerance techniques in preference or in addition to hardware  redundancy."  [Page30](zotero://open-pdf/library/items/74Y7IY96?page=8&annotation=3TSDK73K)



 "a single-server system  requires planned downtime if you need to reboot the machine (to apply operating  system security patches, for example), whereas a system that can tolerate machine  failure can be patched one node at a time, without downtime of the entire system"  [Page30](zotero://open-pdf/library/items/74Y7IY96?page=8&annotation=RRB8EISK)



### "Software Errors"  [Page30](zotero://open-pdf/library/items/74Y7IY96?page=8&annotation=RFX26HIC)



 "Another class of fault is a systematic error within the system [8]. Such faults are  harder to anticipate, and because they are correlated across nodes, they tend to cause  many more system failures than uncorrelated hardware faults [5]. Examples include:  • A software bug that causes every instance of an application server to crash when  given a particular bad input. For example, consider the leap second on June 30,  2012, that caused many applications to hang simultaneously due to a bug in the  Linux kernel [9].  • A runaway process that uses up some shared resource—CPU time, memory, disk  space, or network bandwidth."  [Page30](zotero://open-pdf/library/items/74Y7IY96?page=8&annotation=MKI9HECM)



 "• A service that the system depends on that slows down, becomes unresponsive, or  starts returning corrupted responses.  • Cascading failures, where a small fault in one component triggers a fault in  another component, which in turn triggers further faults [10]."  [Page31](zotero://open-pdf/library/items/74Y7IY96?page=9&annotation=YTRGZUGN)



 "In those circumstances, it  is revealed that the software is making some kind of assumption about its environment—and while that assumption is usually true, it eventually stops being true for  some reason [11]."  [Page31](zotero://open-pdf/library/items/74Y7IY96?page=9&annotation=V8AFRF5V)



### "Human Errors"  [Page31](zotero://open-pdf/library/items/74Y7IY96?page=9&annotation=ISHGRJD9)



 "Even when they have the best intentions, humans are  known to be unreliable. For example, one study of large internet services found that  configuration errors by operators were the leading cause of outages, whereas hardware faults (servers or network) played a role in only 10–25% of outages"  [Page31](zotero://open-pdf/library/items/74Y7IY96?page=9&annotation=RCX7WBFR)



 "How do we make our systems reliable, in spite of unreliable humans? The best systems combine several approaches:  • Design systems in a way that minimizes opportunities for error. For example,  well-designed abstractions, APIs, and admin interfaces make it easy to do “the  right thing” and discourage “the wrong thing.” However, if the interfaces are too  restrictive people will work around them, negating their benefit, so this is a tricky  balance to get right.  • Decouple the places where people make the most mistakes from the places where  they can cause failures. In particular, provide fully featured non-production  sandbox environments where people can explore and experiment safely, using  real data, without affecting real users.  • Test thoroughly at all levels, from unit tests to whole-system integration tests and  manual tests [3]. Automated testing is widely used, well understood, and especially valuable for covering corner cases that rarely arise in normal operation."  [Page31](zotero://open-pdf/library/items/74Y7IY96?page=9&annotation=ID2YHYBV)



 "• Allow quick and easy recovery from human errors, to minimize the impact in the  case of a failure. For example, make it fast to roll back configuration changes, roll  out new code gradually (so that any unexpected bugs affect only a small subset of  users), and provide tools to recompute data (in case it turns out that the old computation was incorrect).  • Set up detailed and clear monitoring, such as performance metrics and error  rates. In other engineering disciplines this is referred to as telemetry. (Once a  rocket has left the ground, telemetry is essential for tracking what is happening,  and for understanding failures [14].) Monitoring can show us early warning signals and allow us to check whether any assumptions or constraints are being violated. When a problem occurs, metrics can be invaluable in diagnosing the issue.  • Implement good management practices and training—a complex and important  aspect, and beyond the scope of this book."  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=4KM6TSVH)



### "How Important Is Reliability?"  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=YUSYTF6L)



 "Reliability is not just for nuclear power stations and air traffic control softwaremore mundane applications are also expected to work reliably. Bugs in business  applications cause lost productivity (and legal risks if figures are reported incorrectly), and outages of ecommerce sites can have huge costs in terms of lost revenue  and damage to reputation."  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=MY6DIX2L)



 "There are situations in which we may choose to sacrifice reliability in order to reduce  development cost (e.g., when developing a prototype product for an unproven market) or operational cost (e.g., for a service with a very narrow profit margin)—but we  should be very conscious of when we are cutting corners."  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=IFPF5CC2)



## "Scalability"  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=NZ3FX5TH)



 "Scalability is the term we use to describe a system’s ability to cope with increased  load."  [Page32](zotero://open-pdf/library/items/74Y7IY96?page=10&annotation=PDH22A6I)



 "scalability means considering questions like “If the system grows in a particular way,  what are our options for coping with the growth?” and “How can we add computing  resources to handle the additional load?”"  [Page33](zotero://open-pdf/library/items/74Y7IY96?page=11&annotation=HW2JGZQE)



### "Describing Load"  [Page33](zotero://open-pdf/library/items/74Y7IY96?page=11&annotation=E43EBKAM)



 "Load can be described  with a few numbers which we call load parameters. The best choice of parameters  depends on the architecture of your system: it may be requests per second to a web  server, the ratio of reads to writes in a database, the number of simultaneously active  users in a chat room, the hit rate on a cache, or something else. Perhaps the average  case is what matters for you, or perhaps your bottleneck is dominated by a small  number of extreme cases"  [Page33](zotero://open-pdf/library/items/74Y7IY96?page=11&annotation=U677EN8F)



 ![[99 - Meta/Attachements/kleppmannDesigningDataIntensiveApplications/image-34-x63-y203.png]] [Page34](zotero://open-pdf/library/items/74Y7IY96?page=12&annotation=SAL66VUU)



 "In the example of Twitter, the distribution of followers per user (maybe weighted by  how often those users tweet) is a key load parameter for discussing scalability, since it  determines the fan-out load. Your application may have very different characteristics,  but you can apply similar principles to reasoning about its load."  [Page35](zotero://open-pdf/library/items/74Y7IY96?page=13&annotation=TDWPVD2A)



 "The final twist of the Twitter anecdote: now that approach 2 is robustly implemented,  Twitter is moving to a hybrid of both approaches. Most users’ tweets continue to be  fanned out to home timelines at the time when they are posted, but a small number  of users with a very large number of followers (i.e., celebrities) are excepted from this  fan-out."  [Page35](zotero://open-pdf/library/items/74Y7IY96?page=13&annotation=Q4GTZE9X)



### "Describing Performance"  [Page35](zotero://open-pdf/library/items/74Y7IY96?page=13&annotation=INN9ZUAM)



 "Once you have described the load on your system, you can investigate what happens  when the load increases. You can look at it in two ways:  • When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth, etc.) unchanged, how is the performance of your system  affected?  • When you increase a load parameter, how much do you need to increase the  resources if you want to keep performance unchanged?"  [Page35](zotero://open-pdf/library/items/74Y7IY96?page=13&annotation=EVUFRA75)



#### "Latency and response time"  [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=788ENXYT)



 "Latency and response time are often used synonymously, but they  are not the same. The response time is what the client sees: besides  the actual time to process the request (the service time), it includes  network delays and queueing delays. Latency is the duration that a  request is waiting to be handled—during which it is latent, awaiting service"  [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=6Q79UWJP)



 "In practice, in a system handling a variety of  requests, the response time can vary a lot. We therefore need to think of response  time not as a single number, but as a distribution of values that you can measure."  [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=XXSAFWCG)



 "But even in a scenario where you’d  think all requests should take the same time, you get variation: random additional  latency could be introduced by a context switch to a background process, the loss of a  network packet and TCP retransmission, a garbage collection pause, a page fault  forcing a read from disk, mechanical vibrations in the server rack [18], or many other  causes"  [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=2A9XBBFX)



 ![[99 - Meta/Attachements/kleppmannDesigningDataIntensiveApplications/image-36-x67-y193.png]] [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=RLEKAQYN)



 "the mean is not a very good metric if you want to know your “typical” response time, because it doesn’t tell you how many users actually experienced  that delay.  Usually it is better to use percentiles."  [Page36](zotero://open-pdf/library/items/74Y7IY96?page=14&annotation=VGSFDEPL)



 "the median a good metric if you want to know how long users typically  have to wait: half of user requests are served in less than the median response time,  and the other half take longer than the median."  [Page37](zotero://open-pdf/library/items/74Y7IY96?page=15&annotation=I3EIWL7A)



 "In order to figure out how bad your outliers are, you can look at higher percentiles:  the 95th, 99th, and 99.9th percentiles are common"  [Page37](zotero://open-pdf/library/items/74Y7IY96?page=15&annotation=NUSZPSX9)



 "High percentiles of response times, also known as tail latencies, are important  because they directly affect users’ experience of the service. For example, Amazon  describes response time requirements for internal services in terms of the 99.9th percentile, even though it only affects 1 in 1,000 requests. This is because the customers  with the slowest requests are often those who have the most data on their accounts  because they have made many purchases—that is, they’re the most valuable customers [19]."  [Page37](zotero://open-pdf/library/items/74Y7IY96?page=15&annotation=NJM9BB5U)



 "On the other hand, optimizing the 99.99th percentile (the slowest 1 in 10,000  requests) was deemed too expensive and to not yield enough benefit for Amazon’s  purposes. Reducing response times at very high percentiles is difficult because they  are easily affected by random events outside of your control, and the benefits are  diminishing."  [Page37](zotero://open-pdf/library/items/74Y7IY96?page=15&annotation=NGGUUR7I)



 "Queueing delays often account for a large part of the response time at high percentiles. As a server can only process a small number of things in parallel"  [Page37](zotero://open-pdf/library/items/74Y7IY96?page=15&annotation=R8N49RVY)



 "When generating load artificially in order to test the scalability of a system, the loadgenerating client needs to keep sending requests independently of the response time.  If the client waits for the previous request to complete before sending the next one,  that behavior has the effect of artificially keeping the queues shorter in the test than  they would be in reality, which skews the measurements [23]"  [Page38](zotero://open-pdf/library/items/74Y7IY96?page=16&annotation=8AXDZQRQ)



 "High percentiles become especially important in backend services that are called multiple times as part of serving a single end-user request. Even if you make the calls in  parallel, the end-user request still needs to wait for the slowest of the parallel calls to  complete. It takes just one slow call to make the entire end-user request slow"  [Page38](zotero://open-pdf/library/items/74Y7IY96?page=16&annotation=ULGDU485)



 "If you want to add response time percentiles to the monitoring dashboards for your  services, you need to efficiently calculate them on an ongoing basis."  [Page38](zotero://open-pdf/library/items/74Y7IY96?page=16&annotation=CJKMJ4P7)



 "The naïve implementation is to keep a list of response times for all requests within the  time window and to sort that list every minute. If that is too inefficient for you, there  are algorithms that can calculate a good approximation of percentiles at minimal  CPU and memory cost, such as forward decay [25], t-digest [26], or HdrHistogram  [27]."  [Page38](zotero://open-pdf/library/items/74Y7IY96?page=16&annotation=YFCFNXCE)



 "the right way of  aggregating response time data is to add the histograms [28]"  [Page38](zotero://open-pdf/library/items/74Y7IY96?page=16&annotation=9QM2NAC7)



 ![[99 - Meta/Attachements/kleppmannDesigningDataIntensiveApplications/image-39-x64-y409.png]] [Page39](zotero://open-pdf/library/items/74Y7IY96?page=17&annotation=NXTCD22H)



### "Approaches for Coping with Load"  [Page39](zotero://open-pdf/library/items/74Y7IY96?page=17&annotation=J5R4NV7A)



 "how do we maintain  good performance even when our load parameters increase by some amount?  An architecture that is appropriate for one level of load is unlikely to cope with 10  times that load. If you are working on a fast-growing service, it is therefore likely that  you will need to rethink your architecture on every order of magnitude load increase  —or perhaps even more often than that."  [Page39](zotero://open-pdf/library/items/74Y7IY96?page=17&annotation=X7MD9MID)



 "In reality, good architectures usually involve  a pragmatic mixture of approaches: for example, using several fairly powerful  machines can still be simpler and cheaper than a large number of small virtual  machines."  [Page39](zotero://open-pdf/library/items/74Y7IY96?page=17&annotation=F3WIMIL7)



 "Some systems are elastic, meaning that they can automatically add computing resources when they detect a load increase, whereas other systems are scaled manually (a  human analyzes the capacity and decides to add more machines to the system). An  elastic system can be useful if load is highly unpredictable, but manually scaled systems are simpler and may have fewer operational surprise"  [Page39](zotero://open-pdf/library/items/74Y7IY96?page=17&annotation=UHT8I9XY)



 "While distributing stateless services across multiple machines is fairly straightforward, taking stateful data systems from a single node to a distributed setup can introduce a lot of additional complexity. For this reason, common wisdom until recently  was to keep your database on a single node (scale up) until scaling cost or highavailability requirements forced you to make it distributed."  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=WKKNJKP5)



 "this common wisdom  may change, at least for some kinds of applications"  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=8RCQBF4M)



 "there is no such thing as a generic, one-size-fits-all scalable architecture"  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=DU5NC5SK)



 "a system that is designed to handle 100,000 requests per second, each  1 kB in size, looks very different from a system that is designed for 3 requests per  minute, each 2 GB in size—even though the two systems have the same data throughput."  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=IWDL7Y5D)



 "An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare—the load parameters. If those assumptions turn out to be wrong, the engineering effort for scaling is at  best wasted, and at worst counterproductive"  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=3MGGSHBT)



## "Maintainability"  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=3SL8GPCN)



 "that the majority of the cost of software is not in its initial development, but in its ongoing maintenance—fixing bugs, keeping its systems operational,  investigating failures, adapting it to new platforms, modifying it for new use cases,  repaying technical debt, and adding new features."  [Page40](zotero://open-pdf/library/items/74Y7IY96?page=18&annotation=5MCXD3YU)



 "Operability  Make it easy for operations teams to keep the system running smoothly.  Simplicity  Make it easy for new engineers to understand the system, by removing as much  complexity as possible from the system. (Note this is not the same as simplicity  of the user interface.)  Evolvability  Make it easy for engineers to make changes to the system in the future, adapting  it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity."  [Page41](zotero://open-pdf/library/items/74Y7IY96?page=19&annotation=E4DJNVVI)



### "Operability: Making Life Easy for Operations"  [Page41](zotero://open-pdf/library/items/74Y7IY96?page=19&annotation=AWY4MHVS)



 "“good operations can often work around the limitations of  bad (or incomplete) software, but good software cannot run reliably with bad operations” [12]."  [Page41](zotero://open-pdf/library/items/74Y7IY96?page=19&annotation=G9ITX567)



 "A good  operations team typically is responsible for the following, and more [29]:  • Monitoring the health of the system and quickly restoring service if it goes into a  bad state  • Tracking down the cause of problems, such as system failures or degraded performance • Keeping software and platforms up to date, including security patches  • Keeping tabs on how different systems affect each other, so that a problematic  change can be avoided before it causes damage"  [Page41](zotero://open-pdf/library/items/74Y7IY96?page=19&annotation=XVBPDT7Y)



 "• Anticipating future problems and solving them before they occur (e.g., capacity  planning)  • Establishing good practices and tools for deployment, configuration management, and more  • Performing complex maintenance tasks, such as moving an application from one  platform to another • Maintaining the security of the system as configuration changes are made  • Defining processes that make operations predictable and help keep the production environment stable  • Preserving the organization’s knowledge about the system, even as individual  people come and go"  [Page42](zotero://open-pdf/library/items/74Y7IY96?page=20&annotation=ABVMZCN7)



 "Data systems can do various things to  make routine tasks easy, including:  • Providing visibility into the runtime behavior and internals of the system, with  good monitoring • Providing good support for automation and integration with standard tools  • Avoiding dependency on individual machines (allowing machines to be taken  down for maintenance while the system as a whole continues running uninterrupted)  • Providing good documentation and an easy-to-understand operational model  (“If I do X, Y will happen”)  • Providing good default behavior, but also giving administrators the freedom to  override defaults when needed  • Self-healing where appropriate, but also giving administrators manual control  over the system state when needed • Exhibiting predictable behavior, minimizing surprises"  [Page42](zotero://open-pdf/library/items/74Y7IY96?page=20&annotation=VLU388BE)



### "Simplicity: Managing Complexity"  [Page42](zotero://open-pdf/library/items/74Y7IY96?page=20&annotation=PE7FLY3K)



 "There are various possible symptoms of complexity: explosion of the state space, tight  coupling of modules, tangled dependencies, inconsistent naming and terminology,  hacks aimed at solving performance problems, special-casing to work around issues  elsewhere, and many more. Much has been said on this topic already [31, 32, 33]"  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=JACZBK5P)



Try to research for theprimagean's video on abstraction I remember it has valid points that counter the author's point about abstractions "One of the best tools we have for removing accidental complexity is abstraction. A  good abstraction can hide a great deal of implementation detail behind a clean,  simple-to-understand façade. A good abstraction can also be used for a wide range of  different applications. Not only is this reuse more efficient than reimplementing a  similar thing multiple times, but it also leads to higher-quality software, as quality  improvements in the abstracted component benefit all applications that use it"  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=H9KXPX4L)



 "high-level programming languages are abstractions that hide machine  code, CPU registers, and syscalls. SQL is an abstraction that hides complex on-disk  and in-memory data structures, concurrent requests from other clients, and inconsistencies after crashes"  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=NN8D6YMN)



 "finding good abstractions is very hard. In the field of distributed systems,  although there are many good algorithms, it is much less clear how we should be  packaging them into abstractions that help us keep the complexity of the system at a  manageable level."  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=YF7XP6M9)



### "Evolvability: Making Change Easy"  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=VQG7C2LD)



 "It’s extremely unlikely that your system’s requirements will remain unchanged forever. They are much more likely to be in constant flux"  [Page43](zotero://open-pdf/library/items/74Y7IY96?page=21&annotation=3IP36J87)



 "The ease with which you can modify a data system, and adapt it to changing requirements, is closely linked to its simplicity and its abstractions: simple and easy-tounderstand systems are usually easier to modify than complex ones. But since this is  such an important idea, we will use a different word to refer to agility on a data system level: evolvability [34]."  [Page44](zotero://open-pdf/library/items/74Y7IY96?page=22&annotation=ZJUZBSKL)




%% end annotations %%

%% Import Date: 2024-09-08T16:54:50.246+03:00 %%
