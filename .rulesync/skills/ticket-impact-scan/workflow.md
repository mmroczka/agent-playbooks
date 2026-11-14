# Ticket Impact Scan

Find ticket assumptions invalidated by the outgoing diff and post evidence-backed heads-up comments while the change is fresh.

**Advisory, never a gate.** Run once when the implementation is ready for review or merge. Routine review fixes do not require another scan; rescan if they materially change the previously reported impact. Skip diffs that change no assumptions other work relies on, and say why. Use the available Linear integration and the selected workspace policy to establish the intended workspace and team.

## 1. Derive search keys from the diff

Read the outgoing diff and extract changed symbols and modules, DB columns and constraints, API or component contracts, defaults and policies, and unresolved work. Search from what actually changed, including changes beyond the PR's own ticket description.

Identify the PR or branch and its current state. Describe unmerged changes as proposed or conditional on merge; a merged change is not necessarily deployed.

## 2. Shortlist under a budget

Full-read budget: **about 15 tickets**. Search titles broadly and full-read narrowly.

Start with open tickets in the same project, then team-wide searches for the diff's feature nouns, symbol names, table names and policy terms. Include relevant older backlog specs and follow-up tickets from the PR's review. Report any important candidates left unread when the budget is exhausted.

## 3. Check comments before classifying

Read each candidate's comments newest-first alongside its description. A claim already corrected or resolved in the discussion needs no new heads-up. An existing comment covering the same change also needs no duplicate.

A ticket is **affected** only when you can quote a claim the diff invalidates: an assumption, reference, plan step, acceptance criterion, or a required mechanism that changes. Distinguish a future impact on merge from something already stale. Mere topic overlap is insufficient. Record tickets you read that remain accurate in a **checked-unaffected** list, with a one-line reason.

## 4. Post, then report

For each affected ticket, post one comment directly, without a separate approval round-trip. Keep it to six sentences or fewer: link the PR or identify the branch, state its actual review/merge/deployment status, quote the affected claim, and explain the evidenced change and its consequence. Link supporting code or diff evidence where available. Check for an equivalent comment before posting again after a retry.

Report each affected ticket as:

- **Ticket identifier — title (status)** — link to the posted comment
- **Affected claim:** the quoted assumption or plan
- **Change and timing:** what differs, and whether it is proposed, merged or deployed

Follow with the checked-unaffected list and any access or coverage gaps. If posting fails, distinguish unposted findings from confirmed comments; provide the unposted text without claiming success. If the change is later abandoned, report which comments need correction.

## 5. Keep writes to comments

Posting these comments is the only Linear write this skill performs. Propose description, status, label, project, assignee or parent changes in the report for separate action.
