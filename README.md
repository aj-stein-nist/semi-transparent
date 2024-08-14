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

### How?

### When?

## References

1. Ben Laurie. 2014. Certificate transparency. Commun. ACM 57, 10 (October 2014), 40–46. https://doi.org/10.1145/2659897
2. Birkholz, Henk; Delignat-Lavaud, Antoine; Fournet, Cedric; Deshpande, Yogesh; Lasker, Steve  (2024-07-22). "An Architecture for Trustworthy and Transparent Digital Supply Chains (draft-ietf-scitt-architecture-08)". ietf.org. IETF. Retrieved 2023-05-28. https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/08/
3. Certificate Transparency Version 2.0. December 2021. doi:10.17487/RFC9162. RFC 9162. https://datatracker.ietf.org/doc/html/rfc9162
