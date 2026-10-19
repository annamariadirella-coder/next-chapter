# Start with the CV you already have

You do not need to install the scanner or write an Evidence Bank before starting.

## Your first action

1. Open a new conversation in your AI assistant. Stay in that conversation for the initial workflow.
2. Attach your CV, or paste its text.
3. Copy **only the starter message under “Attach your CV and copy this message” below**, paste it into the same conversation and send it. You do not need to copy every repository file or complete the other templates first.

Expect a brief CV summary and at most three useful questions in the first response. After you confirm the relevant facts, the assistant proposes your search profile and initial Evidence Bank. If it already has enough information, it should not ask questions just to reach three.

Your first useful result is one reviewed role: supported requirements, unresolved questions and a draft CV if you choose to proceed. You do not need to install Google Apps Script to reach that point. If no credible match is found, the assistant should explain the gap instead of filling a shortlist.

GitHub hosts the instructions; your private assistant conversation is where you provide the CV, answer questions and receive the work. A link to this guide does not automatically configure an assistant: the copied message starts the workflow.

Prefer to try fictional data first? Use [the demo](examples/first-application.md). It needs no Google Drive setup, additional account, script installation or real application.

## 1. Open your AI assistant

Use an assistant that can read your CV or pasted career text. Web access is needed for live job research; document export is needed for downloadable CV files. If either is unavailable, the assistant should explain the limitation and offer a pasted-job-description or editable-text workflow instead.

Keep your CV, evidence and tracker in your private conversation or storage. Do not upload them to this public GitHub repository. Check your assistant service's data settings before providing personal documents. Costs and capabilities depend on that service.

## 2. Attach your CV and copy this message

```text
Help me find relevant jobs and prepare truthful, tailored applications.
I have attached my CV (or will paste its text). Start from it; do not ask
me to complete a large template first.

Work through this sequence:
1. Summarise the roles, experience and results already supported by my CV.
   Treat them as draft evidence until I confirm them. Do not invent facts.
2. Ask at most three short questions at a time about missing constraints
   or facts that materially affect targeting. Do not repeat documented facts.
3. Propose a brief search profile and draft Evidence Bank for my review.
4. Once the critical constraints are confirmed, research a small set of
   relevant jobs. Verify the original employer and check my tracker if I
   provide one. If browsing is unavailable, ask me for the JD and URL and
   label availability unverified.
   If I have no tracker yet, mark duplicate checking unavailable; help me
   create a private tracker from the blank template. Do not claim no prior
   application just because you could not check it.
5. Map must-haves and preferences to direct evidence, transferable evidence
   and uncertainties. Ask only questions that could change the application.
6. For a role I choose, prepare a tailored CV and requested application
   answers. Check dates, ownership, unsupported claims, wording and layout.
   Tell me whether you can actually deliver a downloadable file.

I decide and submit. Do not apply, send messages or change private source
records without my authorization. Suggest updates to my Evidence Bank as
a small reviewable change after each important clarification.

My preferred work location / remote base:
My actual working languages:
My target roles (if known):
My compensation or employment constraints (if known):
Companies / roles already applied to (or attached tracker):
```

You may leave unknown preferences blank. The assistant should help you clarify them rather than pretend they are settled. Add [the full instruction](assistant-instruction.md) if you want the detailed guardrails.

## 3. Confirm a small first Evidence Bank

The assistant drafts it from your CV; you confirm facts and scope. Start with relevant career facts, not a complete life history. Use [the blank template](evidence-bank-template.md) to keep future additions consistent.

A statement such as “led automation” should be clarified only when it matters: did you build/configure the workflow, supervise its implementation or lead adoption? All three can be valuable, but they support different applications.

## 4. Choose one role and review the CV

Expect a short explanation of fit, explicit gaps and only decisive questions. No invented percentage or guarantee of an interview. The final CV should tell one coherent story. You review it and send it yourself.

See [a complete fictional example](examples/first-application.md) before using real data.

## Keep your progress between sessions

Save the confirmed Evidence Bank, search preferences and tracker in your own private folder. At the end of a session, ask for the updated evidence text and unresolved questions; review changes before replacing your saved copy. In a new conversation, attach these saved files alongside your CV. Do not assume the assistant remembers previous chats or can access your Drive automatically.

Start a tracker with [the blank CSV](templates/tracker-template.csv): download it and import it into a private Google Sheet, or use it privately as a spreadsheet file. No scanner installation is needed. Add a row after you submit a real application; leave it empty before your first submission. If the assistant cannot read it, paste the relevant company/role rows privately.

## 5. Add the morning scan when you want it

The scanner is optional. It collects opportunities in your private Google Drive; it does not wake your assistant or automatically produce your daily CVs.

Ask your assistant to propose a JSON search profile using [the example](templates/search-profile.example.json), then review the literal role/location terms. Your private Evidence Bank and targeting document remain the detailed career source; this JSON controls the collector's basic filters.

Follow [scanner setup](apps-script/README.md). Run `checkConfiguration` before initialization or a scan. If a check is blocked, use [troubleshooting](TROUBLESHOOTING.md). Then bring the private `candidates.md` report into your assistant and ask:

```text
Review this scan against my confirmed Evidence Bank and search profile.
Check my tracker for duplicates, verify employer availability where possible,
and choose the most relevant roles. Separate source failures from weak fit.
Ask me only decisive questions, then prepare the CV for a role I select.
```

The scanner does not update your tracker automatically. After you submit, record the role and status in your private tracker so future scans can exclude it.
