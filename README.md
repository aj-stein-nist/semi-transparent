# Semi Transparent

A demonstration of a notional Transparency Service for semiconductor manufacturing.

## Background

### Why?

Some software developers makes it a priority to transparently publish information for downstream developers and consumers to understand it, but hardly any hardware manufacturers do the same. Industry has advanced software transparency for different, but related, use cases to publish such information, known as transparency services. From most most to least well-known, there are certificate transparency, binary transparency, software transparency, and firmware transparency services.[1] This project is prototype for a hardware transparency service, an argument in favor of deployment of hardware transparency services with metadata about semiconductor components. This technology is necessary to have hardware identifiers bound to metadata presented to them.

### What?

This prototype uses IETF's "Architecture for Trustworthy and Transparent Digital Supply Chains,"[2] a specification and emerging standard that generalizes the Certificate Transparency architecture[3] for many digital use cases, including software and hardware. The same principles apply, a set of entities digitally sign statements (metadata) about artifacts (a hardware component), analyze the signature and statement for baseline requirements and quality determination, and register these statements in order. These statements are preserved in order by distributed ledger technology.

### Who?

### How?

### When?

## References

1. Ben Laurie. 2014. Certificate transparency. Commun. ACM 57, 10 (October 2014), 40–46. https://doi.org/10.1145/2659897
2.  Birkholz, Henk; Delignat-Lavaud, Antoine; Fournet, Cedric; Deshpande, Yogesh; Lasker, Steve  (2024-07-22). "An Architecture for Trustworthy and Transparent Digital Supply Chains (draft-ietf-scitt-architecture-08)". ietf.org. IETF. Retrieved 2023-05-28. https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/08/
3. Certificate Transparency Version 2.0. December 2021. doi:10.17487/RFC9162. RFC 9162. https://datatracker.ietf.org/doc/html/rfc9162
