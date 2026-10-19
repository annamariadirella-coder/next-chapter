# Optional morning scanner

This is a standalone private Google Apps Script installation. Repository publication does not install it, create triggers, access your Drive files or enable paid AI.

## Defaults and scope

Without SEARCH_PROFILE_JSON, the original defaults remain senior Operations/Strategy/Product-adjacent roles in Germany and remote Europe. Optional SEARCH_PROFILE_JSON sets literal role/location terms and basic filters without code edits. The company catalog is still BOARD_ROWS in Code.gs; profile changes do not discover an entire new market. The Evidence Bank and Charter do not automatically configure these filters. See the runtime report for actual completed, unavailable and unchecked sources.

## Optional private search profile

Copy [the example](../templates/search-profile.example.json), change it with your assistant and confirm the terms before storing the complete JSON string in the private SEARCH_PROFILE_JSON property. All fields are required. No personal data belongs in the public example.

- candidate_location: country you will work from, for example Spain. This supports simple explicit-exclusion checks; it is not a legal eligibility check.
- role_keywords / excluded_title_keywords: literal phrases matched in job titles, not regex expressions.
- locations: country/city terms that you accept. Include expected aliases where necessary, such as Germany/Deutschland.
- remote_regions: region labels accepted only when the location mentions remote. Explicit country-only restrictions and simple exclusions take precedence.
- require_remote: true excludes locations that do not explicitly say remote.
- exclude_junior: true excludes internship/junior/working-student/entry-level titles.
- allow_mandatory_german: whether the basic filter may retain explicit professional German requirements. Other languages and ambiguous requirements must be reviewed in the assistant.

An absent/empty property preserves the original defaults; malformed or unsupported JSON blocks collection before source/network work or output writes. The JSON string is limited to 8,500 characters, below the Apps Script property-value limit for these inputs. Each list accepts at most 30 nonempty terms of at most 80 characters. Review job eligibility against the original employer even when a location term matches. Profile changes may remove now-ineligible postings from the pending queue; export a private backup first if you want to retain old leads separately.

## New installation

Download the repository ZIP from GitHub's **Code → Download ZIP** menu and extract it first, so the files referenced below are available. Allow time for manual setup; this is not a one-click installation. If you already have a working scanner, use [existing-installation guidance](#existing-working-installations) instead.

1. Complete the Evidence Bank template privately. Create a private targeting document describing role/location/language preferences. Supported sources include native Google Docs, DOCX and text files.
2. Import `templates/tracker-template.csv` into a native Google Sheet. Preserve Company, Role title, Source and Status headers; the scanner reads this sheet and does not write to it.
3. Create an empty private Drive folder to provide the initial OUTPUT_FOLDER_ID. No reports are published.
4. Create a standalone Apps Script project. Add Code.gs, show the manifest in project settings and copy appsscript.json. Keep the default Google Cloud project. Enable the Drive v3 and Sheets v4 advanced services listed in the manifest.
5. In private Script Properties, set:

| Property | Value to provide privately |
|---|---|
| EVIDENCE_FILE_ID | Your Evidence Bank file ID |
| CHARTER_FILE_ID | Your targeting document file ID |
| TRACKER_SHEET_ID | Your native Google Sheet ID |
| TRACKER_RANGE | Full application tab, for example `'Applications'!A1:N500` using your actual tab name |
| OUTPUT_FOLDER_ID | The empty private initial folder ID |

6. Run `checkConfiguration` first. It reads settings and source access, checks tracker headers and validates the profile. It creates no folder/trigger/report. Resolve blocked checks using [troubleshooting](../TROUBLESHOOTING.md). Then run `initializeOutputFolder` once. It creates an app-owned private output folder and stores its ID. Existing state in the initial folder is carried forward if present; the old folder is retained.
7. Run `scanJobs` manually, authorize the existing scopes and inspect Executions and the Drive reports. Verify duplicates, source failures, location/language filtering and job links.
8. After the manual scan succeeds, run `enableDailyScan` once. The default window is 09:00–10:00 Europe/Berlin, not an exact minute. Adjust the scheduler timezone/hour if necessary.

Never commit Script Property values, source files, reports or credentials. Do not deploy the collector as a public web app.

### How to tell whether your first scan worked

- The manual `scanJobs` execution finishes without an unhandled error.
- Your app-owned private output folder contains `candidates.md`, `candidates.json` and `processed_jobs.json`.
- Open `candidates.md`: check the run date and completed sources, failures and deferred work. Zero candidates can be a valid result; partial coverage is not a complete search.
- Open an original employer link and compare its location and requirements with the report before deciding what to pursue.
- Confirm the tracker was read and inspect duplicate checking. If access or headers are wrong, fix them before relying on the result.

Only then enable the daily trigger. Reports stay in Drive; the scanner does not email you a shortlist or start an assistant conversation. Bring `candidates.md` into your private assistant conversation for evidence-based review. If something fails, start with [troubleshooting](../TROUBLESHOOTING.md).

## Existing working installations

The assistant instructions and templates can be used with an existing scanner without reinstalling it. If explicitly updating the collector, back up the installed code, keep the existing private properties/folder/state/manifest/trigger and verify compatibility. Do not call initializeOutputFolder or enableDailyScan again. Do not run another process against the same output folder concurrently.

## Output and limits

The scanner writes processed_jobs.json, candidates.json and candidates.md in its private folder. candidates.json includes the active search profile. Candidates contain up to 20 employer-verified postings, with deferred work retained. Aggregator discovery leads are separate and unverified. These counts are work budgets, not shortlist quotas or evidence of suitable jobs. Bring candidates.md into your assistant as described in [Start here](../START-HERE.md); there is no automatic morning conversation or CV generation.

Default board work budget: 80 attempted boards per run, with rotation and pagination checkpoints. Public discovery feeds include Arbeitnow, Jobicy, Remotive, We Work Remotely, Remote OK, Working Nomads and Himalayas. Source failures are logged as partial coverage. Check the employer's original posting before acting on an opportunity.

Wellfound is recorded as `manual_review_required`; this collector does not automatically search it. Remote.co, Jobgether, AI Jobs, Remote Woman and JS Remotely are not connected. Remote.co's published terms restrict automated collection. Toptal should be checked through its employer careers page. Do not interpret this list as automatic market coverage.

Working Nomads uses the public API linked from its own website. Its response is treated as a current window with unknown completeness, not a paginated inventory. Himalayas uses its official search API: up to three query groups per day, each with the newest page and one saved backlog page (at most six page fetches, with bounded HTTP retries). Groups rotate across later runs. The defaults cover operations, strategy, enablement, delivery, partnerships and music with country DE; custom search profiles supply their own role keywords and country where recognized. An unrecognized country leaves the upstream country filter unset and local eligibility filters still apply. Country metadata can be strings or named objects. Missing location restrictions are rejected rather than assumed worldwide; an explicit empty array means worldwide in the provider's schema. Timezone and salary-period metadata are retained for human review, not used as proof of eligibility or annual base salary.

Successful batches from these two sources are cached for the same UTC day and search plan; failed batches may be retried on a later run. `cached_daily=true` means no new request was made, and retained leads are reused without claiming a fresh employer check. The six-page Himalayas work budget counts page fetches; the existing bounded HTTP retry policy also applies. Schema changes or request failures leave the previous checkpoint and review queue available. Expired Himalayas records are excluded when the provider supplies a valid expiry timestamp. All window sizes and query/page counts are work budgets, not shortlist quotas or full-market coverage.

Himalayas data must stay in the private review workflow. Preserve its source credit and original `applicationLink` for application navigation. Do not republish its job data to other job boards, aggregators, Google Jobs or LinkedIn Jobs. Verifying employer facts is a separate read-only review step; this collector never submits applications.

The We Work Remotely adapter reads its official RSS feed and prefers an explicit country list over a broad region label. Missing locations are not replaced with worldwide eligibility. Feed metadata can still conflict with the job description: location, compensation, seniority and fit require employer verification.

The collector also maintains `archived_jobs.json` in the same private output folder. Unseen discovery leads older than 14 days and pending postings older than 21 days move there with their complete text and an archive reason. Age is measured from a known observation timestamp; legacy records without one get a grace period. Archival does not mean that a vacancy is closed. Failed sources may cause live jobs to become stale, so review the archive before treating anything as unavailable. The archive is retained and may grow; no historical records or learned boards are silently purged.

`filter_audit` reports evaluation counts and sample titles, not counts of distinct rejected jobs. Generic partner matching excludes HR/People/Talent Acquisition Partner titles; custom role profiles retain their explicit keyword choices. Exclusions must reflect explicit search preferences, not facts from a single application.

Tracker deduplication retains source URLs and vacancy IDs and adds a conservative normalized company/title identity (punctuation, `&` and common gender suffixes). Different titles at the same company remain distinct. When `TRACKER_RANGE` is a bounded, sheet-qualified A1 range, the read extends to the current sheet row count, up to 5,000 rows, so newly added applications are included. Set `TRACKER_AUTO_EXPAND=false` to keep an intentionally fixed range. `tracker_read` records the range and row count used; the tracker is never edited by the collector.

Apps Script quotas and provider access limits apply. The soft deadline cannot cancel in-flight requests. Read-only source/Tracker scopes and app-file output access are included in the manifest; external HTTP requests and trigger management are also required.

## Optional paid scoring — off by default

Scoring.gs and ScoringConfig.gs are supplied for compatibility and synthetic tests; they are not required for collector-only use. If installed, no model calls occur unless AI_SCORING_ENABLED is exactly `true` and private OPENAI_API_KEY/OPENAI_MODEL configuration is valid. Custom SEARCH_PROFILE_JSON disables the inherited paid scorer and reports custom_profile_requires_guided_review, because that scorer's prompt assumes Germany. AI_MAX_JOBS defaults to 3. Enabling scoring for the original defaults sends selected private source text to the configured API and incurs provider charges. Do not enable it merely to follow this guide.

The free guided workflow instead reviews the private report with your assistant and asks you decisive questions. That assistant environment may have its own subscription costs and usage limits.
