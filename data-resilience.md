# Data Resilience

Resilience is important to medical data.

The proposed system of storing data will promote resilience by permitting
replication of the data without the ordinary deleterious effects :

* Increased distribution of the data increasing the attack surface
* Special replication mechanisms introducing additional costs

## Encrypted by default

Because the data is encrypted at rest, replicating the data does not greatly
increase the possible attack surface - attacks will still have to compromise
key storage (on dedicated key storage hardware) or key decryption in order to
compromise data.

## Replicated by default

Because the data storage method is designed to operate offline, replication of
the data is part of this mode of operation. This provides resilience as every
device used to access the data will contain a full or partial replication of
the data as part of normal operation.

## Federated replication

It is recommended that in addition to operational replication that federated
replication schemes are used in order to provide additional resilience.