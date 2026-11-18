# DOSE-10060

DRUG OBJECT SIGNED ELECTRONIC · CANONICAL TEXT V1.3 · dose-10060.org

DOSE-10060 defines the signed record of a prescription medicine, and the evidence behind it. Each record is a card: one medicine in one market, complete and signed, at its own permanent address. A card is found by any one of three codes, carries the source and read date of every value, and shows the date it was last checked against the regulator. Each fetch of a card is evidenced separately by a signed receipt. DOSE-10060 carries no dosing advice, no clinical guidance and no recommendation.

## The contract

DOSE-10060 defines the signed, sourced and dated record of a prescription medicine that an artificial-intelligence (AI) agent can inspect and rely on. Its purpose is to preserve the relationship between a medicine, the facts asserted about it, the sources from which those facts were read, the time of that reading, and the node that publishes them.

Drug Object Signed Electronic is the expansion of DOSE. The object is the medicine record. The name refers to the unit every medicine is supplied in. It does not refer to how much a patient should take, and no card states that.

Prescription medicine means what each jurisdiction's law calls it: in the United States, a prescription drug; in the European Union, a medicinal product subject to medical prescription; in the United Kingdom and Ireland, a prescription-only medicine. This version covers human medicines that hold a marketing authorisation in the jurisdiction of the record.

Every card published under DOSE-10060 makes the same five promises, wherever an agent encounters it:

Identity. The card names one medicine in one market: its name as the regulator publishes it, its substance, strength, form and pack size. A card is a pack. Where a market publishes no pack level, or an authorisation has no pack on record, the card is the authorisation, and says so. A shared ingredient does not make two cards the same product, and does not make one usable in place of the other.

Provenance. Every value on a card carries the regulator's page it was read from and the date it was read. Nothing is answered beside a card: a value that is served is inside the signed card. A reader can distinguish the node's assertion from the regulator's decision.

Time. A card keeps three dates apart: the date a status took effect, as the regulator publishes it; the date each value was read; and the stamp, the date the card was last checked against the regulator. The stamp is a date, not a countdown. Nothing expires. A recent reading of an old decision is not a recent fact.

Jurisdiction. The card states the market it was read under. It carries that jurisdiction's own term for the status of the medicine, as published, and never flattens it to one global label. An authorisation in one market says nothing about another.

Signature. The producing node signs the whole card under its record key: one signature over every part of the card. The stamp is not inside the signed card; it is signed on its own and attached when the card is served. The card remains verifiable when detached from the website that first presented it. The regulator is the cited source of a value and never its signer. No card is issued, endorsed or approved by a regulator.

Unknown is shown as unknown. A register that holds no entry is not a prohibition. A missing value is never filled by inference. Where two registers of one regulator disagree on a status, the card says so and serves no term.

History is preserved. A card is a versioned assertion, and a signed version is never rewritten. Only a real change in a served value makes a new signed version, which names the version it supersedes. A new edition of a register, a new file date or the same list in a new order is not a change. The card served is the current version.

A medicine that is no longer in the regulator's file reads as withdrawn on its card, with the date it was first found gone, the page that was read and the regulator's last published status. Withdrawn states that fact and no other.

## What a card carries

Every market uses the same shape, the same names and the same order. No market has its own layout.

| Part of the card | What it holds |
|---|---|
| Address | The card's own permanent address. It never changes. |
| Identity | Name as the regulator publishes it, substance, strength, form, pack size and market. |
| Codes | Pack barcode (Global Trade Item Number, GTIN), national pack code and authorisation number, whichever of the three the regulator publishes. |
| Standing | Status with the regulator, in the regulator's own term, and the date it took effect. A withdrawn medicine says withdrawn, with the date. |
| Holder | The authorisation holder as the regulator publishes it. |
| Source | For every value on the card: the regulator's page it was read from and the date it was read. |
| Standard | The version of DOSE-10060 the card follows. |
| Signature | One signature covering the whole card. |
| Stamp | The date of the last check. It is attached when the card is served and is not inside the signed card. |

## How a card is found

There is one way to get a card: the fetch. It takes a card's address or any one of the three codes. The caller does not say which kind of code it holds. Spaces at the ends are removed, case is ignored and a barcode is padded to 14 digits. The regulator's own punctuation is kept. After that the match is exact, and nothing else is inferred.

One card is returned as the signed card itself, with its stamp, and nothing around it. Where several cards share the code, all of them are returned as a plain list of signed cards. Where there is none, the answer is empty. The same ask returns the same card from every interface a node offers. There is no bulk download: an agent takes the card it needs when it needs it, and the sitemaps list every card.

## The stamp and the read

A node reads every market it holds once a day. Each full read of a market produces one small signed stamp for that market: the date, and the point in the market's list of changes that it covers. Every card of the market shows that date. Cards are not signed again for a stamp.

A read that does not cover a market in full stamps nothing and withdraws nothing, and the market keeps its previous stamp. A read that would withdraw more than one in a hundred of a market's records writes nothing and stops.

## Changes

Each real change to a card is published as an entry on the market's list of changes, which an agent can follow from any date. The entries of a market form a hash chain, signed at its head by a checkpoint under the record key. A read that found nothing changed is recorded on the chain and left out of the list.

A reissue is a card signed again in a new shape from the values already held. It is marked reissued, apart from real changes. A wrong entry is never removed: a later entry names it and corrects it.

## Who may read

The card is public. Anyone may read it and anyone may verify it. A card never carries patient data, so no reader receives any. A successful read does not authorise a downstream clinical or supply action.

## What the standard does not do

It gives no dosing advice and no clinical guidance. A card has no part for either. A node hands over a card; it does not interpret a question.

It does not authorise prescribing, dispensing, the dispensing of one product in place of another, import or sale. A card is an input to those decisions and never the decision.

It does not certify a medicine, a maker or a supplier.

It does not interpret legislation or decide whether a duty is met.

It does not recommend. A card is an information source, not advice.

It does not carry patient data, prices or rankings.

It does not carry products without a marketing authorisation in the jurisdiction of the record. Research-use, investigational and compounded products are outside it.

It does not verify an individual pack. Serial-level and lot-level answers come from the authorisation holder and the official verification systems.

It does not establish that a source is true. Verification establishes integrity and attribution; the accuracy of the source and of the node's reading of it remain separately assessable.

Artificial intelligence makes mistakes. Every value links the page it was read on. Read the regulator.

## Who signs

Two kinds of object are signed, by different keys, and no key signs the other's object.

The card is signed by the producing node under its record key. The same key signs each market's stamp and the checkpoint of each market's list of changes. The public keys are published at the node's /.well-known/jwks.json, with historical keys kept available for historical verification.

The receipt of a fetch is signed by the receipt issuer under a separate receipt key. An issuer may run more than one receipt chain, each under its own key; every receipt names its chain, and every key is on the keyring. The receipt names the card that was read, by its record and version, and when. It carries the hash of the answer exactly as served, and a hash of what was asked, never the text. A receipt is written alongside the answer, never in front of it: the answer carries the receipt's identifier, and the caller reads the receipt by it. The issuer publishes exactly how each hash is made.

Where one record key is shared across markets, the market is named inside the signed card. Subject identity lives in the card's own codes. Server identity lives in the agent card and the key identifier on the server's key set.

## The arrow

medicine → card (DOSE-10060, the node) → market (the jurisdiction instance) → receipt (under every fetch)

An agent begins with a code. The node hands over the card, which names its market and the regulator. The fetch is receipted. The card always names the producing node's key, so a consumer verifies the node and never treats the registry as the content issuer.

## The jurisdiction family

DOSE-10060 supplies the contract for content. Each jurisdiction instance binds that contract to one market and is named country first: US-DOSE-10060, EU-DOSE-10060, UK-DOSE-10060. An instance states its regulator, the registers it reads and the code systems of that market.

The European Union instance covers centrally authorised medicines. National instances cover national authorisations. A card always names the authority that made the decision, and a European card is never assumed to be a central one.

Each member has a member page that states the jurisdiction binding, and a live node that serves its cards. A member page never claims cards that are not being served. Instance and server addresses are drawn from the registry, never constructed from a country code. Membership confers the contract; it does not confer truth or regulatory authority.

## Conformance

An implementation that meets these points is listed on the keyring as an issuer.

Card. Every value is sourced and dated. Every card names the version of this standard it follows and passes its published schema. Codes stay as the regulator publishes them. Matching is exact. Unknown is returned as unknown. Status and holder are inside the signed card.

Stamp. A stamp is issued only by a full read of a market. A source that does not answer leaves the previous stamp in place, never a new date.

Receipt. Every receipt matches the published profile. The hash recomputes and the signature verifies under the keyring. The chain links. Writing requires the issuer credential; checking requires none.

Changes. Every entry matches the published schema. The chain links to a signed checkpoint. A reissue is marked.

## Publication discipline

One approved source. The human page and every machine file under it are generated from the same approved text and the same live record.

Honest surfaces. An agent card describes an endpoint that exists and the tools it serves.

No counts in prose. Coverage is a readout of the live record, rendered by generated tiles.

Versions kept apart. The standard version, the schema version and the deployment version are distinguishable. A new deployment is not a new standard.

Record before page. A page exists only after its card does.

## Versions

Version 1.3 is in force from 18 November 2026. It adds the stamp and the reissue mark, and it carries the receipt profile and the schema for changes as they run. It no longer promises the record as it stood on a past date, and it has no typed refusal: a fetch returns a card, a list of cards or the empty answer.

Version 1.3 accepts the history signed under earlier versions. A version signed under DOSE-10060 1.0, 1.1 or 1.2 stays as it was signed and remains valid under the schema it was signed for. Version 1.2 and its schema stay published, superseded.

## Machine surfaces

/llms.txt · /.well-known/agent-card.json · /.well-known/jwks.json · /.well-known/security.txt · /index.md · /dose.json · /nodes.json · /markets.json

Standard held by Dosidal AI Corp. · Open standard, MIT licence. Artificial intelligence makes mistakes; read the regulator. © 2027 Dosidal AI Corp.
