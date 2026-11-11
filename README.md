# Employee Benefits

The common benefits-administration vocabulary -- benefit plans, the employees' enrollments in them, their dependents, and the deductions they create -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Employee Benefits, Benefits Administration, Health Benefits, Retirement Plans, 401k, HSA, Group Insurance in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| benefit_plan | 10 | 10 | id 80%, plan_type 70%, name 60%, description 50% | plans 6, benefits 6, plan 2, benefit 1 |
| enrollment | 10 | 9 | id 78%, employee 56%, status 56% | enrollments 4, coverage 3, enrollment 2, coverages 2 |

Cohort: 37 providers with harvested OpenAPI, 18 crosswalks. Of the providers exposing a benefit_plan: 50% create, 90% list, 90% fetch, 20% update, 20% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Benefit plans agree on id, plan_type, name and description: a plan is a typed offering (medical, dental, 401k, HSA), and the type decides the rest of its shape.
- Enrollments agree on id, employee and status; the effective start date reaches 44%.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- start_date and end_date keep the benefits words for coverage dates (effective_date maps to start_date), because coverage dates are calendar dates, not timestamps.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
