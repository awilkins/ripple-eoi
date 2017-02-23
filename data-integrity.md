# Data Integrity

The integrity of patient records is paramount.

Digital records make it easier than ever to amend or destroy records.

## Version controlled history

It is proposed to use a data storage scheme inspired by distributed version
control systems, that includes an inherent tamper-resistant history mechanism
that incorporates the digest of the previous revision into the next. Tampering
with such a data store is immediately obvious on verification.

## Distributed Notarization

The proposal includes the investigation of methods of digital notarization, 
principally blockchain technologies, that will permit EHR transactions to be
signed and dated, and their existence preserved and logged in a distributed
trusted system, thus protecting against the casual amendment or destruction of
records.

## Replication

The inherent replication capability of the proposed system improves data
integrity by creating replicated copies of the data. Because data is encrypted
by default, some replication targets should even find it impossible to read the
data in order to tamper with it.