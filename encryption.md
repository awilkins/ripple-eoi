# Encryption

The proposal will develop an encryption scheme similar in nature to the well
established OpenPGP standard - symmetric "session" keys will be encrypted to the
public keys of permitted parties.

In this way records can in theory be encrypted for the access of parties without
the requirement for them to be present, although typical usage patterns will see
session keys encrypted to a variety of public keys including system keys, in
order that record distribution to new parties can be arranged without human
intervention.

The presence of a cryptographic smartcard in the hands of most of the users will
also permit cryptographic signatures to be used for non-repudiation purposes.