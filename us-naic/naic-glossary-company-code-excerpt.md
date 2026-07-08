# NAIC Glossary of Insurance Terms — "Company Code" entry (verbatim)

- Source: Glossary of Insurance Terms, National Association of Insurance
  Commissioners (NAIC)
- Issuer: National Association of Insurance Commissioners (the standard-
  setting body for this identifier — this is a primary source, not a
  third-party restatement)
- Canonical URL: https://content.naic.org/glossary-insurance-terms
- Retrieval method: direct `curl` (no browser automation needed — unlike
  EUR-Lex in `eu-ehds/`, this page is **not** behind a JS/WAF challenge; a
  plain HTTP GET with a standard desktop-browser `User-Agent` string
  returned the full HTML page directly, HTTP 200).
- Retrieved: 2026-07-08
- Full-page fetch size: 396,089 bytes
- Full-page fetch SHA-256: `8464fe199d08871297d0e95067a6fa3ad2827f1e32f62bd6581cf237a2fa7eb4`
  (of the complete raw HTML page as served at the URL above on the retrieval
  date; not committed to this dataset in full because the glossary page is a
  single large alphabetical listing of hundreds of unrelated insurance
  terms — only the one relevant entry is excerpted verbatim below, per this
  dataset's "curated excerpt" convention already used for `eu-ehds/`).

## Verbatim excerpt (raw HTML, entry unmodified)

> **Company Code** - a five-digit identifying number assigned by NAIC,
> assigned to all insurance companies filing financial data with NAIC.

(Extracted from the raw HTML via `grep`, i.e. read directly from the fetched
bytes — not summarized or paraphrased by an intermediate tool. The
surrounding HTML markup, `<strong>Company Code&nbsp;</strong>- a five-digit
identifying number assigned by NAIC, assigned to all insurance companies
filing financial data with NAIC.`, confirms this is the complete, unedited
entry — it is not truncated.)

## Negative finding: no check-digit algorithm documented

A full-text search of the fetched raw HTML for the string "check digit"
(case-insensitive) returns **zero matches** anywhere on the entire glossary
page. There is also no separate "NAIC Number" glossary entry distinct from
"Company Code". Combined with the absence of any check-digit mention in
HL7 Terminology's `NAICCompanyCodes` NamingSystem registration (which cites
this same NAIC glossary page as its source — OID
`2.16.840.1.113883.6.300`), this is treated as a confirmed negative: **NAIC
does not publish a check-digit algorithm for the company code**, rather than
an unconfirmed absence. See `kotoba-lang/insurance`'s
`src/kotoba/insurance/us.cljc` namespace docstring for how this shapes the
implementation (5-digit shape validation only, no check-digit function).

## Known open question (not resolved by this source)

A numeric-range convention (company codes below 10000 allegedly mapping to
a legacy combined property/casualty statement category) was encountered
only as secondary search-result summaries, never confirmed by reading a
full primary document — the one candidate NAIC PDF fetched to check this
(`https://content.naic.org/sites/default/files/publication-loc-zu-listing-companies-summary.pdf`)
returned as an undecodable compressed/font-subset stream rather than
extractable text. **Not implemented** in `kotoba-lang/insurance` — see that
repo's README and `src/kotoba/insurance/us.cljc` docstring for the explicit
"not implemented, would need a primary source" note, in the same spirit as
`jp.cljc`'s pre-1976 legacy-code exception note.

## Implementation consumer

`kotoba-lang/insurance`, `src/kotoba/insurance/us.cljc` —
`valid-naic-company-code?` / `validate-naic-company-code`.
