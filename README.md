# emr-claims-primary-sources

**Primary-source archive for EMR (electronic medical record) / claims
(レセプト) identifier specifications**, used to keep implementations such as
[`kotoba-lang/insurance`](https://github.com/kotoba-lang/insurance) (Japan
health-insurer number 保険者番号 / medical-institution code 医療機関コード
check-digit and structure) honest against the government notifications that
actually define them, instead of guessing at digit widths, category codes or
check-digit algorithms from secondary sources (blog posts, Wikipedia, etc.).

This is a [DataLad](https://www.datalad.org/) dataset (`text2git`
configuration: small text files go straight into git, large binaries — here,
PDFs — go through git-annex). The actual PDF bytes are stored in a
[Backblaze B2](https://www.backblaze.com/cloud-storage) (S3-compatible)
special remote named `b2`, sharing the same bucket as the
`gftdcojp/mangaka-data` dataset with `fileprefix=emr-claims-primary-sources/`
to keep the two datasets' objects apart. Git itself only holds annex-key
pointers, so a plain `git clone` of this repo is small; `datalad get
jp-mhlw/*.pdf` (or `west annex-get`, from the west-managed superproject)
fetches the real file content from B2.

Scope: **Japan (JP), EU (`eu-ehds/`, `eu-ehic/`), and a first US directory
(`us-naic/`)**. Layout convention: one directory per jurisdiction/issuer
(`jp-mhlw/`, `eu-ehds/`, `eu-ehic/`, `us-naic/`, and in the future
`us-cms/` etc., named for the issuing authority) — **not** one directory
per identifier, since not every US claims identifier has an issuing
authority to archive against (see `us-naic/`'s own note on why Payer ID has
no corresponding directory here).

**`eu-ehds/` and `eu-ehic/` are curated verbatim-excerpt archives, not
full-text/PDF mirrors** like `jp-mhlw/`: EUR-Lex (the EU's official
legislation portal) blocks automated `curl`/headless fetches behind an AWS
WAF JS challenge, so their content was retrieved by navigating EUR-Lex in a
real (non-automated) browser session and copying the rendered article text
verbatim, rather than downloading an official PDF/HTML file whose bytes
could be hashed the way the `jp-mhlw/` PDFs are. Each `eu-ehds/*.md` /
`eu-ehic/*.md` file documents this retrieval method, the CELEX identifier,
and exactly which articles/annexes were and were not captured -- see
`eu-ehds/ehds-article3-excerpt.md`'s and `eu-ehic/s2-decision-2009-annex1-excerpt.md`'s
own provenance sections for the specifics of what "curated excerpt" means
here.

## Contents

### `jp-mhlw/mhlw-001275316-iryokikan-code-2024.pdf`

- **Title**: 厚生労働省「診療報酬請求書等の記載要領等について」等の一部改正について
- **Issuer**: 厚生労働省 (Ministry of Health, Labour and Welfare, Japan)
- **Date**: 2024-07-12
- **Source URL**: https://www.mhlw.go.jp/content/12400000/001275316.pdf
- **Retrieved**: 2026-07-08
- **Size**: 4,821,029 bytes
- **SHA-256**: `398b5d8e808ade0a4a238191400b35d3236a263b0fbb568cc8b575c4abc002c6`
- **Relevant section**: 別添２「保険者番号、公費負担者番号、公費負担医療の受給者
  番号並びに医療機関コード及び薬局コード設定要領」— 第１ (保険者番号) and
  第４ (医療機関コード及び薬局コード), including the 検証番号 (check digit)
  algorithm, the 点数表番号 category codes (医科１／歯科３／薬局４), the
  医療機関(薬局)番号 numeric ranges per category, and 別表２ (都道府県番号,
  01-47 primary + 51-97 alternate codes).
- **Implementation consumer**: `kotoba-lang/insurance`,
  `src/kotoba/insurance/jp.cljc` — this PDF is the primary source backing
  `iryokikan-bangou-check-digit`, `tensuhyou-bangou-category`,
  `valid-iryokikan-kikan-bangou-range?` and the extended 都道府県番号 table.

### `jp-mhlw/mhlw-tp0305-1az_0004-2008.pdf`

- **Title**: 厚生労働省 2008年通知（保険者番号等の設定要領、旧版）
- **Issuer**: 厚生労働省 (Ministry of Health, Labour and Welfare, Japan)
- **Date**: 2008 (published under `/topics/2008/03/`)
- **Source URL**: https://www.mhlw.go.jp/topics/2008/03/dl/tp0305-1az_0004.pdf
- **Retrieved**: 2026-07-08 (originally referenced in an earlier cycle when
  implementing `hokensha-bangou-check-digit`)
- **Size**: 508,602 bytes
- **SHA-256**: `b42890b67fcfef87eda0e89a400beaaf2b282c2e51afa3b76551abf7c512941a`
- **Relevant section**: same 保険者番号 worked example (法別番号=06,
  都道府県番号=13, 保険者別番号=048 → 検証番号=8) as the 2024 notification's
  第１, independently confirming the check-digit algorithm and worked example
  used by `kotoba-lang/insurance`'s `hokensha-bangou-check-digit` are stable
  across the 2008 → 2024 notification revisions.
- **Implementation consumer**: `kotoba-lang/insurance`,
  `src/kotoba/insurance/jp.cljc` (`hokensha-bangou-check-digit`,
  `parse-hokensha-bangou`).

### `eu-ehds/ehds-article3-excerpt.md`

- **Title**: Regulation (EU) 2025/327 of the European Parliament and of the
  Council of 11 February 2025 on the European Health Data Space and
  amending Directive 2011/24/EU and Regulation (EU) 2024/2847 (EHDS)
- **Issuer**: European Parliament and Council of the European Union
- **CELEX**: 32025R0327
- **Official Journal**: L series, 2025/327, published 2025-03-05, entered
  into force 2025-03-26
- **Canonical URL**:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32025R0327
- **Retrieved**: 2026-07-08, via a real Chrome browser session (see the
  format note above -- EUR-Lex WAF-blocks automated fetches). This is a
  plain-text `.md` file (small, goes straight into git via `text2git`, not
  through the `b2` annex remote like the `jp-mhlw/*.pdf` binaries).
- **Content captured verbatim**: Article 3 ("Right of natural persons to
  access their personal electronic health data"), paragraphs 1-3 in full
  (paragraph 3 is truncated where the source text itself continues past
  the captured passage -- marked inline as `[text continues, not captured
  further]`).
- **Content confirmed to exist but NOT yet captured**: Article 4
  (electronic health data access services) is cross-referenced by Article 3
  but its own operative text has not been retrieved. See the excerpt
  file's own "Cross-references confirmed" section. (Article 14 and Article
  15 -- also cross-referenced by Article 3 -- are now captured separately;
  see `eu-ehds/ehds-article14-15-excerpt.md` below.)
- **Implementation consumer**: `kotoba-lang/com-hl7-fhir`,
  `src/hl7_fhir/validation.cljc` / `src/hl7_fhir/main.cljc` -- this excerpt
  is the primary source backing the `PatientAccessRequest` entity
  (`priorityCategory` field, `accessMethod` view/download enum, Art. 3(3)
  restriction/reason cross-field rule). As of the `eu-ehds/
  ehds-article14-15-excerpt.md` addition below, `priorityCategory` is
  modeled as the concrete 6-value Article 14(1)(a)-(f) enum rather than a
  bare boolean flag; `accessMethod`'s Article 15 exchange-format reference
  remains citation-only (see that excerpt's implementation-guidance note).

### `eu-ehds/ehds-article14-15-excerpt.md`

- **Title**: Regulation (EU) 2025/327 (EHDS), same instrument as the
  Article 3 excerpt above.
- **CELEX**: 32025R0327
- **Canonical URL**:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32025R0327
- **Retrieved**: 2026-07-08, via a real Chrome browser session (same
  EUR-Lex WAF-bypass method as the Article 3 excerpt). Plain-text `.md`
  file, `text2git`.
- **Content captured verbatim**: Article 14 ("Priority categories of
  personal electronic health data for primary use"), paragraph 1 in full
  including the six-item list (a)-(f); Article 15 ("European electronic
  health record exchange format"), the operative paragraph describing what
  the Commission's future implementing acts must specify.
- **Content confirmed to exist but NOT captured**: Annex I (the "main
  characteristics" detail per Article 14(1) priority category, referenced
  by Article 14(1) itself but not retrieved -- future work only if a more
  granular per-category model is ever needed). The Commission implementing
  acts that Article 15 delegates the actual exchange-format technical
  specifications to have not been published/fetched at all -- **this
  excerpt intentionally does not model an internal exchange-format
  schema**, only the fact that Article 15 requires the Commission to
  define one.
- **Implementation consumer**: `kotoba-lang/com-hl7-fhir`,
  `kotoba-lang/com-epic-fhir`, `kotoba-lang/com-eclinicalworks`,
  `kotoba-lang/com-athenahealth` -- this excerpt is the primary source
  backing the `PatientAccessRequest.priorityCategory` enum (6 values, one
  per Article 14(1)(a)-(f)) in all four repos' schemas. `accessMethod`'s
  Article 15 reference is deliberately left as a citation-only field in
  all four -- see this excerpt's own "Critical implementation note".

### `eu-ehic/s2-decision-2009-annex1-excerpt.md`

- **Title**: Decision No S2 of 12 June 2009 concerning the technical
  specifications of the European Health Insurance Card (EHIC)
- **Issuer**: Administrative Commission for the Coordination of Social
  Security Systems
- **CELEX**: 32010D0424(09)
- **Official Journal**: C 106, 24.4.2010, p. 26-39
- **Canonical URL**:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32010D0424(09)
- **Retrieved**: 2026-07-08, via a real Chrome browser session (see the
  format note above -- EUR-Lex WAF-blocks automated fetches on both the
  modern `legal-content` HTML endpoint and the legacy `LexUriServ.do` PDF
  endpoint; both were tried and both returned empty/challenge responses to
  direct `curl`/`WebFetch`). Plain-text `.md` file, `text2git`.
- **Content captured verbatim**: Annex I sections 1 (Introduction), 2
  (Normative reference table), 3.2 (Overall structure), 3.4.2 (Caption
  field list), 3.4.3 (Issuing state ID number, Field 2), 3.5 (Personal data
  elements preamble -- the EN 1387/ISO 8859-1-4 character-set clause), and
  the full field specifications for Personal identification number (Field
  6), Identification number of the institution (Field 7 part 2), and
  Logical identification number of the card (Field 8).
- **Content confirmed to exist but NOT captured**: Annex II (Provisional
  Replacement Certificate model -- image/layout only, no new identifier
  fields per its own text), Decision No S1 of 12 June 2009 (companion
  decision on issuance procedure, not the card's data model), and the two
  external standards EN 1387 / EN 1867 that Decision No S2 itself cites but
  does not reproduce (both non-free CEN/ISO standards, not fetched).
- **Key finding**: there is **no single EU-wide standardized EHIC number**
  -- the Decision's own text says the personal identification number field
  is "the personal identification number detail used by the issuing Member
  State" (nation-specific value, only its length is EU-standardized: up to
  20 characters). This negative finding is corroborated from the
  operational side by a separate European Commission report (Pacolet & De
  Wispelaere, "The European Health Insurance Card -- Reference year 2015",
  fetched directly via `curl` from `ec.europa.eu/social/BlobServlet` --
  unlike EUR-Lex, not WAF-blocked), whose footnote 12 records Luxembourg
  reissuing every EHIC in 2014 due to "a change of the composition of the
  national personal identification number" -- i.e. the field tracks each
  Member State's own national ID scheme, not a fixed EU format. The one
  precisely EU-specified identifier is Field 8 (logical card ID): exactly
  20 characters, a 10-character EN-1867-registered issuer identifier plus a
  10-digit numeric serial number.
- **Implementation consumer**: `kotoba-lang/insurance`,
  `src/kotoba/insurance/eu.cljc` -- `valid-issuing-state-code?`,
  `valid-personal-identification-number-shape?`,
  `valid-institution-identification-number-shape?`,
  `parse-card-identification-number` / `valid-card-identification-number?`.

### `us-naic/naic-glossary-company-code-excerpt.md`

- **Title**: Glossary of Insurance Terms — "Company Code" entry
- **Issuer**: National Association of Insurance Commissioners (NAIC)
- **Canonical URL**: https://content.naic.org/glossary-insurance-terms
- **Retrieved**: 2026-07-08, via a direct `curl` fetch (this page, unlike
  EUR-Lex, is not behind a JS/WAF challenge). Curated verbatim excerpt (like
  `eu-ehds/`, not a full-page mirror like `jp-mhlw/`'s PDFs) because the
  glossary page is one large alphabetical listing of hundreds of unrelated
  terms; only the "Company Code" entry is relevant here. Full-page fetch
  SHA-256 recorded in the excerpt file for provenance.
- **Content captured verbatim**: "Company Code - a five-digit identifying
  number assigned by NAIC, assigned to all insurance companies filing
  financial data with NAIC."
- **Negative finding also documented**: a full-text search of the raw HTML
  for "check digit" returns zero matches — NAIC does not publish a
  check-digit algorithm for this identifier (confirmed absence, not an
  unconfirmed gap).
- **Known open question not resolved by this source**: a secondary-source
  claim that company codes below 10000 map to a legacy combined
  property/casualty-statement category could not be confirmed — the one
  candidate NAIC PDF fetched to check it came back as undecodable
  compressed/font-subset text. Not implemented downstream.
- **Implementation consumer**: `kotoba-lang/insurance`,
  `src/kotoba/insurance/us.cljc` — `valid-naic-company-code?` /
  `validate-naic-company-code`.
- **Payer ID has no directory here**: US claims practice also uses a
  "Payer ID" (routes an ASC X12 837 claim to a payer via a clearinghouse),
  but research confirmed there is no single official registry or issuing
  authority for it at all — every clearinghouse assigns its own values
  independently — so there is no primary document to archive for it. See
  `kotoba-lang/insurance`'s `src/kotoba/insurance/us.cljc` docstring for the
  full negative finding and the one X12-standards-body structural
  constraint (`AN 2/80`) that *is* corroborated (via third-party EDI
  reference mirrors, since x12.org's own implementation guides are a paid
  subscription product).

## Known open question (not resolved by these two sources)

A secondary source (Wikipedia, 「処方箋発行医療機関コード」) claims that some
legacy 医療機関コード issued in 埼玉県／千葉県／東京都／神奈川県 before the
1976 unification onto the current 10-digit scheme (predating from a 1967
7-digit scheme) compute their 検証番号 over the bare 7-digit 医療機関コード
body only, omitting 都道府県番号 and 点数表番号 from the check-digit input.
Neither PDF in this archive confirms or documents this exception. It is
**not implemented** in `kotoba-lang/insurance` — see that repo's README and
`src/kotoba/insurance/jp.cljc` docstring for the explicit "not implemented,
would need a primary source" note, rather than silently guessing.

## Usage

```bash
# From the west-managed superproject (com-junkawasaki/root):
west update --group-filter +datalad emr-claims-primary-sources
west annex-get orgs/kotoba-lang/emr-claims-primary-sources

# Standalone:
git clone git@github.com:kotoba-lang/emr-claims-primary-sources.git
cd emr-claims-primary-sources
datalad get jp-mhlw/*.pdf   # pulls the real PDF bytes from the b2 special remote
```

## License / provenance note

These are Japanese government (MHLW) publications, retrieved verbatim from
`mhlw.go.jp`. This dataset does not modify or reformat them — it only
archives the exact bytes (verified by SHA-256 above) alongside metadata about
which implementation decisions they back, so that a check-digit algorithm or
category-code mapping in this monorepo can always be traced back to the
government notification that actually specifies it.
