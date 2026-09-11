# cloud-itonami-lei-529900e95812sywmce44

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Avis Budget Group, Inc..**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Avis Budget Group, Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Avis Budget Group, Inc.
- **LEI (ISO 17442)**: [529900E95812SYWMCE44](https://search.gleif.org/#/record/529900E95812SYWMCE44) (GLEIF-verified)
- **Jurisdiction**: US-DE (state of incorporation, per GLEIF/Delaware Division of Corporations file 804185; headquarters are in Parsippany, US-NJ)
- **Website**: https://www.avisbudgetgroup.com
- **Ticker**: CAR (NASDAQ)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 9 verified registry facts with per-fact provenance. **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The identity table above used to be assertions with nothing in the repository
behind them. `facts.edn` now carries them as data, and every value in it was read
out of a public registry response whose URL and retrieval time sit next to the
value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO URLs were fetched and 9 facts recorded — the LEI record
(legal name as GLEIF spells it, **`AVIS BUDGET GROUP, INC.`**, upper case, `en`;
entity **ACTIVE**; two different addresses recorded separately — the legal
address `C/O CORPORATION SERVICE COMPANY, 251 LITTLE FALLS DRIVE, 19808,
WILMINGTON, US-DE, US`, a registered-agent address in Delaware, and the
headquarters `379 Interpace Parkway, 07054, Parsippany, US-NJ, US`; entity
creation date `1974-08-01` — this Delaware corporation is over three decades
older than the "Avis Budget Group" name, which it took in 2006; it is the
entity formerly named Cendant Corporation, though the LEI record itself names
no predecessor, so that history is context here, not a claim this file
verifies; no BIC — the empty list is a measured empty, where some corporates
do carry a treasury SWIFT code; OpenCorporates id `us_de/804185`, S&P Global
id `26268`), its ISIN mapping (**53** instrument identifiers, read from
`meta.pagination.total` of the cited page — at that volume the list is
deliberately *not* mirrored into `facts.edn`: instruments mature and are
issued, which would keep the check red for reasons that are not "the citation
broke"; walk the cited URL's 4 pages to enumerate them), its managing LOU and
LEI-issuer accreditation (**Bloomberg Finance L.P.**, LEI
`5493001KJTIIGC8Y1R12`, jurisdiction `US-DE`, marketing name **Bloomberg**,
accredited 2017-04-13), registration authority `RA000602` (**Division of
Corporations, Department of State** — `corp.delaware.gov`, serving Delaware
only — where the entity is file number `804185`), ISO 20275 legal form `XTIQ`
(**`Corporation`**, US-DE), and **both consolidation levels**: no parent at
either level, each level carried as a reporting-exception entity with category
`DIRECT_ACCOUNTING_CONSOLIDATION_PARENT` /
`ULTIMATE_ACCOUNTING_CONSOLIDATION_PARENT` and reason **`NATURAL_PERSONS`** —
GLEIF's code for an entity controlled by natural persons with no intermediate
legal entity meeting the definition of an accounting consolidating parent (a
different exception reason than the `NO_KNOWN_PERSON` carried by this family's
widely-held records, and recorded here as what the registry says, not as an
ownership analysis). Nine of the eleven URLs answered `200`; the
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the *exception* side of that pair for this entity, which the checker
treats as a fact rather than a failure.

Unlike its LAPSED siblings in this family, this registration is maintained:
**`ISSUED`**, `CONFORMING`, `FULLY_CORROBORATED`, first registered 2018-11-23,
last updated 2026-01-29, next renewal due 2027-02-28. The direct-children
count is still a measured **0** — for a holding company whose SEC filings
name a long list of subsidiaries (Avis Rent A Car System, Budget Rent A Car
System, Zipcar, and the rest). A maintained registration does not change the
shape of *LEI regulation*: a subsidiary appears in GLEIF's relationship graph
only if it holds an LEI and reports the relationship, which US rules mostly
do not compel. The 0 is a measured count of what GLEIF's graph holds, not a
census of subsidiaries.

One file in this repository *was* contradicted by the fetch. `blueprint.edn`
and the identity table above both said jurisdiction `US-NJ`, which is the
headquarters state, not the state of incorporation — four independent registry
points (the LEI record's `US-DE`, the registered-agent legal address in
Wilmington, registration authority `RA000602` with Delaware file `804185`,
and the ISO 20275 form's `US-DE` subdivision) agree the corporation is a
Delaware one. Both files were corrected in the same landing that added
`facts.edn`, and the jurisdiction line above now carries the distinction
explicitly.

The check has three exit codes, not two: `0` when every cited URL answered and
every recorded value still matches, `1` when a citation broke or a value
drifted (each difference is named, with the recorded and live values side by
side), and `3` when the check could not be performed at all — `facts.edn`
missing or empty, or GLEIF unreachable at the transport level — because a check
that could not run must not look like a check that ran and found nothing.
Before this landed, all three were shown against the live API: unmodified →
`0` (`OK all 9 recorded fact(s) still match the live sources`);
`:company/jurisdiction` edited `US-DE` → `FR` → `1`, naming `gleif-lei-record`
and `:company/jurisdiction` as `DRIFT`; the `gleif-direct-children-count`
entity deleted → `1`, naming it as `ADDED`; `facts.edn` absent → `3`
(`INCONCLUSIVE … Refusing to report a pass`). The file was restored
byte-identical afterwards (`shasum` equal).

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
