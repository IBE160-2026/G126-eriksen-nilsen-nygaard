# G126 — IBE160 Programmering med KI

Group project at Høgskolen i Molde, autumn 2026. Members: Nicolas Einrem Eriksen,
Truls Nilsen, Kristoffer Benjamin Nygaard. The repo holds the application plus the
documentation of how it was developed, tested and quality-assured with AI.

The project runs roughly 12 weeks, with hand-in around 5 December 2026, and must
end in a working prototype. Scope decisions should be made against that runway, not
against a short sprint.

We follow the BMAD method (v6.12.0). Planning artifacts go in
`_bmad-output/planning-artifacts/`. Before any product work, read `product-brief.md`
and `addendum.md` at the repo root — they are the agreed foundation and nothing
should contradict them without the group deciding to change them.

## The product: Motvekt

A Norwegian web application that takes a stock the user is already considering —
something they saw on X, heard from a colleague, read in a post — and subjects it to
adversarial analysis by a council of AI agents: an analyst who states only facts, a
bull, a bear, a portfolio agent examining overlap and concentration, and a Norwegian
tax-and-account agent. A translator agent is the only one the user talks to. The user
leaves with a documented rationale and their own recorded decision.

## Hard rules

1. **Never produce a recommendation.** Motvekt analyses; the user decides. No output
   may state or imply that an instrument is suitable for a particular person. This is
   what keeps the product outside the definition of investeringsrådgivning under
   MiFID II, which would otherwise require a licence from Finanstilsynet. It is a
   design constraint enforced throughout the product, not a disclaimer in a footer.
   If asked "so should I buy it?", the system declines and returns the question.

2. **No unsourced numbers.** Every figure shown to a user must be traceable to a
   fetched source, with the source linked. If a number cannot be sourced, the system
   says so rather than inferring or estimating. A hallucinated financial figure is
   worse than no product at all.

3. **Norwegian interface.** All user-facing text is Norwegian. Code, comments,
   identifiers and BMAD documents are English.

4. **Out of scope for v1:** options, cryptocurrency, unlisted instruments, real-time
   pricing, trade execution, broker connections, and any form of payment or
   subscription. See the Scope section of the brief before adding anything.

## Working conventions

- One branch per story once building starts. Do not commit directly to `main`.
  Open a pull request and have a teammate read the diff before it merges.
- Ask before adding a dependency, a paid service, or a data provider. Cost and
  lock-in are group decisions, not implementation details.
- Commit messages in Norwegian match the existing history; either language is fine.

## Working with this team

We are learning to code. Explain what a change does and why, not just what to run.
Assume no prior JavaScript, TypeScript or Python. Show the diff and the reasoning
rather than silently doing more than was asked. Finance domain knowledge is strong —
you do not need to explain what an ETF or a P/E ratio is.

## Open decisions — do not treat these as settled

- **Stack.** Leaning toward all-TypeScript (Next.js plus the Vercel AI SDK for agent
  orchestration) rather than splitting with a Python backend, because nobody on the
  team writes Python. The architecture phase decides this, not the brief.
- **Market data provider**, and what it costs per month.
