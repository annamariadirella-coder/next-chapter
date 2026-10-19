# Next Chapter

*Your experience. Better understood.*

Job searching means repeating your story, checking scattered listings and deciding which requirements your experience actually supports. Next Chapter helps you keep that work together: find opportunities, ask useful clarification questions and prepare a truthful CV for a role you choose.

It is an independent open-source workflow you use with your own AI assistant. Your private Career Evidence Bank records experience you confirm; it is not an external certification or reference check.

## Choose your starting point

| You want to… | Start with | What you need |
|---|---|---|
| Use your existing CV to assess a role and prepare an application | [Start here](START-HERE.md) | Your CV and an AI assistant; a pasted job description works without browsing |
| Understand the process before sharing personal information | [Try the fictional example](examples/first-application.md) | Supplied fictional inputs; no scanner or Google setup |
| Collect opportunities on a daily schedule | [Install the optional scanner](apps-script/README.md) | A Google account, private reference files and a tracker; setup and authorization required |

**Start with your CV. Add the scanner later if useful.** Downloading or starring this repository does not run anything.

## What you get

A typical review explains which requirements your confirmed experience supports, what remains unknown and which short questions could change the decision. For a role you choose, your assistant prepares a tailored CV and requested answers for your review. Downloadable documents depend on the assistant's capabilities.

For example, “built automation” may become “defined routing requirements, coordinated testing and trained the team” after you clarify that Engineering wrote the integration. The aim is a more accurate application, not a fabricated stronger claim. [See the full fictional walkthrough](examples/first-application.md).

The optional scanner produces a private review packet. An employer-verified posting means its source was checked during collection; it does not mean the job is suitable for you, that pay is confirmed or that you can legally work from your location.

## How it works

The assistant helps with four steps:

1. Find relevant vacancies and verify the original employer posting.
2. Check the applicant's private tracker to avoid duplicate applications.
3. Map material requirements to confirmed experience, transferable experience and unresolved questions.
4. Ask only questions that can materially change the application, then prepare a targeted CV and any requested application answers.

The applicant decides whether to apply and submits the application.

**Have a CV already? [Start here](START-HERE.md).** No scanner installation or complete Evidence Bank is needed to begin. Copy the starter message into your assistant, attach your CV privately and let it draft your first profile and evidence records for confirmation.

[Fictional first application](examples/first-application.md) · [Morning scan setup](apps-script/README.md) · [Troubleshooting](TROUBLESHOOTING.md)

Try the fictional walkthrough with its supplied CV, JDs and tracker; see [review results and limits](FLOW-REVIEW.md). No installation or real application is needed.

**Is the scan doing enough?** [Check coverage and deferred work](SCAN-COVERAGE.md). An optional offline audit reports counts without changing your scan or exposing vacancy content.

## What is included and what it costs

This package contains a reusable assistant instruction, an Evidence Bank template, a tracker template, a review checklist and an optional Google Apps Script morning scanner. It is a documented, human-guided workflow, not an autonomous application agent. The scanner runs only after you configure it in your own Google account.

Connected browsing, document and spreadsheet tools depend on the assistant environment. The files themselves require no API subscription. An existing assistant subscription or optional external services may have their own costs and limits.

## Start

1. Follow [Start here](START-HERE.md) with the CV you already have.
2. Confirm a short profile and draft Evidence Bank prepared by the assistant; unknown facts stay unknown.
3. Request a small set of relevant, employer-verified jobs, or provide a JD if browsing is unavailable. An empty set is acceptable if no credible match is found.
4. Answer only decisive clarification questions, choose a role and review its tailored CV before submitting it yourself.
5. Optionally add the morning scanner later. Configure its literal filters with [the search-profile example](templates/search-profile.example.json), run the read-only configuration check and bring the private report back to your assistant.

## Design principles

- Direct user clarifications outrank older source wording. Keep facts and scope boundaries explicit.
- A job title alone is insufficient to establish fit or exclude a role.
- Mandatory requirements and preferences must be distinguished.
- Missing evidence is an uncertainty, not proof the applicant has never done something.
- Supervising a technical implementation does not establish personally building it.
- Collaboration and influence do not automatically establish final ownership.
- No invented experience, metrics, tools, language proficiency or seniority.
- No quota of weak recommendations, fabricated fit percentages or guaranteed interview predictions.
- Errors, partial coverage and unverified employer availability must be disclosed.
- No autonomous applications, outreach, payments or changes to source documents.

## Privacy

Career records, CVs, tracker exports, contact information and clarification histories stay in the applicant's private environment. Publish only blank templates, generic instructions and fictional examples. Do not publish real job-search screenshots containing personal information.

## Morning scanner

The collector reads private reference files and a Google Sheets tracker, rotates through configured employer ATS feeds, checks public discovery feeds, filters/deduplicates jobs and saves a private review packet. It distinguishes employer-verified jobs from discovery leads. Collection alone does not establish personal fit and never creates a CV or applies for a job.

With no custom profile, the included defaults target senior Operations/Strategy/Product-adjacent roles in Germany and remote Europe. Set SEARCH_PROFILE_JSON privately to change literal role terms, excluded titles, location terms, remote regions, junior filtering and the mandatory-German rule without editing code. The source catalog stays fixed; coverage for a new target may be limited. Other language requirements and legal eligibility need human review. The Evidence Bank does not silently rewrite your filters.

An existing working installation does not need replacement to use the assistant workflow. Do not create a duplicate trigger or output writer. See [setup and existing-installation guidance](apps-script/README.md).

## Tests and provenance

Run the JavaScript suites listed in [the checks workflow](.github/workflows/checks.yml) from the repository root with Node.js 24, matching CI. These use synthetic inputs. The collector and its fixtures are a pinned MIT-licensed snapshot from JobOps; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). No private runtime data is included.

Run `node tests/search_profile.test.cjs` for the configurable-profile and read-only-check tests. Custom profiles use the guided assistant review; the inherited paid scorer is blocked for them because its prompt assumes Germany.

These tests cover collector behavior and optional scoring guardrails; they do not prove that the assistant workflow will find a job or generate error-free application documents. See [verification scope](VERIFICATION.md).

## Current limitations

The workflow requires human judgment and source verification. Exact quotations establish provenance, not semantic correctness. Job availability can change; web research is not exhaustive. A polished CV cannot guarantee an interview or job offer. The workflow has not undergone an independent accuracy benchmark.

## License

MIT. Copyright notices for the reused collector are retained. LinkedIn publication is a separate action; no post is sent by this project.
