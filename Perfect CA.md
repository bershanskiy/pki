# Perfect Certificate Authority

## Problem

### Certificate authorities do not sell security, they sell a _subscription to the idea_ of security

1. CAs are reactive, not proactive
   CAs migrate to newer primitives/algorithms/standards only when they are forced to by external circumstances.
2. CAs are money-driven enterprises
   Anything that does not result in immediate monetary gains gets thrown out.
3. There is no mandatory CT for any types of certificates aside from CT for TLS certificates.
   Google literally forced TLS CT by sheer force of will (and market share).

### System is rigid

1. It's almost impossible to introduce new trust roots since old systems will not recognize them.
2. It's almost impossible to initiate formal process of trust revocation, even when everyone would like to stop working with a particular CA.
3. System administrators do not care about security, they care about lack of warnings.

### Solution

1. Equivalent of Certificate Transparency, but throughout the issuance process
   - either of these two happens:
     - CAs themselves carry a separate CT-like log (append-only Merkle tree) of all verifiable data observed during issuance process: CAA records (hopefully DNSSEC-signed), challenge responses, etc.
     - if CAs do not carry such a log, then some external parties can do this instead. Specifically, external parties observe regular CT logs and when they see a new pre-certificate, they try to obtain the same data that CA collects during certificate issuance
   - (some other) external parties validate these logs on a regular basis (the same way they validate regular CT logs)
   - in case of an issuance error, CAs and external parties have a complete record they can audit and spot the mistakes

2. CAs already can be run by organizations which have an alterior motive than direct revenue from certificate sales. Can these CAs can make public commitments to audit each other's logs?
   - Hosting providers already run CAs for themselves (Cloudflare, Amazon, etc.)
   - Universities can run CAs for public recognition and clout

3. Alternative TLS certificate paths
   - Migration to newer algorithms, different CAs and different roots belonging to the same CAs
   - Disjoint sets of roots (?!)

### Challenges
1. Complete indifference on CA's part
   - I'm effectively asking CAs to take on more responsibiity (in a manner which guarantees any mistake they make will be spotted) without providing any more revenue. Solution: rorrowing from Extended Validation cetrificates idea, CAs could upsell existing consumers. Needs a catchy name like "Assured Validation" and a "new" green padlock. :)
2. Lack of strong interest from Relying Parties
   - However, if Google does it, the rest will follow.
   - Apparently, Firefox does not validate even regular CT yet... Can I create browser extension for Firefox which will check regular CT logs and CAA (yes, spec permits RP to check CAA during validation). Then I can simply add these "extra" logs as well to promote them.

### TODO
Remove all ":)"