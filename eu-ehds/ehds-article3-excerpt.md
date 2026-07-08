# EHDS Regulation (EU) 2025/327 — Article 3 excerpt (verbatim)

- Source: Regulation (EU) 2025/327 of the European Parliament and of the Council of 11 February 2025
  on the European Health Data Space and amending Directive 2011/24/EU and Regulation (EU) 2024/2847
  (Text with EEA relevance)
- CELEX: 32025R0327
- Official Journal: L series, 2025/327, published 2025-03-05, entered into force 2025-03-26
- Canonical URL: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32025R0327
- Retrieval method: EUR-Lex serves this page behind an AWS WAF JS challenge that blocks
  automated `curl`/headless fetch (verified: direct HTTP request returns HTTP 202 with an
  `awsWafCookie` challenge page, no article text). Retrieved 2026-07-08 via a real Chrome
  browser session (JS challenge passes normally for real browser navigation), then the
  rendered page's `document.body.innerText` was searched and the relevant passages extracted
  verbatim below. This is a curated excerpt, not a byte-identical mirror of the official PDF —
  noted honestly for provenance; a full-text/PDF mirror is future work if EUR-Lex access allows.

## CHAPTER II — PRIMARY USE / SECTION 1 heading

> Rights of natural persons in relation to the primary use of their personal electronic health
> data, and related provisions

## Article 3 — Right of natural persons to access their personal electronic health data

> 1.   Natural persons shall have the right to access at least personal electronic health data
> relating to them that belong to the priority categories referred to in Article 14 and are
> processed for the provision of healthcare through the electronic health data access services
> referred to in Article 4. Access shall be provided immediately after the personal electronic
> health data have been registered in an EHR system, while respecting the need for technological
> practicability, and shall be provided free of charge and in an easily readable, consolidated
> and accessible format.
>
> 2.   Natural persons, or their representatives referred to in Article 4(2), shall have the
> right to download free of charge an electronic copy of at least the personal electronic health
> data in the priority categories referred to in Article 14 related to those natural persons,
> through the electronic health data access services referred to in Article 4, in the European
> electronic health record exchange format referred to in Article 15.
>
> 3.   In accordance with Article 23 of Regulation (EU) 2016/679, Member States may restrict the
> scope of rights provided for in paragraphs 1 and 2 of this Article, in particular whenever
> those restrictions are necessary to protect natural persons, on the basis of patient safety and
> ethical considerations by delaying access to their personal electronic health data for a
> limited period of time until a health professional is able to properly communicate and explain
> to the natural persons concerned information that can have a significant impact on their
> health [text continues, not captured further].

## Cross-references confirmed (not yet fetched in full — future work)

- "priority categories" of personal electronic health data → defined/listed in **Article 14**
  (not yet retrieved verbatim)
- "electronic health data access services" → **Article 4** (not yet retrieved verbatim)
- "European electronic health record exchange format" → **Article 15** (not yet retrieved
  verbatim; the definitions article uses the term ~34 times but the dedicated defining
  article is Article 15, not the Article 2 definitions list)

## Implementation guidance derived from this excerpt

A minimal, defensible model based on confirmed text only:
- A boolean/enum capturing that a given health-data category is a "priority category" under
  Article 14 (do NOT enumerate the actual priority-category list without fetching Article 14 —
  unconfirmed, would be a guess).
- A flag/field for "primary-use access request" honoring: (a) immediate provision after
  registration, (b) free-of-charge, (c) EHR export format reference (Article 15), (d) the
  Article 23 GDPR-aligned restriction/delay-of-access carve-out for patient safety.
- Do NOT invent the "European electronic health record exchange format" technical schema
  itself (Article 15 content unconfirmed) — only reference it as an external format
  identifier/citation, not model its internal structure.
