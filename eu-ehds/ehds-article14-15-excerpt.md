# EHDS Regulation (EU) 2025/327 — Articles 14-15 excerpt (verbatim)

- Source: Regulation (EU) 2025/327, CELEX 32025R0327
- Canonical URL: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32025R0327
- Retrieval method: EUR-Lex serves this page behind an AWS WAF JS challenge that blocks
  automated curl/headless fetch. Retrieved 2026-07-08 via a real Chrome browser session
  (same method as the Article 3 / EHIC excerpts already archived), `document.body.innerText`
  searched and relevant passages extracted verbatim below.

## Article 14 — Priority categories of personal electronic health data for primary use

> 1.   For the purposes of this Chapter, where data are processed in electronic format the
> priority categories of personal electronic health data shall be the following:
>
> (a) patient summaries;
> (b) electronic prescriptions;
> (c) electronic dispensations;
> (d) medical imaging studies and related imaging reports;
> (e) medical test results, including laboratory and other diagnostic results and related
>     reports; and
> (f) discharge reports.
>
> The main characteristics of the priority categories of personal electronic health data for
> primary use shall be as set out in Annex I.
>
> Member States may provide in their national law for additional categories of personal
> electronic health data to be accessed and exchanged for primary use pursuant to this Chapter.

(Annex I itself, with the detailed "main characteristics" per category, was NOT retrieved —
future work if a more granular model is ever needed.)

## Article 15 — European electronic health record exchange format

> By [date specified elsewhere in the Regulation, not captured in this excerpt], the
> Commission shall, by means of implementing acts, establish the technical specifications for
> at least the priority categories referred to in Article 14(1), setting out the European
> electronic health record exchange format. Such format shall be commonly used, machine-readable
> and allow transmission of personal electronic health data between different software
> applications, devices and healthcare providers. Such format shall support transmission of
> structured and unstructured health data and shall include the following elements:
>
> (a) harmonised datasets containing electronic health data and defining structures, such as
>     data fields and data groups for the representation of clinical content and other parts
>     of the electronic health data;
> (b) coding systems and values to be used in datasets containing electronic health data;
> (c) technical interoperability specifications for the exchange of electronic health data,
>     including its content representation, standards and profiles.

**Critical implementation note**: Article 15 does NOT itself define the concrete technical
schema of the exchange format — it delegates that to future European Commission
*implementing acts* (secondary legislation, not yet published/fetched). Do NOT model an
"exchange format" internal structure from this Article; only the fact that such a format
exists and is externally defined can be cited/referenced.

## Implementation guidance

- `priorityCategory` may now be modeled as a concrete enum of 6 values matching Article 14(1)
  (a)-(f) verbatim, rather than a bare boolean flag.
- `accessMethod`'s reference to "European electronic health record exchange format" (Article 15)
  should remain a citation-only reference (e.g. a format-version/identifier string field), not
  an attempt to model the format's internal schema.
