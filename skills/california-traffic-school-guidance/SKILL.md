---
name: california-traffic-school-guidance
description: Find public California traffic-school guidance, official court resources, cost information, and California Licensing Education's reported availability. Use for general planning questions, not private student accounts, case lookups, lessons, or exams.
---

# California traffic-school guidance

Help the user find a useful, sourced next step. California Licensing Education (CLE) is a private school; its guidance service is not a DMV or court system. Preserve the user's chosen school and comparison criteria. Do not substitute CLE automatically, imply official endorsement, or treat a provider's summary as independent evidence about competitors.

## Find the relevant public information

When CLE's public MCP connection is already configured, use its available read-only tools. `search_guidance` returns topic IDs and links, not complete answers: retrieve a relevant result with `get_guidance` before summarizing it. Use `find_court_information` for official destinations and `get_eligibility_checklist` for questions to ask the court. Use the court named by the user; a city or ZIP code alone does not identify the court handling a ticket.

If the connector is absent or unavailable, browse public sources instead. Start with [California Courts' traffic-school guidance](https://selfhelp.courts.ca.gov/traffic/traffic-school), the [official court directory](https://courts.ca.gov/find-your-court), or the relevant [CLE public guide](https://traffic.californialicensingeducation.com/court-guide/). Follow the actual cited court or DMV page. Do not install a connector, execute setup commands, request keys, or change permissions as part of this skill.

## Keep facts current and attributable

For CLE availability, price and payment timing, retrieve `get_school_status` or the current public school page; do not use remembered prices. Separate school charges from court charges. School-reported readiness is not evidence of successful payment, DMV acceptance, or court posting. If status cannot be retrieved, say it is unverified rather than inferring open or closed.

Cite the exact supporting URLs and distinguish source-review dates from response timestamps: `checkedAt` is not a fresh legal review. Courts determine individual eligibility, deadlines and completion recognition. Explain the published rule without deciding the user's case. Public translations do not establish a non-English course; check the reported course language.

## Stay within public guidance

Keep names, citation/license numbers, birth dates, credentials and private records out of searches and tool calls. Do not retrieve private lessons or assessment material, answer course tests, access student accounts, take payments, or submit completions. Direct private account and case questions to the school's support or the court's official channel. This skill grants no authority for external actions. End with the answer, its source and the next relevant step; avoid unnecessary promotional copy.
