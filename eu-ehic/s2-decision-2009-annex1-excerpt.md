# Decision No S2 of 12 June 2009 — Annex I excerpt (verbatim)

- Title: Decision No S2 of 12 June 2009 concerning the technical
  specifications of the European Health Insurance Card
- Issuer: Administrative Commission for the Coordination of Social Security
  Systems (adopted under Article 72(a) of Regulation (EC) No 883/2004 of the
  European Parliament and of the Council of 29 April 2004, and Regulation
  (EC) No 987/2009 of 16 September 2009)
- CELEX: 32010D0424(09)
- Official Journal: C 106, 24.4.2010, p. 26-39
- Canonical URL: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32010D0424(09)
- Retrieval method: EUR-Lex serves this page (both the modern
  `legal-content/EN/TXT/HTML/?uri=CELEX:...` endpoint and the legacy
  `LexUriServ.do?uri=OJ:...` PDF endpoint) behind an AWS WAF JS challenge
  that blocks automated `curl`/headless fetch (verified 2026-07-08: a direct
  `curl` request to the legacy PDF endpoint returns HTTP 202 with an empty
  body — a WAF challenge page, no document content — and `WebFetch` against
  the modern HTML endpoint likewise returns empty content). Retrieved
  2026-07-08 via a real Chrome browser session (the JS challenge passes
  normally for real browser navigation, same method used for
  `eu-ehds/ehds-article3-excerpt.md`), then the rendered page's text was
  extracted and the operationally relevant clauses transcribed verbatim
  below. This is a curated excerpt (Annex I only — the substantive
  technical-specification annex — not Annex II's certificate model image,
  and not the card-background/colour/font layout clauses that do not bear
  on any identifier format), not a byte-identical mirror of the official
  PDF, consistent with how `eu-ehds/` and `us-naic/` are already documented
  as curated excerpts rather than full-page mirrors in this dataset's
  README.

## DECISION No S2 of 12 June 2009 (recitals, verbatim)

> In order to facilitate the acceptance and the reimbursement of the costs
> of benefits in kind provided on the basis of a European Health Insurance
> Card, it is necessary for the three main parties concerned, namely the
> insured person, the health care providers and the institutions, to
> recognise easily and accept the European Health Insurance Card in
> conformity with a single model and uniform specifications.

> The information which must be visible on the European Health Insurance
> Card is defined in point 7 of Decision No S1. The introduction of a
> European Health Insurance Card with visible data is the first stage of a
> process leading to the use of an electronic medium proving entitlement to
> benefits in kind during a temporary stay in a Member State other than the
> competent one or the State of residence.

## ANNEX I — Technical provisions concerning the design of the European Health Insurance Card (excerpt)

### 1. INTRODUCTION (verbatim)

> In compliance with the related Decisions of the Administrative Commission
> for the Coordination of Social Security Systems, the European Health
> Insurance Card provides a minimum set of 'eye-readable' data to be used
> in a Member State other than the Member State of insurance or residence
> for:
> — Identifying the insured person, the competent institution and the card
> — Stating the entitlement to receive care during a temporary stay in
>   another Member State.

### 3.2. Overall structure (verbatim)

> The format of the European health insurance card complies with the ID-1
> format (53,98 mm high, 85,60 mm wide and 0,76 mm thick). However, if the
> European health insurance card takes the form of a sticker to be applied
> on the reverse side of a national card, the ID-1 thickness criterion will
> not apply.

### 3.4.2. Caption (verbatim, field list only)

> The values are written in a European Union official language and are set
> as follows (using English as the base text):
> 1. (no caption for the form identifier)
> 2. (no caption for the issuing Member State code number)
> 3. Name
> 4. Given names
> 5. Date of birth
> 6. Personal identification number
> 7. Identification number of the institution
> 8. Identification number of the card
> 9. Expiry date

### 3.4.3. Issuing state (verbatim)

> Field Name: Issuing state ID number
> Description: Identification code of the card issuer's state.
> Position: Field 2: Centrally positioned within the European mark with a
> white square 4 mm high and 4 mm wide.
> Values: The 2 digit ISO country code (ISO 3166-1)
> Format: Font 'Verdana True Type' or equivalent, in capital and regular
> style, 7 point size, black, with character width compressed to 90 % of
> normal size and 'normal' position and spacing of characters.
> Length: 2 characters.
> Remark: The code 'UK' will be used instead of 'GB', the standard ISO code
> for United Kingdom. One single code will be used for each Member State.

### 3.5. Personal data elements — preamble (verbatim)

> The personal data elements have the following common characteristics:
> — Compliance with EN 1387 with regard to the character set: Latin
>   alphabet Nos 1-4 (ISO 8859-1 to 4))
> — If there is a need to abbreviate elements due to the limited number of
>   spaces, this must be indicated by a full stop.
> Data will be laser or thermal-transfer printed or engraved but not
> embossed.

### 3.5.2. Card holder related data elements — Personal identification number (verbatim)

> Field Name: Personal identification number of card holder
> Description: The personal identification number detail used by the
> issuing Member State.
> Position: Field 6
> Values: See applicable Personal identification number
> Format: Font 'Verdana True Type' or equivalent, in regular style, 7 point
> size, black, with character width compressed to 90 % of normal size and
> 'normal' position and spacing of characters. Aligned to the right border
> when on the front side of the card, but to the left when on the reverse
> one. Line spacing of 3 points plus character size
> Length: Up to 20 characters for the ID code.
> Remark: The personal identification number of the card holder or, when no
> such number exists, the number of the insured person from whom the
> rights of the card holder derive. Personal attributes, such as gender,
> status of family member, cannot be assigned a dedicated field on the
> card. They can, however, be included within the personal identification
> number.

### 3.5.3. Competent institution related data elements — Identification number of the institution (verbatim)

> Field Name: Identification number of the institution
> Description: Identification code awarded nationally to the
> 'institution', viz. the competent institution of insurance.
> Position: Field 7, part 2
> Values: See national code list of competent institutions
> Format: Font 'Verdana True Type' or equivalent, in regular style, 7 point
> size, black, with character width compressed to 90 % of normal size and
> 'normal' position and spacing of characters. Field 7 is aligned to the
> right border and Part 2 is to the left of Part 1. Line spacing of 3
> points plus character size.
> Length: Between 4 and 10 characters.
> Remark: Complementary up-to-date and historical information which may be
> required for communicating with the institution could be made available
> on the Internet thanks to a knowledge centre tool. The competent
> institution may be different from the liaison body or the organisation
> in charge of the cross-border reimbursement as well as from the
> organisation in charge of technically issuing the European health
> insurance card.

### 3.5.4. Card related data elements — Logical identification number of the card (verbatim)

> Field Name: Logical identification number of the card
> Description: Logical individual number aiming at uniquely identifying the
> card and assigned to each card by the card issuer. It is made up of two
> parts, the issuer identifier number and the serial number of the card.
> Position: Field 8
> Values: The first 10 characters identify the card issuer in compliance
> with the standard EN 1867 of 1997. The last 10 digits constitute the
> unique serial number
> Format: Font 'Verdana True Type' or equivalent, in regular style, 7 point
> size, black, with character width compressed to 90 % of normal size and
> 'normal' position and spacing of characters. Line spacing of 3 points
> plus character size
> Length: 20 characters (with leading 0 as needed in the 10 digits used for
> the unique serial number of the card).
> Remark: For assigning an issuer identifier number, an ad hoc registration
> procedure may be used, instead of the official one as defined in the
> standard EN 1867, in the Member States which issue European health
> insurance cards without an electronic component. This logical card ID
> number must enable the information carried by the card to be checked
> against the information held by the issuing organisation for the same
> logical number, for example in order to reduce the risk of fraud or to
> identify errors in data entry when processing the information of the
> card for claim reimbursement purposes.

### 2. NORMATIVE REFERENCE (verbatim, table)

> ISO 3166-1 — Codes for the representation of names of countries and
> their subdivisions – Part 1: Country codes (1997)
> ISO/IEC 7810 — Identification cards – Physical characteristics (1995)
> ISO/IEC 7816 — Identification cards – Integrated circuit(s) cards with
> contacts, Part 1: Physical characteristics (1998), Part 2: Dimension and
> location of the contacts (1999)
> ISO 8859 series — 8-bit single-byte coded graphic character sets, Part
> 1-4: Latin alphabet Nos 1 to 4 (1998)
> EN 1867 — Machine readable cards – Health care application – Numbering
> system and registration procedure for issuer identifiers (1997)

## Content confirmed to exist but NOT captured here

- Annex II (Provisional Replacement Certificate model) — image/layout only,
  not transcribed (the certificate "contains, in the same order, the same
  data as the European card (fields 1 to 9)", so no new identifier fields).
- Decision No S1 of 12 June 2009 (OJ C 106, 24.4.2010, p. 23-25) — the
  companion decision on *whether* an EHIC or a Provisional Replacement
  Certificate is issued (procedural), not the card's technical data model.
  Not fetched in this cycle.
- EN 1387 (printing character-set standard) and EN 1867 (issuer-identifier
  numbering/registration standard) — both are separate CEN/ISO standards
  cited by Decision No S2 but not themselves free-access documents; not
  fetched.
- Card background colour/font/layout clauses (Annex I sections 3.3, 3.4.1,
  3.6) — not transcribed here as they carry no identifier-format
  information.

## Implementation guidance derived from this excerpt

A minimal, defensible model based on confirmed text only (see
`kotoba-lang/insurance`, `src/kotoba/insurance/eu.cljc`):

- There is **no single EU-wide standardized EHIC "number"**: Field 6
  ("Personal identification number") is explicitly "the personal
  identification number detail used by the issuing Member State" — a
  nation-specific value with no documented cross-Member-State digit count
  or check digit. Only its length bound (up to 20 characters) is
  EU-standardized.
- Field 7 part 2 ("Identification number of the institution") is likewise
  nationally assigned ("see national code list of competent institutions"),
  with only a length bound (4-10 characters) standardized.
- Field 8 ("Logical identification number of the card") is the one
  precisely specified identifier: 20 characters total, split into a
  10-character EN-1867-registered issuer identifier (not itself modelled —
  EN 1867 not fetched) and a 10-digit numeric serial number.
- Field 2 ("Issuing state ID number") is a 2-character code, nominally ISO
  3166-1 alpha-2 with the documented "UK instead of GB" exception — only
  the 2-uppercase-letter shape is validated (no full ISO 3166-1 membership
  table embedded — a scope decision, not a sourcing gap).
- Do NOT implement a character-set check against "Latin alphabet Nos 1-4
  (ISO 8859-1 to 4)" (EN 1387) — the referenced standard was not fetched,
  and a portable approximation across JVM/ClojureScript/SCI/GraalVM would
  be an invented rule, not a sourced one.
