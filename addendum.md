# Addendum: Motvekt — Course Rubric Dimensions

Supporting detail for `product-brief.md`. The brief is the product story; this document answers the five dimensions the course uses to describe every project proposal, so each can be found directly. Nothing here contradicts the brief — it expands it.

## Data inn

**From the user.** The claim he arrives with, in one of four shapes: a name he types, a post or passage he pastes, a comparison between two names, or a hold-or-sell question about something he already holds. His existing holdings, entered manually — instrument and either quantity or share of portfolio. His account type (aksjesparekonto, fondskonto, or ordinary custody). The decision text he writes himself at the end of a session.

**From external sources.** Company fundamentals and filed financial statements. Historical price and volatility. Instrument reference data — ISIN, listing venue, currency, and for funds and ETFs their constituent holdings, which is what makes overlap analysis possible. Norwegian tax and account rules, held as a static reference set derived from Skatteetaten's published rules rather than fetched per request.

**Explicitly not taken in.** No bank connection. No broker connection. No transaction history. No national identity number. The product never needs them.

## Data ut

**Per analysis.** A factual company profile with every figure linked to the filing it came from. A bull case and a bear case, presented as competing arguments rather than a blended summary. Overlap and concentration figures showing what proportion of the user's existing holdings already sit in this name. Account and tax implications in Norwegian terms. A plain-language translation of anything technical. And the open question the user has never been asked: what would have to be true for this to work?

**Persisted.** The decision record — buy, wait, or decline, in the user's own words, together with the conditions he states would change his mind — and its history over time.

**Never out.** A recommendation. A statement that anything is suitable for this user. A price target. An order.

## Beslutningspunkter

**The system's decisions.** Resolving an ambiguous input to one specific instrument, and knowing when to ask rather than guess — a theme resolves to a handful of names and the user chooses. What to do when a data source fails or returns nothing: degrade visibly and say so, never infer around the gap. Whether a given number may be stated at all, which is the hard gate — a figure without an attached source is withheld rather than published. How much disagreement between the agents to surface versus reconcile, given that the disagreement is the pedagogical point. And when to refuse outright: options, crypto, unlisted instruments, and every rephrasing of "so should I buy it?"

**The user's decisions.** What he is actually asking, and through which entry point. Which instrument, when a theme resolves to several. Whether to enter his holdings, which determines whether the overlap analysis can say anything real. And finally buy, wait, or decline — together with the conditions under which he would revisit it.

## Sikkerhet/innlogging

An account is required. It is not there to gate the product but because the decision record, which is the artifact that turns his activity into a process, cannot exist without one.

Stored per user: holdings, decisions, and analysis history. That is personal financial data under GDPR — not a special category, but sensitive in practice and treated as such. Hosting is within the EU/EEA. Access is isolated at the row level so an account can read only its own data. Data is encrypted in transit and at rest. The user can export or delete everything on request.

The strongest control available here is what the product never collects: no bank or broker credentials, no account numbers, no identity numbers. A breach cannot leak what was never stored.

Third-party processors are the market-data provider, the LLM provider, and the hosting platform. Prompts sent to the LLM carry instrument names and proportions, not user identity, so an individual's portfolio is not reconstructible from the request stream.

Out for version one, and acknowledged as such: two-factor authentication, role-based access, shared or team accounts, and any sharing between users. Two-factor authentication is the first of these that should arrive.

## Kjøp/salg over nettet

No, in both senses of the question.

The product sells nothing. Version one is free: no subscription, no payment provider, no transaction of any kind. This is deliberate rather than deferred by neglect — the success criteria treat repeat use as the signal that matters, and charging before knowing whether anyone returns would substitute a revenue assumption for the evidence the first version exists to gather. If monetisation follows, it would be a subscription, and integrating a payment provider becomes an architecture decision for version two rather than one taken here.

The product also does not transact on the user's behalf. It places no orders and holds no broker connection. The furthest it goes toward the market is a link to the user's own broker, which he then acts on himself — a boundary that is both a technical reality and the correct product position, given that the entire premise is that the decision remains his.
