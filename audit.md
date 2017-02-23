# Audit

Audit is a common requirement that I see expressed in virtually every RFP for
healthcare system that I encounter. Typically several concerns are lumped
together under this noun.

* Audit of the records being written
* Integrity of the records after being written
* Audit of the records being read

## Audit like a programmer

The proposal is to provide a data storage structure that inherently provides a
transactional, historic view of all stored data with no additional effort
required on the part of the programmer or designer of the data.

Inspired by the distributed version control systems that programmers are
accustomed to, the system shall provide a *full* history of all changes made to the
patient record, able to construct with ease an exact replica of the available
data at any point in time, or indeed, within a distributed system, space.

In addition, the system should define similar auditability for the software
used to view and construct the data, in order to provide auditors with a view of
the full stack in situ at the time of the creation of records, enabling a fair
and complete assessment of e.g. medico-legal cases.

### Easy to query

Querying the data boils down to a 2-step process

* Identifying the revision of the data you wish to examine
* Performing normal everyday operations on that data
* No need to account for audit metadata in normal operation

### Reduced overhead

This system preserves every revision of the data but only imposes a small
overhead on each revision. Data is not copied for the purposes of auditing.
All revisions of the data are preserved as-is without abridgement.

Data is not copied during normal write operations.

## Audit in most systems a second thought

Typical design and implementation cycles are aware of the requirement for audit
but concentrate on providing user-visible features in order to keep clients
happy. Audit features are often "bolted on" after the fact, and are typically
not a first-class feature of the system, compromised in performance, ease of use,
or implementation complexity.

Partiularly in relational-database systems, 
audit requires design compromises.

* Store audit logs separately
* Design primary data to be auditable

### Separate audit data

This design writes audit data to separate structures.

* A copy of the existing structures (perhaps with extra audit fields)
* A general log of data changes

The disadvantages of this approach include

* Hard to query - often data is unstructured
* Data is often transformed in a way which abridges it and removes data
* Data is copied during normal write operations

### "Auditable" data

This often takes the form of adding timestamps and other audit fields to
every row in the database.

This imposes additional overheads on normal operations of the system ;

* Reduced ability to impose referential integrity
* Increased difficulty of writing basic queries
* Increased disk consumption
* Increased processor load

