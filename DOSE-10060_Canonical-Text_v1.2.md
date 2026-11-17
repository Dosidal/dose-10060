# DOSE-10060

DRUG OBJECT SIGNED ELECTRONIC · CANONICAL TEXT V1.2 · dose-10060.org

DOSE-10060 defines the signed record of a prescription medicine, and the evidence behind it. Each producing node identifies the medicine, binds its record to the jurisdiction it was read under, preserves the source and read date of every field, and signs its own content. The jurisdiction instances of DOSE-10060 implement this contract market by market. A cleared read is evidenced separately by an RCO-10060 (Record of Cleared Orders) receipt whose answer hash binds it to the signed record supplied. Together they let an agent identify the medicine, inspect the provenance of what is said about it, verify the publisher and keep evidence of the read. DOSE-10060 carries no dosing advice, no clinical guidance and no recommendation.

## The contract

DOSE-10060 defines the signed, sourced and dated record of a prescription medicine that an artificial-intelligence (AI) agent can inspect and rely on. Its purpose is to preserve the relationship between a medicine, the facts asserted about it, the sources from which those facts were read, the time of that reading, and the node that publishes them.

Drug Object Signed Electronic is the expansion of DOSE. The object is the medicine record and its related, explicitly typed records. The name refers to the unit every medicine is supplied in. It does not refer to how much a patient should take, and no record states that.

Prescription medicine means what each jurisdiction's law calls it: in the United States, a prescription drug; in the European Union, a medicinal product subject to medical prescription; in the United Kingdom and Ireland, a prescription-only medicine. This version covers human medicines that hold a marketing authorisation in the jurisdiction of the record.

Every record published under DOSE-10060 makes the same five promises, wherever an agent encounters it:

Identity. The record names its subject at one of three levels and says which. The substance is the active molecule, with its Anatomical Therapeutic Chemical (ATC) classification code where one exists. The presentation is the brand, strength, form, route, device and pack. The market authorisation is that presentation as authorised in one jurisdiction, named by the regulator's own identifier and by the pack's product code where one exists. Where a pack product code exists it is the anchor identifier of the presentation: a name resolves to candidates, a code resolves to one record within its market. A substance, a presentation and an authorisation are related subjects, and no one of them is a name for another. A shared ingredient does not make two records the same product, and does not make one usable in place of the other.

Provenance. Every substantive field carries the page it was read from and the date it was read. A reader can distinguish the node's assertion from the regulator's decision.

Time. The record distinguishes the date the source was published, the date a status took effect, and the time the node produced the record. Every field is kept as a timeline, so a record answers for any past date as well as for today, and each change is published as an event an agent can follow. A recent reading of an old decision is not a recent fact.

Jurisdiction. The record states the market it was read under. It carries that jurisdiction's own terms for authorisation status and prescription class, as published, and never flattens them to one global label. An authorisation in one market says nothing about another.

Signature. The producing node signs its own record under its record key, and the record remains verifiable when detached from the website that first presented it. The regulator is the cited source of a field and never its signer. No record is issued, endorsed or approved by a regulator.

Absent, unavailable, not applicable and conflicting information have distinguishable representations. A register that holds no entry is not a prohibition. A missing value is never filled by inference without the inference and its basis being labelled. A resolved conflict between sources carries the selection rule that resolved it.

History is preserved. A record is a versioned assertion, and a signed version is never rewritten. A correction creates a new published version that names the version it supersedes. A re-read that finds no change is recorded as an event beside the version. Earlier versions remain available to anyone holding a receipt that references them, so that an earlier answer hash is never read as the hash of today's content.

## What a record carries

Each of these is a typed field with its own source and read date.

| Field | What it states |
|---|---|
| Pack product code | The code printed on the pack, bound to its presentation |
| Identity | Substance, presentation, authorisation holder |
| Authorisation status | The regulator's own status term and the date it took effect |
| Prescription class | The jurisdiction's own class and sub-class |
| Controlled status | The jurisdiction's own schedule or control class, where one applies |
| Label reference | The approved label, by reference to the regulator's copy |
| Storage and handling | Temperature range, freezing, light, time allowed outside refrigeration, in-use life |
| Authorised channel | The parties the authorisation holder names as authorised to supply |
| Recalls and notices | Regulator recalls and enforcement notices, by reference |

## How a record is found

A node answers a lookup. The agent gives a code, or the medicine's name or substance as the regulator publishes it, with any further named fields it holds. Matching is exact: a field matches after normalising case, accents, spacing, punctuation and unit notation, and in no other way. Where more than one record fits, the agent receives the candidates and the fields in which they differ, never a guess. Where none fits, the answer is that the record is not available.

## Who may read

The record is public. Anyone may read it and anyone may verify it. A record never carries patient data, so no reader receives any. A successful read does not authorise a downstream clinical or supply action.

## What the standard does not do

It gives no dosing advice and no clinical guidance. A record has no field for either, and a node answers a lookup, not a question.

It does not authorise prescribing, dispensing, the dispensing of one product in place of another, import or sale. A record is an input to those decisions and never the decision.

It does not certify a medicine, a maker or a supplier.

It does not interpret legislation or decide whether a duty is met.

It does not recommend. A record is an information source, not advice.

It does not carry patient data, prices or rankings.

It does not carry products without a marketing authorisation in the jurisdiction of the record. Research-use, investigational and compounded products are outside it.

It does not verify an individual pack. Serial-level and lot-level answers come from the authorisation holder and the official verification systems. The record carries recall and notice references.

It does not establish that a source is true. Verification establishes integrity and attribution; the accuracy of the source and of the node's reading of it remain separately assessable.

It does not evidence a read. That is the work of RCO-10060.

Artificial intelligence makes mistakes. Every field links the page it was read on. Read the regulator.

## Who signs

Two objects are signed, by different keys, and no key signs the other's object.

The record is signed by the producing node under its record key. The public keys are published at the node's /.well-known/jwks.json, with historical keys kept available for historical verification.

The receipt of a cleared read is signed by the receipt issuer under a separate receipt key. That signature belongs to RCO-10060. An issuer may run more than one receipt chain, each under its own key; every receipt names its chain, and every key is on the keyring. The receipt carries the hash of the signed record the agent received, and pins the version of this standard and of the jurisdiction instance it was read under. That hash is the only link between the two objects, and the issuer publishes exactly how it is made.

An authorisation holder that has claimed its seat signs its own assertions, such as its authorised channel, under its own key listed on the keyring. A holder's signature covers what the holder asserts and nothing else.

Where one record key is shared across nodes, node attribution is carried inside the signed payload and checked against the published list of authorised publishing nodes. Subject identity lives in the record's own identifiers. Server identity lives in the agent card and the key identifier on the server's key set.

## The arrow

medicine → record (DOSE-10060, the node) → market (the jurisdiction instance) → receipt (RCO-10060, under every read)

An agent begins with a medicine identifier and a jurisdiction. The registry names the responsible instance and its exact address. The instance page states the jurisdiction binding; the live node supplies the record. The read is receipted under RCO-10060. The response always names the producing node, so a consumer verifies the node and never treats the registry as the content issuer.

## The jurisdiction family

DOSE-10060 supplies the contract for content. Each jurisdiction instance binds that contract to one market and is named country first: US-DOSE-10060, EU-DOSE-10060, UK-DOSE-10060. An instance states its regulator, the registers it reads, the identifier systems it accepts, the status terms and prescription classes of that market, and its keyring entry.

The European Union instance covers centrally authorised medicines. National instances cover national authorisations. A record always names the authority that made the decision, and a European record is never assumed to be a central one.

Each member has a member page that states the jurisdiction binding, and a live node that serves its records. A member page never claims records that are not being served. Until the member page exists, the address forwards to the standard's home. Instance and server addresses are drawn from the registry, never constructed from a country code. Membership confers the contract; it does not confer truth or regulatory authority.

## Conformance

An implementation that passes the conformance suite is listed on the keyring as an issuer.

Record. Every field is sourced and dated. Identifiers stay in their own namespaces. Matching is exact. Unknown is returned as unknown. A strength, form or pack that disagrees never binds. Ambiguity returns candidates.

Policy. Every field carries its read date. A source that does not answer gives unknown, never a cached answer presented as new. An authorisation in one market never populates another.

Receipt. All required fields and both pinned versions are present. The hash recomputes and the signature verifies under the keyring. The chain links. Writing requires the issuer credential; verifying requires none.

## Publication discipline

One approved source. The human page and every machine file under it are generated from the same approved text and the same live record.

Honest surfaces. An agent card describes an endpoint that exists and the tools it serves, with an accurate account of what needs a key.

No counts in prose. Coverage is a readout of the live record, rendered by generated tiles.

Versions kept apart. The standard version, the instance version, the schema version and the deployment version are distinguishable. A new deployment is not a new standard.

Record before page. A page exists only after its record does.

## Machine surfaces

/llms.txt · /.well-known/agent-card.json · /.well-known/jwks.json · /.well-known/security.txt · /index.md · /dose.json · /nodes.json

Standard held by Dosidal AI Corp. · Open standard, MIT licence. RCO is the Record of Cleared Orders, cited by reference. Artificial intelligence makes mistakes; read the regulator. © 2027 Dosidal AI Corp.
