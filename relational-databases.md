# Relational Databases in EHRs

## Impedence mismatch with reality

Relational databases are not the best way to represent healthcare data.

Relational databases are designed for high-volume, low data size, homogenous,
transactional data.

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

## Poor integrity

Relational databases are not designed with any special controls for integrity
in mind. Like most computer systems they are designed for the data to be as
plastic as possible - large swathes of data can be amended with a single
update query. When audit data is stored separately, integrity checks must be
performed separately.

## Poor security

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

## How the proposal addresses this

Primarily the approach will be to avoid relational databases and instead use
[composite document storage](composite-data-storage.md).

The proposed scheme will firstly allow data to be segregated in multiple
aggregate storage silos, reducing the value of any one silo and thus reducing
the likelyhood that it will be attacked. Secondly, the encryption-by-default
design of the data storage means that each patient record forms a silo of its
own that must be attacked to gain access. Thirdly, the distribution of encryption
keys to access the data is limited only to those individuals with a legitimate
reason for access, meaning that while the sysadmin may be induced to dump data
and pass it on, they cannot provide key access. The nature of the encryption
proposed makes it impractical to consider brute-force attacks for decryption.

