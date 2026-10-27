# Canadian home energy rebate programs

An open dataset of Canadian home energy rebate, grant, loan and tax-credit programs for homeowners, landlords and renters. It covers federal, provincial, territorial, utility and municipal programs across all 13 provinces and territories. Published by [RebateHub.ca](https://rebatehub.ca/data), an independent Ontario business. It is not a government site and does not take applications.

<!-- stats:start -->
Snapshot 2026-10-25: 181 program records. 135 current (124 open, 4 closing soon, 5 waitlist, 2 upcoming) and 46 closed.
<!-- stats:end -->

Always confirm details with the program administrator before you buy or install anything. Programs change, sometimes without notice.

## Files

| File | What it is |
|---|---|
| [`data/programs.csv`](data/programs.csv) | One row per program. UTF-8, comma separated, header row. Lists (eligibility, categories) are joined with ` \| `. |
| [`data/programs.json`](data/programs.json) | The same records with nested incentives, plus licence, attribution and update date at the top. |
| [`datapackage.json`](datapackage.json) | [Frictionless Data](https://datapackage.org/) description of the CSV, with a typed schema. |
| [`CITATION.cff`](CITATION.cff), [`.zenodo.json`](.zenodo.json) | Citation and archive metadata. |

The live, always-current files are at <https://rebatehub.ca/data/rebates.csv> and <https://rebatehub.ca/data/rebates.json>. There is also a read-only JSON API: <https://rebatehub.ca/api/v1/programs> (filters such as `?province=on&category=heat-pumps&status=open`).

Records include closed programs, so you can see what was replaced.

## Fields

Every record follows one schema. The CSV has one column per field below. The JSON adds `jurisdictionNames`, `categoryNames` and `currency` (always `CAD`) for readability.

<!-- fields:start -->
| Column | Meaning |
|---|---|
| `id` | Stable identifier. Our program page is /rebates/{id}. |
| `name` | Program name in English, as the administrator writes it. |
| `shortName` | Common short name or acronym, if there is one. |
| `administrator` | The government body, agency or utility that runs the program. |
| `level` | Level of government: federal, provincial, utility, municipal. |
| `jurisdictions` | Province or territory codes it covers. CA means Canada-wide. |
| `regions` | Cities or areas it is limited to, if any. |
| `status` | One of open, closing-soon, waitlist, upcoming, closed. |
| `categories` | Upgrades it pays for, such as heat-pumps or insulation. |
| `audience` | Who can apply: homeowners, landlords, renters, low-income, businesses, new-builds. |
| `summary` | One-sentence plain-language summary. |
| `description` | Longer plain-language description. |
| `maxAmount` | Largest amount in Canadian dollars across its tiers. Empty when there is no single maximum. |
| `amountDisplay` | The amount in words, as shown on our pages. |
| `fundingType` | Kind of support: rebate, grant, loan, interest-free-loan, tax-credit, free-upgrade, point-of-sale-discount. |
| `incentives` | Each upgrade and what it pays. In the CSV, each item is written as “measure: amount”. |
| `eligibility` | The main eligibility rules. |
| `howToApply` | Application steps, in order. |
| `requiresAudit` | Whether an energy assessment is required. Empty when the program doesn’t say. |
| `requiresPreapproval` | Whether you must be approved or registered before buying or installing. Empty when it varies by upgrade or the program doesn’t say. |
| `incomeTested` | Whether the program has an income limit. |
| `stackableWith` | Ids of programs its administrator says it can be combined with. Our totals only add programs recorded as combining. |
| `stackableWithLevels` | Levels of government (e.g. provincial) whose programs it says it can be combined with, when it says so in general terms. |
| `excludesWith` | Ids of programs that can’t pay for the same upgrade as this one. Only the larger is counted in our totals. |
| `stackingGroup` | Programs sharing this group can’t both pay for the same upgrade (e.g. one Hydro-Québec or Québec-government grant per heat pump). |
| `deadline` | Official deadline (YYYY-MM-DD), if one is published. |
| `startDate` | Start date (YYYY-MM-DD), if one is published. |
| `officialUrl` | The administrator’s program page, where you apply. |
| `sourceUrls` | Every official source we used for the record. |
| `lastVerified` | Date we last checked the record against official sources (YYYY-MM-DD). |
| `confidence` | Our confidence in the record: high, medium or low. See the methodology page. |
| `notes` | Guidance and caveats for readers. |
| `homeTypes` | Set only when a program is limited to a kind of home (house or condo). |
| `heatingFuels` | Set only when a program is limited to homes heated by these fuels, e.g. a gas utility's offer to its own customers. |
| `url` | Our page for the program. |
<!-- fields:end -->

## How it is made

Each record is checked by a person against the official program pages listed in its `sourceUrls`. The method, confidence levels and corrections policy are at <https://rebatehub.ca/methodology>. What changed and when is at <https://rebatehub.ca/rebate-tracker> (RSS: <https://rebatehub.ca/rebate-tracker/feed.xml>).

## Update cadence

- The site is checked every day: an automated job compares a rotating batch of official pages with the version last reviewed.
- A person reviews each flagged change every week before a record is edited.
- Medium and low confidence records, and anything not checked in 30 days, are re-verified every month.
- This repository is refreshed once a month, and sooner after a major program change (a new federal program, a program closing). Each refresh is a tagged release (`vYYYY.MM.DD`, the date the data was last verified), which is archived with a DOI on Zenodo once connected.

## Limits

- Amounts are the maximum for the measure named, not what a typical household receives.
- "Upcoming" means announced but not open. Do not treat it as available.
- `maxAmount` is empty when a program has no single maximum.
- Eligibility is decided only by each program's administrator.

## Licence

[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may copy, share and adapt the data, including commercially, if you give credit and say if you changed it. Credit line:

> Source: RebateHub.ca, CC BY 4.0

Link "RebateHub.ca" to <https://rebatehub.ca/data> where you can. Do not present the data as coming from a government or utility.

## How to cite

> RebateHub.ca (2026). Canadian home energy rebate programs dataset. https://rebatehub.ca/data

GitHub shows a "Cite this repository" button from [`CITATION.cff`](CITATION.cff). Once archived, cite the version DOI shown on the Zenodo record.

## Corrections

Open an issue with the program and a link to the official source, or email hello@rebatehub.ca.

## Maintainers

Maintained by RebateHub.ca, an independent Ontario business. Records are reviewed by the Rebate Researcher, RebateHub. Source and full site: <https://rebatehub.ca>.
