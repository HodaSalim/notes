Title: High Performance MySQL-Error: `format` can only be applied to dates. Tried for format object
Author: Silvia Botros, Jeremy Tinley
Zotero Link: [PDF](zotero://select/library/items/7U54BS6H)

> [!NOTE]- Abstract
> 

%% begin annotations %%


**Imported: 2024-09-08**

# Chapter 1

 "This chapter provides a high-level overview of the MySQL server architecture, the  major differences between the storage engines, and why those differences are important."  [Page23](zotero://open-pdf/library/items/7U54BS6H?page=1&annotation=GCE843D9)



## "MySQL’s Logical Architecture"  [Page23](zotero://open-pdf/library/items/7U54BS6H?page=1&annotation=KHIKH8U5)



 "The topmost layer, clients, contains the services that aren’t unique to MySQL. They’re  services most network-based client/server tools or servers need: connection handling,  authentication, security, and so forth."  [Page23](zotero://open-pdf/library/items/7U54BS6H?page=1&annotation=DV4J2ZJ8)



 "The second layer is where things get interesting. Much of MySQL’s brains are here,  including the code for query parsing, analysis, optimization, and all the built-in functions (e.g., dates, times, math, and encryption). Any functionality provided across  storage engines lives at this level: stored procedures, triggers, and views, for example."  [Page23](zotero://open-pdf/library/items/7U54BS6H?page=1&annotation=PYRLCLR6)



https://dev.mysql.com/doc/refman/8.4/en/storage-engines.html "The third layer contains the storage engines. They are responsible for storing and  retrieving all data stored “in” MySQL. Like the various filesystems available for GNU/  Linux, each storage engine has its own benefits and drawbacks"  [Page23](zotero://open-pdf/library/items/7U54BS6H?page=1&annotation=H9PYP4QG)



 "MySQL 5.5 and newer versions support an API that can accept thread-pooling plug-ins, though not commonly used. The common practice for thread pooling is done at access layers, which we discuss in Chapter 5."  [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=PPS8YMPJ)



 "the storage engine API. This API hides differences between  storage engines and makes them largely transparent at the query layer. It also contains a couple of dozen low-level functions that perform operations such as “begin a  transaction” or “fetch the row that has this primary key.”"  [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=3MMQTQKH)



 ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-24-x68-y330.png]] [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=RAUBEF3P)



### "Connection Management and Security"  [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=RX37YVBC)



 "By default, each client connection gets its own thread within the server process. The  connection’s queries execute within that single thread, which in turn resides on one  core or CPU. The server maintains a cache of ready-to-use threads, so they don’t need  to be created and destroyed for each new connection.2"  [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=MR8LDDUP)



 "Once a client has connected, the server verifies whether the client has privileges for  each query it issues (e.g., whether the client is allowed to issue a SELECT statement  that accesses the Country table in the world database)."  [Page24](zotero://open-pdf/library/items/7U54BS6H?page=2&annotation=MPLV7A7L)



### "Optimization and Execution"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=V2MIVPZ3)



 "MySQL parses queries to create an internal structure (the parse tree) and then applies  a variety of optimizations. These can include rewriting the query, determining the  order in which it will read tables, choosing which indexes to use, and so on."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=JRWFCR6Y)



 "You can  pass hints to the optimizer through special keywords in the query, affecting its  decision-making process. You can also ask the server to explain various aspects of  optimization."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=XR7N2JPF)



 "The optimizer does not really care what storage engine a particular table uses, but the  storage engine does affect how the server optimizes the query. The optimizer asks the  storage engine about some of its capabilities and the cost of certain operations as well  as for statistics on the table data"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=FTY44CAY)



 "as concurrency increased, the query cache became a  notorious bottleneck. As of MySQL 5.7.20, the query cache was officially deprecated  as a MySQL feature, and in the 8.0 release, the query cache is fully removed."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=ICPJK5AL)



 "caching frequently served result sets is a good practice. While outside the scope of this book, a  popular design pattern is to cache data in memcached or Redis."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=GMY8VZEN)



## "Concurrency Control"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=4YPX6Y4Q)



 "Any time more than one query needs to change data at the same time, the problem of  concurrency control arises"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=HTTEBGQS)



 "MySQL has to do this at  two levels: the server level and the storage-engine level."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=UA7L395K)



 "To illustrate how MySQL handles concurrent work on the same set of data, we will  use a traditional spreadsheet file as an example"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=WF228HZN)



 "Assume the file is on your laptop and only you  have access to it. There are no potential conflicts;"  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=WLYCFVK2)



 "Now, imagine you need to collaborate with a coworker on that spreadsheet."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=BILSBT5J)



 "What happens when both of  you need to make changes to this file at the same time? What if we have an entire  team of people actively trying to edit, add, and remove cells from this spreadsheet?  We can say that they should take turns making changes, but that is not efficient."  [Page25](zotero://open-pdf/library/items/7U54BS6H?page=3&annotation=H7V6Y6CZ)



### "Read/Write Locks"  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=ESUIYYHD)



 "There’s nothing wrong with multiple clients reading the same file simultaneously; because they aren’t making changes"  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=NKHYH9R2)



 "but a reader could come  away with a corrupted or inconsistent view of the data. So, to be safe, even reading  from a spreadsheet requires special care."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=622LXWRM)



 "The solution to this classic problem of concurrency control is rather simple. Systems  that deal with concurrent read/write access typically implement a locking system that  consists of two lock types. These locks are usually known as shared locks and exclusive  locks, or read locks and write locks."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=7UF5S85Y)



 "Read locks on a resource are shared, or mutually nonblocking: many clients can read from a resource at the same time and not interfere with one another."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=XAHSFG4F)



 "Write locks, on the other hand, are exclusive—that is, they block both read locks and  other write locks—because the only safe policy is to have a single client writing to the  resource at a given time and to prevent all reads when a client is writing."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=CQ992DAW)



 "If a database server is performing in an acceptable manner, this management of locks is fast enough to not be  noticeable to the clients."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=9DU43V78)



### "Lock Granularity"  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=2R5DZBA4)



 "One way to improve the concurrency of a shared resource is to be more selective  about what you lock. Rather than locking the entire resource, lock only the part that  contains the data you need to change"  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=XPER6VZG)



 "Minimizing the amount of data that you lock at any one time lets  changes to a given resource occur simultaneously, as long as they don’t conflict with  each other."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=66UY2W3P)



 "Unfortunately, locks are not free—they consume resources. Every lock operationgetting a lock, checking to see whether a lock is free, releasing a lock, and so on—has  overhead. If the system spends too much time managing locks instead of storing and  retrieving data, performance can suffer."  [Page26](zotero://open-pdf/library/items/7U54BS6H?page=4&annotation=E6QVS43U)



 "A locking strategy is a compromise between lock overhead and data safety, and that  compromise affects performance"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=NYF7VEPZ)



 "commercial database servers don’t give you  much choice: you get what is known as row-level locking in your tables, with a variety  of often complex ways to give good performance with many locks"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=I9DQIJZI)



 "MySQL, on the other hand, does offer choices. Its storage engines can implement  their own locking policies and lock granularities."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=42HEJXXH)



 "fixing the granularity at a certain level can  improve performance for certain uses yet make that engine less suited for other purposes."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=WLHVEEMI)



 "Because MySQL offers multiple storage engines, it doesn’t require a single  general-purpose solution. Let’s have a look at the two most important lock strategies"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=MZMHT3GI)



#### "Table locks"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=YMFSLLKP)



 "The most basic locking strategy available in MySQL, and the one with the lowest  overhead"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=4Z4N2VFQ)



 "A table lock is analogous to the spreadsheet locks described  earlier: it locks the entire table."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=GGX37FSZ)



https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html "Table locks have variations for improved performance in specific situations. For  example, READ LOCAL table locks allow some types of concurrent write operations.  Write and read lock queues are separate with the write queue being wholly of higher  priority than the read queue."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=S25TYGQT)



#### "Row locks"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=CPUX4YK8)



 "The locking style that offers the greatest concurrency (and carries the greatest overhead)"  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=7EBLUN45)



 "row locks would  be the same as locking just the row in the spreadsheet. This strategy allows multiple  people to edit different rows concurrently without blocking one another."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=XNX3H9VF)



 "but the cost is more overhead in having to  keep track of who has each row lock, how long they have been open, and what kind of  row locks they are as well as cleaning up locks when they are no longer needed."  [Page27](zotero://open-pdf/library/items/7U54BS6H?page=5&annotation=NVUXNK4Z)



 "Row locks are implemented in the storage engine, not the server. The server is  mostly4 unaware of locks implemented in the storage engines"  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=XL6MQ8LN)



 "the storage engines all implement locking in  their own ways."  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=CKLSEGDC)



## "Transactions"  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=CBF9XWRB)



 "A transaction is a group of SQL statements that are  treated atomically, as a single unit of work. If the database engine can apply the entire  group of statements to a database, it does so, but if any of them can’t be done because  of a crash or other reason, none of them is applied. It’s all or nothing."  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=M5UX8AB5)



 "A banking application is the classic example of why transactions are necessary.5 Imagine a bank’s database with two tables: checking and savings."  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=EB9WI7RD)



 "you need to perform at least three steps: 
1. Make sure her checking account balance is greater than $200. 
2. Subtract $200 from her checking account balance.
3. Add $200 to her savings account balance."  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=PEMC5VLK)



 "You start a transaction with the START TRANSACTION statement and then either make  its changes permanent with COMMIT or discard the changes with ROLLBACK"  [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=TLAIVAPS)



 ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-28-x86-y188.png]] [Page28](zotero://open-pdf/library/items/7U54BS6H?page=6&annotation=HLUKPWEV)



 "You could  see connection drops, timeouts, or even a crash of the database server running them  midway through the operations. This is typically why highly complex and slow twophase-commit systems exist: to mitigate against all sorts of failure scenarios."  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=KBEYHS4E)



 "Transactions aren’t enough unless the system passes the ACID test. ACID stands for  atomicity, consistency, isolation, and durability"  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=X453NEMJ)



 "Atomicity  A transaction must function as a single indivisible unit of work so that the entire  transaction is either applied or never committed. When transactions are atomic,  there is no such thing as a partially completed transaction: it’s all or nothing."  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=LURIQGUE)



 "Consistency  The database should always move from one consistent state to the next. In our  example, consistency ensures that a crash between lines 3 and 4 doesn’t result in  $200 disappearing from the checking account. If the transaction is never committed, none of the transaction’s changes are ever reflected in the database."  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=5M57B7BU)



 "Isolation  The results of a transaction are usually invisible to other transactions until the  transaction is complete. This ensures that if a bank account summary runs after  line 3 but before line 4 in our example, it will still see the $200 in the checking  account. When we discuss isolation levels later in this chapter, you’ll understand  why we said “usually invisible.”"  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=F9UP2N3K)



 "Durability  Once committed, a transaction’s changes are permanent. This means the changes  must be recorded such that data won’t be lost in a system crash. Durability is a  slightly fuzzy concept, however, because there are actually many levels. Some  durability strategies provide a stronger safety guarantee than others, and nothing  is ever 100% durable (if the database itself were truly durable, then how could  backups increase durability?)."  [Page29](zotero://open-pdf/library/items/7U54BS6H?page=7&annotation=AG6KBAZY)



### "Isolation Levels"  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=VSGJD8DJ)



https://blog.acolyer.org/2016/02/24/a-critique-of-ansi-sql-isolation-levels/ "The ANSI SQL standard defines four isolation levels."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=9Z5GDWU4)



 "The goal of this standard is to define the  rules for which changes are and aren’t visible inside and outside a transaction. Lower  isolation levels typically allow higher concurrency and have lower overhead."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=PY9YKIWS)



 "Each storage engine implements isolation levels slightly differently,  and they don’t necessarily match what you might expect if you’re  used to another database product (thus, we won’t go into exhaustive detail in this section). You should read the manuals for  whichever storage engines you decide to use."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=NJD338W6)



 "READ UNCOMMITTED  In the READ UNCOMMITTED isolation level, transactions can view the results of  uncommitted transactions. At this level, many problems can occur unless you  really, really know what you are doing and have a good reason for doing it. This  level is rarely used in practice because its performance isn’t much better than the  other levels, which have many advantages. Reading uncommitted data is also  known as a dirty read."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=KBTFCYE7)



 "READ COMMITTED  The default isolation level for most database systems (but not MySQL!) is READ  COMMITTED. It satisfies the simple definition of isolation used earlier: a transaction  will continue to see changes made by transactions that were committed after it  began, and its changes won’t be visible to others until it has committed. This level  still allows what’s known as a nonrepeatable read. This means you can run the  same statement twice and see different data."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=MZSU3IJG)



 "REPEATABLE READ REPEATABLE READ solves the problems that READ UNCOMMITTED allows. It guarantees that any rows a transaction reads will “look the same” in subsequent reads within the same transaction, but in theory it still allows another tricky problem: phantom reads. Simply put, a phantom read can happen when you select some range of rows, another transaction inserts a new row into the range, and then you select the same range again; you will then see the new “phantom” row.
REPEATABLE READ is MySQL’s default transaction isolation level."  [Page30](zotero://open-pdf/library/items/7U54BS6H?page=8&annotation=XWAEFR7Z)



 "SERIALIZABLE  The highest level of isolation, SERIALIZABLE, solves the phantom read problem  by forcing transactions to be ordered so that they can’t possibly conflict. In a nutshell, SERIALIZABLE places a lock on every row it reads. At this level, a lot of  timeouts and lock contention can occur. We’ve rarely seen people use this isolation level, but your application’s needs might force you to accept the decreased  concurrency in favor of the data safety that results."  [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=EJ2L53NI)



 ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-31-x68-y324.png]] [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=529H5T7B)



### "Deadlocks"  [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=7CCCU8ZS)



 "A deadlock is when two or more transactions are mutually holding and requesting  locks on the same resources, creating a cycle of dependencies."  [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=6ULGUW3G)



 "Deadlocks occur when  transactions try to lock resources in a different order. They can happen whenever  multiple transactions lock the same resources."  [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=8Q4TMUEW)



Example of a deadlock causing transactions ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-31-x70-y83.png]] [Page31](zotero://open-pdf/library/items/7U54BS6H?page=9&annotation=5CQRDA7U)



 "Each transaction will execute its first query and update a row of data, locking that  row in the primary key index and any additional unique index it is part of in the process. Each transaction will then attempt to update its second row, only to find that it is  already locked. The two transactions will wait forever for each other to complete  unless something intervenes to break the deadlock."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=NCP8IDJ3)



 "To combat this problem, database systems implement various forms of deadlock  detection and timeouts."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=YP88ICQH)



 "InnoDB storage  engine, will notice circular dependencies and return an error instantly."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=FH6GMH5N)



 "Others will give up after the query exceeds a lock wait timeout, which is not always  good."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=3E9WXHQQ)



 "Lock behavior and order are storage engine specific, so some storage engines might  deadlock on a certain sequence of statements even though others won’t."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=MNG94KWW)



some storage engines lock entire tables, and others implement more complex row-based locking. All that logic lives for the most part in the storage engine layer. "Deadlocks  have a dual nature: some are unavoidable because of true data conflicts, and some are  caused by how a storage engine works.7"  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=CNU73VZX)



 "Once they occur, deadlocks cannot be broken without rolling back one of the transactions, either partially or wholly"  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=XBE6XGYD)



 "Many applications can simply  retry their transactions from the beginning, and unless they encounter another deadlock, they should be successful."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=WQQD4WR5)



### "Transaction Logging"  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=K3SGXFYE)



 "Transaction logging helps make transactions more efficient. Instead of updating the  tables on disk each time a change occurs, the storage engine can change its inmemory copy of the data."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=TBUDN5CA)



 "The storage engine can then write a record  of the change to the transaction log, which is on disk and therefore durable. This is  also a relatively fast operation, because appending log events involves sequential I/O  in one small area of the disk instead of random I/O in many places"  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=5LNI58FF)



 "most storage engines that use  this technique (known as write-ahead logging) end up writing the changes to disk  twice."  [Page32](zotero://open-pdf/library/items/7U54BS6H?page=10&annotation=FQX6EH2F)



 "If there’s a crash after the update is written to the transaction log but before the  changes are made to the data itself, the storage engine can still recover the changes  upon restart. The recovery method varies between storage engines."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=VYE9JNGN)



### "Transactions in MySQL"  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=5VKTHFVB)



 "While MySQL has traditionally offered a number of storage engines that  support transactions, InnoDB is now the gold standard and the recommended engine  to use."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=NPNRJTS9)



#### "Understanding AUTOCOMMIT"  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=3HM9DPB6)



 "By default, a single INSERT, UPDATE, or DELETE statement is implicitly wrapped in a  transaction and committed immediately. This is known as AUTOCOMMIT mode."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=NX8BYSNI)



 "By disabling this mode, you can execute a series of statements within a transaction and, at  conclusion, COMMIT or ROLLBACK."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=9KI2REQX)



 "You can enable or disable the AUTOCOMMIT variable for the current connection by  using a SET command. The values 1 and ON are equivalent, as are 0 and OFF"  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=3KFD876R)



 "you are always in a transaction until you issue a COMMIT  or ROLLBACK. MySQL then starts a new transaction immediately"  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=VHPJ7VL7)



 "Changing the value of AUTOCOMMIT has no effect  on nontransactional tables, which have no notion of committing or rolling back  changes."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=A6Y9K7KJ)



 "Certain commands, when issued during an open transaction, cause MySQL to commit the transaction before they execute. These are typically DDL commands that  make significant changes, such as ALTER TABLE, but LOCK TABLES and some other  statements also have this effect."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=ZAFJPS4M)



 "MySQLlets you set the isolation level using the SET TRANSACTION ISOLATION LEVEL  command, which takes effect when the next transaction starts."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=JLQVX6K2)



 "`SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;`"  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=LJT7FVTX)



 "It is preferable to set the isolation you use most at the server level and only change it  in explicit cases. MySQL recognizes all four ANSI standard isolation levels, and  InnoDB supports all of them."  [Page33](zotero://open-pdf/library/items/7U54BS6H?page=11&annotation=DKQZQ9BL)



#### "Mixing storage engines in transactions"  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=57B4MJ8C)



 "MySQL doesn’t manage transactions at the server level. Instead, the underlying storage engines implement transactions themselves."  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=VAMUTTG2)



 "If you mix transactional and nontransactional tables (for instance, InnoDB and MyISAM tables) in a transaction, the transaction will work properly if all goes well. However, if a rollback is required, the changes to the nontransactional table can’t be  undone."  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=R4EUDZDH)



 "This is why it is  really important to pick the right storage engine for each table and to avoid mixing  storage engines in your application logic at all costs."  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=SLF7QA4F)



#### "Implicit and explicit locking"  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=GPTE4C6C)



 "InnoDB uses a two-phase locking protocol. It can acquire locks at any time during a  transaction, but it does not release them until a COMMIT or ROLLBACK. It releases all the  locks at the same time. The locking mechanisms described earlier are all implicit.  InnoDB handles locks automatically, according to your isolation level"  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=A4DCPUDF)



8 These locking hints are frequently abused and should usually be avoided.


9 SELECT...FOR SHARE is a MySQL 8.0 feature that replaces SELECT...LOCK IN SHARE MODE of previous versions. "InnoDB also supports explicit locking, which the SQL standard does not  mention at all:8, 9  SELECT ... FOR SHARE SELECT ... FOR UPDATE"  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=RLSJF789)



 "MySQL also supports the LOCK TABLES and UNLOCK TABLES commands, which are  implemented in the server, not in the storage engines."  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=HWFZE28R)



 "LOCK TABLES is unnecessary because InnoDB supports  row-level locking"  [Page34](zotero://open-pdf/library/items/7U54BS6H?page=12&annotation=HIREN9TL)



 "The interaction between LOCK TABLES and transactions is complex,  and there are unexpected behaviors in some server versions. Therefore, we recommend that you never use LOCK TABLES unless you  are in a transaction and AUTOCOMMIT is disabled, no matter what  storage engine you are using."  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=7HXHG8DB)



## "Multiversion Concurrency Control"  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=WYIFLDWQ)



MVCC isn't unique to MySQL though although with some differences of course in the implementation as MVCC doesn't have a standard "Most of MySQL’s transactional storage engines don’t use a simple row-locking mechanism. Instead, they use row-level locking in conjunction with a technique for increasing concurrency known as multiversion concurrency control (MVCC)."  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=EJUMWBBN)



 "You can think of MVCC as a twist on row-level locking; it avoids the need for locking  at all in many cases and can have much lower overhead."  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=6XGYFW9N)



 "MVCC works by using snapshots of the data as it existed at some point in time. This  means transactions can see a consistent view of the data, no matter how long they  run. It also means different transactions can see different data in the same tables at  the same time!"  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=AJ8YKCXE)



 "Each storage engine implements MVCC differently. Some of the variations include  optimistic and pessimistic concurrency control"  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=GYJZVTTQ)



 "InnoDB implements MVCC by assigning a transaction ID for each transaction that  starts. That ID is assigned the first time the transaction reads any data. When a record  is modified within that transaction, an undo record that explains how to revert that  change is written to the undo log, and the rollback pointer of the transaction is pointed at that undo log record. This is how the transaction can find the way to roll back if  needed."  [Page35](zotero://open-pdf/library/items/7U54BS6H?page=13&annotation=QBL3J2FI)



 ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-36-x67-y401.png]] [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=CCGXHYCL)



 "When a different session reads a cluster key index record, InnoDB compares the  record’s transaction ID versus the read view of that session. If the record in its current  state should not be visible (the transaction that altered it has not yet committed), the  undo log record is followed and applied until the session reaches a transaction ID  that is eligible to be visible. This process can loop all the way to an undo record that  deletes this row entirely, signaling to the read view that this row does not exist."  [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=PL8Y2CLY)



 "Records in a transaction are deleted by setting a “deleted” bit in the “info flags” of the  record. This is also tracked in the undo log as a “remove delete mark.”"  [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=FYIXURVY)



https://blog.jcole.us/2014/04/16/the-basics-of-the-innodb-undo-logging-and-history-system/ "all undo log writes are also redo logged because the undo  log writes are part of the server crash recovery process and are transactional."  [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=QWIJUFC6)



 "The result of all this extra record keeping is that most read queries never acquire  locks. They simply read data as fast as they can, making sure to select only rows that  meet the criteria."  [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=YWUBK6VZ)



 "The drawbacks are that the storage engine has to store more data  with each row, do more work when examining rows, and handle some additional  housekeeping operations."  [Page36](zotero://open-pdf/library/items/7U54BS6H?page=14&annotation=UAA8CRXS)



 "MVCC works only with the REPEATABLE READ and READ COMMITTED isolation levels."  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=VI4F4DRY)



 "READ UNCOMMITTED isn’t MVCC compatible12 because queries don’t read the row version that’s appropriate for their transaction version; they read the newest version, no  matter what. SERIALIZABLE isn’t MVCC compatible because reads lock every row  they return."  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=D5LIYSTZ)



## "Replication"  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=KAU8NG7X)



 "MySQL is designed for accepting writes on one node at any given time. This has  advantages in managing consistency but leads to trade-offs when you need the data  written in multiple servers or multiple locations."  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=IC8XAFI3)



 "MySQL offers a native way to distribute writes that one node takes to additional nodes. This is referred to as replication."  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=DEJ6MAZD)



 "In MySQL, the source node has a thread per replica that is logged in as a  replication client that wakes up when a write occurs, sending new data. In Figure 1-3,  we show a simple example of this setup, which is usually called a topology tree of multiple MySQL servers in a source and replica setup."  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=2F6T4J9R)



 ![[99 - Meta/Attachements/botrosHighPerformanceMySQL/image-37-x68-y287.png]] [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=WYARNG8B)



 "For any data you run in production, you should use replication and have at least three  more replicas, ideally distributed in different locations"  [Page37](zotero://open-pdf/library/items/7U54BS6H?page=15&annotation=HU883ZR5)



## "Datafiles Structure"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=YZW77GEV)



 "In version 8.0, MySQL redesigned table metadata into a data dictionary that is  included with a table’s .ibd file."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=4T9EMIBK)



 "Instead of relying only on informa  tion_schema for retrieving table definition and metadata during operations, we are  introduced to the dictionary object cache, which is a least recently used (LRU)-based  in-memory cache of partition definitions, table definitions, stored program definitions, charset, and collation information."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=ZT7PJUG8)



 "reduces I/O and is efficient, especially if a subset of  tables is what sees the most activity and therefore is in the cache most often"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=2QTB8USU)



 "The .ibd  and .frm files are replaced with serialized dictionary information (.sdi) per table."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=7HVUGX5K)



## "The InnoDB Engine"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=XB6Y3XJL)



 "InnoDB is the default transactional storage engine for MySQL and the most important and broadly useful engine overall."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=8PTMM5IL)



 "It was designed for processing many shortlived transactions that usually complete rather than being rolled back."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=TK289ER8)



 "Its  performance and automatic crash recovery make it popular for nontransactional  storage needs too."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=7XG2C9DH)



 "It is best practice to use the InnoDB storage engine as the default  engine for any application. MySQL made that easy by making  InnoDB the default engine a few major versions ago"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=TRPLHXHG)



 "By default, InnoDB  stores its data in a series of datafiles that are collectively known as a tablespace. A  tablespace is essentially a black box that InnoDB manages all by itself."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=IIJ7K9W8)



 "InnoDB uses MVCC to achieve high concurrency, and it implements all four SQL  standard isolation levels. It defaults to the REPEATABLE READ isolation level, and it has  a next-key locking strategy that prevents phantom reads in this isolation level: rather  than locking only the rows you’ve touched in a query, InnoDB locks gaps in the index  structure as well, preventing phantoms from being inserted."  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=L76F7ABJ)



will be discussed in Chapter 8 "InnoDB tables are built on a clustered index,"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=II9QFI99)



 "InnoDB’s index structures are very different from those of most other MySQL storage engines. As a result, it provides very fast primary key lookups. However, secondary indexes (indexes that aren’t the primary key) contain the primary key columns, so if your primary key is large, other indexes will also be large. You should strive for a small primary key if you’ll have many indexes on a table"  [Page38](zotero://open-pdf/library/items/7U54BS6H?page=16&annotation=NV6FIH9Q)



 "InnoDB has a variety of internal optimizations. These include predictive read-ahead  for prefetching data from disk, an adaptive hash index that automatically builds hash  indexes in memory for very fast lookups, and an insert buffer to speed inserts."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=EC4WTB27)



Check this link as suggested by the author: https://dev.mysql.com/doc/refman/8.0/en/innodb-locking-transaction-model.html

InnoDB because of its MVCC architecture, there are many subtle things we should be aware of as we build Apps using it [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=YMPIVVSI)



 "Working with a storage engine  that maintains consistent views of the data for all users, even when some users are  changing data, can be complex."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=ZEI4BMEP)



 "As a transactional storage engine, InnoDB supports truly “hot” online backups  through a variety of mechanisms, including Oracle’s proprietary MySQL Enterprise  Backup and the open source Percona XtraBackup."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=6X46JEPQ)



Will be discussed in Chapter 6 "Beginning with MySQL 5.6, InnoDB introduced online DDL, which at first had limited use cases that expanded in the 5.7 and 8.0 releases. In-place schema changes allow  for specific table changes without a full table lock and without using external tools,  which greatly improve the operationality of MySQL InnoDB tables"  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=PMT3BGWQ)



### "JSON Document Support"  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=PU9B8WI8)



 "First introduced to InnoDB as part of the 5.7 release, the JSON type arrived with  automatic validation of JSON documents as well as optimized storage that allows for  quick read access, a significant improvement to the trade-offs of old-style binary large  object (BLOB) storage engineers used to resort to for JSON documents"  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=GKK7CB6H)



 "InnoDB also introduced SQL functions to support rich  operations on JSON documents."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=Q6QTLUX4)



 "MySQL 8.0.7 adds the  ability to define multivalued indexes on JSON arrays."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=U5MDFBMB)



 "We go  over the use and performance implications of the JSON data type in “JSON Data” on  page 139 in Chapter 6."  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=HA2GA6CF)



### "Data Dictionary Changes"  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=NNTAWKQ4)



 "Another major change in MySQL 8.0 is removing file-based table metadata storage  and moving to a data dictionary using InnoDB table storage. This change brings all of  InnoDB’s crash-recovery transactional benefits to operations like changes to tables"  [Page39](zotero://open-pdf/library/items/7U54BS6H?page=17&annotation=EY9FU8KX)



 "also require major changes in operating a MySQL server. Most notably, back-up  processes that used to rely on the table metadata files now have to query the new data  dictionary to extract table definitions"  [Page40](zotero://open-pdf/library/items/7U54BS6H?page=18&annotation=226VI2Y3)



### "Atomic DDL"  [Page40](zotero://open-pdf/library/items/7U54BS6H?page=18&annotation=STFDDL5M)



 "MySQL 8.0 introduced atomic data definition changes. This means that data  definition statements now can either wholly finish successfully or be wholly rolled  back."  [Page40](zotero://open-pdf/library/items/7U54BS6H?page=18&annotation=FX378CCM)




%% end annotations %%

%% Import Date: 2024-09-08T00:13:40.829+03:00 %%
