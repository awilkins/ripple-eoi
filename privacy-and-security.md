# Privacy and Security

With data breaches almost a way of life now, it's clear that systems must be
designed to be secure by default. Medical records remain one of the most sought
after forms of personal data, with recent reductions in their price on black
markets only reflecting the relative ease with which systems appear to be
compromised.

The value of medical data makes a large silo a valuable target ; as with all
security measures, the key concern is to make compromise of the target more
expensive than its potential value. Aside from hacking, in some cases it may
make financial sense for an attacker to compromise and bribe or blackmail a 
sysadmin with access to the data (and this may have already happened, as it
would be very difficult to detect).

Current designs that place large amounts of plaintext data in a single large
silo, often protected only by filesystem-level encryption (or no encryption at
all), are rich targets vulnerable to compromise by both hackers and sysadmins.

## Intent

The proposal outlines a system that

* Is encrypted by default
  * Uses strong public-key encryption methods
  * Strictly limits key distribution to permitted parties
  * Is significantly less vulnerable to sysadmin attacks
* Permits smaller silos of data
  * Smaller targets are less valuable targets
  
## Methodology

### Encryption

* All records are [encrypted](encryption.md) with a symmetric key
* The symmetric keys used to encrypt records are stored encrypted
  * Symmetric key blocks are encrypted with the public key of only those with access rights
* Records are decrypted as they are rendered

Thus :

* Only holders of a corresponding private key can read records

In its most extreme expression, this system could produce a clinical record that
could only be read with the authorization of a single user - perhaps the patient.
This would have some deleterious operational constraints, but nevertheless, it
is important for the system to be *capable* of this level of operation in order
to provide a level of security that can be laxened to provide a more utilitarian
access profile.

This also provides a system capable of secure, offline data storage, thus
ensuring portability and permitting operation off the network, without excess
compromise to security.

Typically, private keys will be sequestered within hardware containers, e.g.
smart cards, thus rendering them robust against theft or copying.

### Silo Size

By avoiding the [relational database](relational-databases.md) and it's tendency
to create a large silo of homogenously stored records, smaller data silos may
be maintained. Smaller silos make smaller targets, making any potential data
breach less serious.