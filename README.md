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

Scope: **Japan (JP) today, with US and EU expected to be added later** as
those jurisdictions' EMR/claims implementations mature and need primary-source
verification of their own identifier formats (e.g. US NPI check digit, EU
health-insurance card / EHIC formats). Layout convention: one directory per
jurisdiction (`jp-mhlw/`, and in the future `us-cms/`, `eu-*/` etc., named for
the issuing authority).

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
