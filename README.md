# Overview

The proposal addresses platform considerations essential to the enterprise of
creating and maintaining medical records. These are concerns I have seen stated
over and over again in RFP requirements at multiple Healthcare IT companies.
They are seldom if ever addressed satisfactorily, in most implementations I have
been party to, most effort is concentrated on putting a functioning system in
front of users and these concerns remain secondary.

The proposal is to build a model EHR system based on a design that places these
considerations as integral to the system rather than as bolted-on afterthoughts.

## What the proposal addresses

* [Audit](audit.md)
* [Data integrity](data-integrity.md)
  * And [data resilience](data-resilience.md)
* [Privacy and security](privacy-and-security.md)
* [Offline working](offline-working.md)
* Simplicity of system creation by 
  * [Avoiding relational databases](relational-databases.md)
  * [Creating a simple and ubiquitous platform](ubiquitous-platform.md)

## How the proposal addresses the concerns

* [Content-addressible storage] enabling.. 
  * [Composite document storage]()
  * [Chained historic data storage]() aka "Version Control"
* [Public key encryption]()
* [Blockchain Notarization]()
* [NodeJS]() and [Electron]() for application and user interface

---

[About the author](who-am-i.md)