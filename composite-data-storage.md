# Composite Document Storage

## Content-Addressible IDs

### Hash Functions

### Why use content-addressible IDs?

* Uniqueness
* Comparison
* Data Integrity
* Redundancy Reduction

#### Uniqueness

CAIDs are created by running the content data through a hash function. Because of the nature of hash functions, this means that the identifier is almost certain to be unique for that particular data (even more likely if the data is not nonsense).

#### Comparison

Hash functions are deterministic, which means that given the same inputs, they will always produce the same outputs. This means that two records can be compared by comparing their hashes - even if the records are very large, you can be very sure that the data is identical.

*Illustrate this with two hashes of very slightly different content*

#### Data Integrity

Because even a small change in the input to a hash function produces a large change in it's output, you can be sure that a particular piece of data has not been tampered with or corrupted if it matches it's identifier.

You can combine this with a [version controlled data model] and be assured that not only is a particular record intact, but that all records preceding it are as well.

#### Redundancy Reduction

By employing a [Composite] pattern for your records, and using a CAID to identify components, you can reduce redundancy. Many record components will be identical, and thus have identical CAID values, reducing the entire record to the size of your chosen CAID form, regardless of it's actual size. Many components will repeatedly occur from day 1, many more will naturally repeat over time, e.g.

* Blood pressure measurements
* "Normal range" values on test results
* Fully specified clinician identifiers (including role etc)
* Views on test results
** e.g. clinicians copying results into ward round notes

*Illustrate this with a picture of the same things with the same IDs referred to from different parts of the same patient record and maybe different parts of different patient records*