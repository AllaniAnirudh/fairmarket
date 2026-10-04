# FairMarket RFC Process

Substantial changes to the protocol go through public RFCs (Request for Comments). An RFC is a numbered markdown document, proposed as a pull request, reviewed in the open, and decided with recorded rationale.

## When you need an RFC

- A new vertical extension (for example, `healthcare/v1`)
- A change to the core protocol (identity, offers, order lifecycle, fee model, reputation, disputes)
- A change to fee policy or governance
- Any change that would break existing implementations

You do not need an RFC for: typo fixes, clarifications that do not change meaning, new examples, or editorial improvements. Open a regular PR for those.

## Process

1. **Check for duplicates.** Search open and merged RFCs and Discussions first.
2. **Write the RFC.** Copy `rfcs/0000-template.md`. Number it with the next available number. Keep it focused: one proposal per RFC.
3. **Open a PR.** Title it `RFC-NNNN: <short title>`. The PR description should summarize the proposal in a few sentences.
4. **Discussion.** Announce it in GitHub Discussions. The review period is at least 14 days for extensions, 30 days for core protocol or fee policy changes.
5. **Revision.** Address feedback by updating the RFC in the PR. Major redirections should be noted in a changelog section at the bottom of the RFC.
6. **Decision.** Spec stewards approve, request changes, or reject, with written rationale. Approval merges the RFC as `accepted`.
7. **Implementation.** Accepted RFCs are worked into the spec and released under the [versioning policy](VERSIONING.md). The RFC stays in the repo as a permanent decision record.

## RFC states

- `draft` — under discussion
- `accepted` — approved, awaiting spec integration
- `implemented` — integrated into a spec release
- `rejected` — declined, with rationale recorded
- `superseded` — replaced by a newer RFC

## Template sections

Every RFC must include: Summary, Motivation, Proposal (the actual change), Drawbacks, Alternatives considered, Compatibility impact, and Open questions. The template in `rfcs/0000-template.md` has the full structure.
