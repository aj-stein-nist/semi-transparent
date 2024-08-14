# Semi Transparent

A demonstration of a notional Transparency Service for semiconductor manufacturing.

## Background

### Why?

Some software developers makes it a priority to transparently publish information for downstream developers and consumers to understand it, but hardly any hardware manufacturers do the same. Industry has advanced software transparency for different, but related, use cases to publish such information, known as transparency services. From most most to least well-known, there are certificate transparency, binary transparency, software transparency, and firmware transparency services.[1] This project is prototype for a hardware transparency service, an argument in favor of deployment of hardware transparency services with metadata about semiconductor components. This technology is necessary to have hardware identifiers bound to metadata presented to them.

### What?

This prototype uses IETF's SCITT Architecture. "Architecture for Trustworthy and Transparent Digital Supply Chains"[2] is the specification that generalizes the Certificate Transparency architecture[3] for many digital use cases, including software and hardware. The same principles apply in the original architecture for certificates and the newer generalized architecture for all digital supply chains, including hardware.

A set of entities digitally sign statements (metadata) about artifacts (a hardware component), analyze the signature and statement for baseline requirements and quality determination, and register these statements in order.

Distributed ledger technology guarantees the integrity of individual statements and the order of their publication as a sequence on a transparency service. Digital signatures of the statements allow for cryptographic verification of the statement, in this case metadata about a hardware component, including a hash of its contents. On the transparency service, each record of this statement, with its own cryptographically verified hash, is combined with the hash of the previously published record's hash, countersigned, and published. This protocol is a kind of verifiable data structure, a Merkle tree. This Merkle tree construction allows efficient, performant verification of recent records (inclusion in the service) and the chain of all previous statement records (consistency of the service).

This architecture, and the use of distributed ledger technology, is similar to that of popular "permissionless" blockchain technologies (e.g. Bitcoin, Ethereum) because they are append-only data stores that guarantee properties of non-equivocation and replayability, but with key differences for efficiency and interoperability for parallel operation of heterogenous use cases.

In regards to this interoperability, unlike the transparency service architecture, blockchain systems are a superset of distributed ledger technologies that presume the deployment of one chain verified with many use cases persisted to this one chain in its many copies of the ledger. The design of this prototype, and others conformant to the SCITT architecture, presume multiple heterogenous ledgers with several redundant copies, not all use cases on unified ledger like the former. Use cases and customer-facing applications can and should utilize multiple transparency services, with distinct or overlapping data about raw materials, design software, build equipment, and resulting hardware components, to build futures for different stakeholders and customers. Despite a similar architecture, the deployment and application usage of SCITT-conformant transparency services are fundamentally different from that of popular blockchain systems. 

### Who?

For transparency services confirming to the SCITT Architecture, there are several entities that perform core functions in the protocol that correlate to the interactions of key stakeholders in a supply chain for hardware components.

#### Issuers

In a transparency service, the issuer is the entity that makes a statement about an artifact in a supply chain. The issuer of a statement is not always a person or organization who makes the artifact that is the subject of the statement.

For this hardware prototype, an issuer for some of the core information will come from a notional organization that makes the hardware component, namely the identifier(s) for a component, its physical dimensions, and basic operational characteristics. In addition, different issuer(s) will be from a downstream manufacturer describing the identifier of an integrated system and its compositional properties. Another distinct issuer will be an independent assessment organization that inspects an integrated hardware device, performs security analysis, and publishes a qualitative statement about the security design, implementation, and operation of that hardware by consumers. These three distinct organizations serve different logical roles in a supply chain, but all of them act as issuers registering statements in one or more hardware transparency services.

#### Transparency Service Operators

The SCITT Architecture with its underlying architecture, unlike blockchain systems, [presumes the deployment of multiple heterogenous services](#what), and each will require technical staff to design, implement, deploy, and maintain them. These technical staff are transparency service operators. They can work for a variety of organizations, not all of them traditional corporate structures. For this prototype, the manufacturers of an integrated hardware system will run their own transparency service with statements recording data about their products' individual hardware components, documenting provenance and traceability. Additionally, a separate transparency service can be run by a hardware consortium that employees technical staff and/or volunteers from consortium members to receive data about the hardware components and products they compose from each of the respective members. Records in the transparency service operated by the latter entity can reference records in the service operated by the former because they are retrievable by identifiers for the statement records themselves via APIs for supply chain use cases and applications. At a high level, this arrangement of transparency service operators mirrors that in the Certificate Transparency ecosystem, with traditional corporate entities, such as Cloudflare and Entrust, that want to transparently publish and monitor their certificates. Additionally, there are other transparency service operators, such as the [Let's Encrypt](https://letsencrypt.org/) service, which the non-profit organization and industry consortium [Internet Security Research Group](https://www.abetterinternet.org/) operate with funding support from its members.

#### Auditors

Auditors are the persons or organizations that design, implement, deploy, and maintain client software to check the consistency and integrity of the statement records in the log. Unlike [verifiers](#verifiers), they do not individually inspect and monitor the content of the individual statement records to make quantitative and/or qualitative determinations about individual statements.

In this prototype, auditors are hardware security and supply chain firms who will want to consume hardware manufacturer data from transparency services as a data source for their applications. It is vital for them to monitor different copies of one or more transparency services and coordinate with other auditors to consistently confirm non-equivocation, preventing issuers from using a transparency service to publish multiple valid, but conflicting, statements about the same statement. They also ensure non-equivocation and non-repudiation over the lifetime of the log for instances of the same transparency service.

#### Verifiers

Verifiers are persons or organizations that design, implement, deploy, and maintain client software that analyzes a chosen subset of statement records to make quantitative and qualitative determinations about their data. This role is different from that of [auditors](#auditors), who are monitoring the integrity and consistency of the sum of all statement records in the append-only log.

In this prototype, verifiers can be organizations from a variety of roles. Hardware security and supply chain analysis firms will likely serve as verifiers to support the use cases underlying their applications. The specifications do not require the same firms to perform both auditor and verifier roles simultaneously, even though the architecture documents their operation separately to increase interoperability and resiliency. Unlike auditors, different verifiers will build applications to meet specific use cases for particular subsets of hardware and analysis. The architecture and this role, especially relevant for hardware, is intended for verifiers to specialize in metrology applications target specific niches.

### How?

Below is a diagram that visualizes how issuers register statements, transparency services publish them after registration, issuers recirculate transparent statements, and how auditor and verifiers sustain healthy operation of the transparency service for downstream consumer applications over time.

![diagram](./flow_diagram.svg)

### When?

## References

1. Ben Laurie. 2014. Certificate transparency. Commun. ACM 57, 10 (October 2014), 40–46. https://doi.org/10.1145/2659897
2. Birkholz, Henk; Delignat-Lavaud, Antoine; Fournet, Cedric; Deshpande, Yogesh; Lasker, Steve  (2024-07-22). "An Architecture for Trustworthy and Transparent Digital Supply Chains (draft-ietf-scitt-architecture-08)". ietf.org. IETF. Retrieved 2023-05-28. https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/08/
3. Certificate Transparency Version 2.0. December 2021. doi:10.17487/RFC9162. RFC 9162. https://datatracker.ietf.org/doc/html/rfc9162
