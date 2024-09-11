## [[ACID]]
ACID: stands for "Atomicity, Consistency, Isolation, Durability"
### What is a transaction
A transaction is nothing but a collection of SQL queries that are treated as a one unit of work. The most famous example which I believe comes from the roots of relational databases is financial transactions which consists of (SELECT, UPDATE, UPDATE)
#### Transaction Lifespan
- Transaction BEGIN
- Transaction COMMIT -> what is exactly a commit ? a lot of database design choices come into commit, refer back to [[kleppmannDesigningDataIntensiveApplications]] Transactions chapter as it goes even more in depth in the different commit scenarios. What happens when the DB crashes during a commit for example ? 
- Transaction ROLLBACK

#### Nature of Transactions
- Usually transactions are used to modify data or even delete it, however it's possible and normal to have a read-only transaction, example: generating a report and use the snapshot feature to get the data at a specific point of time.

### Atomicity
it means simply that all queries in a single transaction must succeed like an "Atom" it can't be split if one query fails the whole transaction fails and needs to rollback. If the database crashes before a transaction is committed all the successful queries must rollback once the database restarts and restart the query from start if we chose to ,, but how does it rollback ? does it go back to a snapshot ? does it go and delete the action from disk ? 

### Isolation 
to understand isolation [[nasserFundamentalsDatabaseEngineering]] suggest that we need to answer this question "Can my inflight transaction see changes made by other transactions?" the lack of isolation or weak isolation, or maybe we can say not text-book isolation with concurrent requests can result in a multiple issues:
- Dirty reads
  انت شايف تغيرات من ترانزاكشن تانية بس هي لسه مش كوميتيد فممكن تتمسح او تقع 
  ![[Screenshot 2024-09-10 at 8.40.37 AM.png]]
- Non-repeatable reads -> expensive to fix it's not easy, and the fix varies from one DB to another.
  لما تعمل كويريز مختلفة المفروض يقروا من نفس الحتة بس كل واحدة يرجعلها نتيجة مختلفة بمعنى ان مش كلهم بيتكررلهم نفس الread 
  ![[Screenshot 2024-09-10 at 8.41.13 AM.png]]
- Phantom reads: happens with a committed value which is what differentiates it from dirty-reads, and it's a row that you can't really lock which differentiates it from non-repeatable reads and where the name comes from 
  الحاجات اللي مينفعش تقراها فعلا علشان هي لسه مش موجودة اصلا، مثلا انت بتقرا من جدول وحد بيضيف صف تاني عليها فيجيلك صف تاني زيادة بس انت مش عارف تشوفه فعلا لانه لسه مش committed مثلا لما تعد ال entries تلاقي مثلا ١٠٠ بس انت مش عارف تقرا غير ٩٩ بس
  ![[Screenshot 2024-09-10 at 8.41.37 AM.png]]
- Lost updates
  زي لما تبوست على حسابك بس لما تريفريش الحساب متلاقيش البوست لانه لسه الread مش synced مع الwrite اللي انت عملته
  ![[Screenshot 2024-09-10 at 8.41.52 AM.png]]
#### Isolation levels for inflight transactions
- Read uncommitted -> No Isolation, any change from the outside is visible to the transaction, committed or not.
- Read committed -> Each query in a transaction only sees committed changes by other transactions
- Repeatable Read -> The transaction will make sure that when a query reads a row, that row will remain unchanged while its running.
- Snapshot -> Each query in a transaction only sees changes that have been committed up to the start of the transaction. It's like a snapshot version of the database at that moment.
- Serializable -> Transactions are run as if they serialized one after the other. Each DBMS implements Isolation level differently
![[Screenshot 2024-09-10 at 8.50.28 AM.png]]
#### Database Implementation of Isolation
- Each DBMS implements Isolation level differently
- Pessimistic -> Row level locks, table locks, page locks to avoid lost updates (MySQL InnoDB implements row locks by default [[botrosHighPerformanceMySQL]])
- Optimistic -> No locks, just track if things changed and fail the transaction if so
- Repeatable read “locks” the rows it reads but it could be expensive if you read a lot of rows, postgres implements RR as snapshot. That is why you don’t get phantom reads with postgres in repeatable read
- Serializable are usually implemented with optimistic concurrency control, you can implement it pessimistically with SELECT FOR UPDATE

### Consistency
- Consistency in data
- Consistency in reads

Some databases sacrifice consistency for speed and efficiency, consistency basically means persistence of data, all reads on the same data should get consistent results meaning that the data itself is consistent as so are the reads.

Consistency in data is defined by the user, and usually comes down to enforcing referential integrity which depends on atomicity ensures it. Isolation may lead to inconsistency however. 

#### Consistency in reads
- If a transaction committed a change will a new transaction immediately see the change? 
- Affects the system as a whole
  مثلا لو عندك ماستر داتابيز وكدا فولور فلو مثلا الread حصل على فولور هيجيله احدث write علي الماستر ولا لا ؟ الconsistency في الحالة دي لازم تكون متطبقة على السيستم كله masters and followers
- Relational and NoSQL databases suffer from this
- Eventual consistency

### Durability
It's basically persisting the writes that a user makes to a database to a non-volatile storage system (disk) so even if the database crashed after a committed transaction the data would still be there
Durability is slow, it implies writing to disk and disks are slow so durability is inherently slow. 

#### Durability techniques
- WAL -> write ahead log
  writing a lot of data to disk is expensive (indexes, data, files, ...), this is why DBMSs persist a compressed version of the changes knows as WAL 
- Asynchronous snapshot
- AOF -> append only file 

 a write request usually goes to the OS cache, the OS wants to batch writes to the disk for better performance. 
 مثلا لو بنعمل WAL ال OS هيقول للداتابيز تمام كتبت بس في الحقيقية ال OS كتب على الcache فلو ال OS وقع الداتا دي هتروح في الحالة دي الداتابيز عندها حل وهو ال Fsync command اللي بيجبر ال OS انه يكتب على disk بشكل مباشر بس طبعا ال Fsync is expensive and slow 
 there is always a tradeoff ! 

## Database Internals
### How tables and indexes are stored on disk
![[How+tables+and+indexes+are+stored+on+disk.pdf]]

a page is nothing but a fix sized memory location which translates to a disk location of different bytes that's it 
unlike RAM where it's addressed using pointers disk uses pages it reads a whole page by a time so it's either page + or nothing you can't access just a single row you get the whole page in a single I/O

### Row-based vs Column-based Databases
![[Row-Based+vs+Column-Based+Databases.pdf]]


## Indexing

## B-Trees

## Partitioning

## Sharding

## Concurrency Control

## Replication

## Database System Design

## Database Engines
