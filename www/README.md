# Why

My proposal addresses platform considerations that are not covered in the brief
but that I believe are nevertheless essential to the enterprise. These are
concerns I have seen stated over and over again in RFP requirements at multiple
Healthcare IT companies. They are seldom if ever addressed satisfactorily, most
effort is concentrated on putting a functioning system in front of users and
these concerns remain secondary.

* Audit
* Data integrity
* Privacy and security

## Audit

Audit is a common requirement that I see expressed in virtually every RFP for
healthcare system that I encounter. Typically several concerns are lumped
together under this noun.

* Audit of the records being written
* Integrity of the records after being written
* Audit of the records being read

### Why my approach is great

#### Easy to query

Querying the data boils down to a 2-step process

* Identifying the revision of the data you wish to examine
* Performing normal everyday operations on that data
* No need to account for audit metadata in normal operation

#### Reduced overhead

This system preserves every revision of the data but only imposes a small
overhead on each revision. Data is not copied for the purposes of auditing.
All revisions of the data are preserved as-is without abridgement.

Data is not copied during normal write operations.

### Why RDBMS suck for audit

RDBMs require design compromises to be auditable.

* Store audit logs separately
* Design primary data to be auditable

#### "Auditable" data

This often takes the form of adding timestamps and other audit fields to
every row in the database.

This imposes additional overheads on normal operations of the system ;

* Reduced ability to impose referential integrity
* Increased difficulty of writing basic queries
* Increased disk consumption
* Increased processor load

#### Separate audit data

This design writes audit data to separate structures.

* A copy of the existing structures (perhaps with extra audit fields)
* A general log of data changes

The disadvantages of this approach include

* Hard to query - often data is unstructured
* Data is often transformed in a way which abridges it and removes data
* Data is copied during normal write operations

### Why the proposal will improve this

By using a data structure inspired by that of a programmers version control
system, it will be possible to examine the full history of the data, including
the provision of a full snapshot as it was available to any client at any point
in it's history. Because the construction of this record would be an intrinsic
part of writing any record to the data store

* Writing this history would be an intrinsic part of adding any record to the
  data store 
  * No additional programming effort required
* The data supporting the audit history is not an intrinsic part of the data
  * No overhead to accommodate the presence of audit data in normal data operations
* The audit data forms part of the container the data is kept in, rather than
  * Being a separate log
    * No extra overhead to write to a separate logging system
  * Being a part of the data
    * No need to design data that contains its own history
    * New forms of data get the intrinsic audit capacity of the system for free

This design also provides

* A means of non-repudiation through signing of metadata
* Protection against tampering through chained cryptographic hashing of metadata and data
* A well designed method of merging records created at multiple loci of the system
* A distributed data storage model which permits
  * Replication
  * Offline working



### Why RDBMs suck for representing patient data

Relational databases are designed for high-volume, low data size, homogenous, transactional
data.

Patient records are relatively low volume, high data size, highly heterogenous data.
One only has to picture the typical patient notes folder - a big fat cardboard
envelope containing a large variety of different data formats, inlcuding a lot
of unstructured longhand notes - to realize that a system based on something akin
to writing very small pieces of text on carefully printed index cards and filing
each in it's own drawer, indexed on the numbers of the other cards, probably isn't
a good conceptual fit. This matters tremendously when writing, growing, and
amending systems. The author has seen systems with *many hundreds* of tables that 
required extensive collaboration between system architects, designers, and 
programmers to amend. A ward clerk doesn't think twice about *just filing that
non-standard form from the other hospital with all the others*.


### Why RDBMs suck for integrity

Relational databases are not designed with any special controls for integrity
in mind. Like most computer systems they are designed for the data to be as
plastic as possible - large swathes of data can be amended with a single
update query. When audit data is stored separately, integrity checks must be
performed separately.

### Why RDBMs suck for security

* Most data stored as plaintext
* Data stored in a single large silo
* Not resistant to the Bribe-a-Sysadmin Attack

While schemes like field-level encryption exist, they foil indexing and impose a
performance overhead and are thus seldom used. If you can gain access to the
database, you can therefore usually dump all the medical records contained
therein for analysis and exploitation.

A single large silo of personal data forms a juicy target, making it more
worthwhile to attack the problem of cracking that target. No security is
perfect, the primary concern is to make cracking the target more costly than the
value that may be extracted. While black market prices for electronic medical
records have dropped to around $10 per record recently, this may merely reflect
the ease with which large quantities of records have been obtained. Even with
the falling price, medical data is more valuable than most classes of hacked
PII, to the degree that it becomes economically viable to compromise and
blackmail, or simply bribe, a sysadmin with access to a large silo of the data.

#### How the proposal fixes this

The proposed scheme will firstly allow data to be segregated in multiple
aggregate storage silos, reducing the value of any one silo and thus reducing
the likelyhood that it will be attacked. Secondly, the encryption-by-default
design of the data storage means that each patient record forms a silo of its
own that must be attacked to gain access. Thirdly, the distribution of encryption
keys to access the data is limited only to those individuals with a legitimate
reason for access, meaning that while the sysadmin may be induced to dump data
and pass it on, they cannot provide key access. The nature of the encryption
proposed makes it impractical to consider brute-force attacks for decryption.

