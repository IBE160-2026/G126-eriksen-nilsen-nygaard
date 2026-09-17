# Product Brief: Motvekt — Rigorous Analysis for the Pop-Finance Investor

## Executive Summary

Motvekt is a Norwegian web application that takes the stock tip a person already has in their head and puts it through the analysis they never learned to do. The user arrives holding a name — something from X, a colleague, a podcast — and instead of a verdict, receives a council of AI agents that argues about it in front of them. An analyst establishes what the company factually is. A bull constructs the strongest honest case for the position. A bear argues the base rates and what usually happens to stories shaped like this one. A portfolio agent asks the question nobody has asked him before: how much of this do you already own? A Norwegian tax agent explains what the position does inside an aksjesparekonto versus a fondskonto. The user leaves with a documented rationale and a decision that is unambiguously their own.

The person this serves is not a beginner. He has read *The Psychology of Money*, follows the market on X, knows what an IPO is, and can discuss Snowflake and Datadog without hesitation. What he lacks is the technical layer that a formal finance education would have given him — and, decisively, the time and energy to acquire it after a full working day. He knows his process is unserious. He cannot fix it in evenings. So he invests anyway, on instinct, and quietly knows it.

Two developments make this buildable now. LLM agents can conduct genuine adversarial analysis rather than summary — a structured disagreement, which is the format real investment committees actually use, and a format no consumer product currently offers. And the regulatory boundary, which at first looks like an obstacle, resolves into the correct product decision: because Motvekt never issues a personal recommendation, it requires no licence from Finanstilsynet and can launch immediately. That constraint improves the product. This user does not suffer from a shortage of recommendations. He receives a hundred a day. He suffers from a total absence of judgement with which to evaluate them.

## The Problem

There is a large and growing class of investor who is neither novice nor competent. By the standards of the general public he is well-informed. By the standards of anyone who has studied finance formally, he is operating without instruments.

The gap is specific and diagnosable. He has heard of calls and puts and does not understand how they work. He cannot assess whether a valuation is stretched, because nobody has shown him mechanically what "priced in" means. He cannot distinguish a thesis from a narrative. He has no sense of whether a position is large relative to everything else he holds, because he has never thought of his holdings as a portfolio at all. He does not know that his global index fund already makes him a meaningful Nvidia shareholder, and that adding the individual stock concentrates a bet he has already placed.

What makes this durable rather than a passing phase is time. He works nine to five. The knowledge that would close the gap — corporate finance, valuation, portfolio theory — is not available in the ninety minutes he has left on a Tuesday, and he correctly perceives that it isn't. Because the path looks impassable, he never sets foot on it. He is left in a stable and uncomfortable equilibrium: aware that his process lacks rigour, unable to see a route to fixing it, and investing regardless, because the money is there and the market is moving without him.

His coping strategies are all poor and all rational given his constraints. He follows commentators who sound confident, because confidence is the only signal he can evaluate. He buys the names he has encountered most often, mistaking familiarity for research. He holds index funds as a private alibi while making concentrated bets alongside them. He writes nothing down, which means that years later he still cannot distinguish a good decision from a lucky one. The cost is partly financial. The larger cost is that a decade of investing produces no learning whatsoever, because no claim was ever recorded in a form that could later be checked against reality.

No existing product meets him. Brokers — Nordnet, Kron, Saxo — are execution surfaces; they will sell him anything and explain nothing. Education products demand precisely the resource he lacks and address a generic student rather than the specific decision in front of him this evening. Licensed advisors are priced for considerably larger portfolios. Social media, which is where he actually goes, is optimised for engagement rather than accuracy, and rewards exactly the confidence that misleads him. He falls through every gap.

## The Solution

Motvekt begins where the user actually begins: with a claim somebody else made.

He types a name he keeps hearing. Or he pastes the post he just read. Or he asks which of two names is the better bet, or whether to sell something he already holds, or what to make of a sweeping statement like "the AI trade is over." Whatever shape the thought arrives in, the system's first move is to resolve it into one specific instrument — a theme becomes the handful of names it actually refers to, and he picks one. The unit of analysis is always a single holding, because that is the unit in which he will eventually place an order.

Then he does not receive an answer. He receives a room.

The **analyst** establishes what is factually true — what the company does, how it earns money, what the financial statements say — with every figure traceable to the filing it came from, and with no opinion attached. The **bull** then builds the most persuasive honest case for the position, and the **bear** answers it with base rates and structural counterarguments. The **portfolio agent** sets the position against what the user already holds and surfaces overlap, concentration, and the size of the bet as a proportion of everything. The **tax and account agent** translates the whole thing into Norwegian reality: which account type this belongs in, what it costs him, what skjermingsfradrag does here. A **translator** is the only agent the user speaks to directly, converting jargon into plain Norwegian and asking the questions he has never been prompted with — most importantly, *what would have to be true for this to work?*

The disagreement is the product, not a side effect. Pop-finance culture's central falsehood is that competent people agree and that the confident voice is the informed one. Watching five rigorous perspectives fail to converge teaches him more about markets than any single correct answer could, and it teaches it in ninety seconds rather than a semester.

He then records a decision — buy, wait, or decline — in his own words, along with what would change his mind. This is the artifact that converts activity into a process. Months later he can return to it and discover whether he was right for the reasons he thought he was right, which is the thing his current approach structurally cannot give him.

Motvekt never tells him what to buy. This is a design principle enforced throughout the product, not a disclaimer appended to it. The system analyses; the user decides. Everything downstream of that line — the honest bear case, the refusal to answer "so should I buy it", the insistence that he write his own rationale — follows from it, and each of those is better for him than the alternative would have been.

Motvekt is a web application, deliberately not a native mobile app: the moment of need arrives while the user is reading something on a phone or a laptop, distribution is a link rather than a download, and an app-store review cycle would sit badly with a product that needs to change quickly while it is being tested. It is responsive down to phone width. Architecturally it separates a browser-facing interface from an agent orchestration service that runs the council, calls market-data sources, and enforces the rule that no figure reaches the user without a source attached. Specific frameworks, languages and providers are decisions for the architecture phase and are not fixed here.

## What Makes This Different

**It meets the user at the ticker, not at a curriculum.** Every education product asks him to start at lesson one. Motvekt starts at the decision already in his head this evening, which is the only moment he is actually motivated.

**Disagreement is the interface.** Competing products deliver a single synthesised answer, which teaches him to trust an oracle — the precise habit that got him here. A council that visibly fails to agree teaches him to hold a position provisionally.

**The Norwegian layer.** ASK versus fondskonto, skjermingsfradrag, currency exposure for a Norwegian holding US equities: these are the things Norwegian retail investors most reliably get wrong, the rules are public and citable, and no international competitor will ever build them. This is the most defensible part of the product.

**The regulatory posture is a feature.** Staying outside the definition of investeringsrådgivning means no licence, immediate launch, and — more importantly — a product that builds the user's judgement rather than substituting for it.

Honesty requires stating what is *not* a moat. Agent orchestration is commodity technology and will be more so in a year. There is no proprietary model, no exclusive data, and nothing here that a funded competitor could not replicate in a quarter. The advantage is the combination — adversarial structure, Norwegian specificity, and a clear position on what the product refuses to do — held only for as long as it takes someone else to assemble the same three things.

## Who This Serves

**The primary user** is a Norwegian professional between roughly 25 and 45, in salaried employment, financially literate in the popular sense and technically unqualified in the formal one. He invests already. He has a broker account and probably an index fund. He needs to stop making decisions he cannot defend, and he needs this to cost him minutes rather than semesters. Success for him is that he can articulate why he holds what he holds, and that six months later he can check whether that reasoning survived contact with events.

**Secondarily**, the same person at the earlier moment — money accumulated, no position yet, paralysed by the sense that starting badly is worse than not starting. And the partner or friend he talks to about money, who is one step further back still.

Motvekt is explicitly not for active traders, professional investors, or anyone seeking a recommendation. Those users will find it obstinate, which is correct.

## Success Criteria

**Functional.** A user can submit a name and receive a complete council analysis in which every numeric claim links to its source. The tax agent correctly classifies account treatment for all instrument types in scope. A decision can be recorded, retrieved, and revisited.

**Technical.** Zero unsourced numeric claims reaching the user, audited across a sample of 100 analyses — this is a hard gate, because a hallucinated financial figure is worse than no product at all. Analysis completes within 90 seconds. The system degrades gracefully and visibly when a data source fails rather than inventing around it.

**User outcome.** 60% or more of completed analyses end in a recorded decision, where declining to buy counts fully as success. Users can state, unprompted, what would have to be true for their thesis to hold. A measurable share discover portfolio overlap they were unaware of.

**Business.** 100 registered users within the first month after launch, and 20% of them returning within 30 days for a second analysis. Repeat use is the metric that carries the weight here: a tool consulted once was entertainment, a tool consulted twice is becoming a process. Version one is free and sells nothing — monetisation is deliberately deferred until there is evidence that people come back, rather than assumed into the plan. These targets are set low enough to detect genuine demand instead of flattering the project.

## Scope

**In for the first version.** Accounts with stored holdings and decision history. That stored material is personal financial data under GDPR: it is held on EU infrastructure, visible only to the account that entered it, exportable and deletable on request, never shared between users and never sold. An account is required, because the decision record — the artifact that turns activity into a process — cannot exist without one. Four entry points feeding one analysis engine — a name he types, a claim or post he pastes, a comparison between two names, and a hold-or-sell question about something he already owns — each resolved to a single listed equity or ETF before analysis begins. The five-agent council with a translator interface. Source-linked figures throughout. Manual entry of existing holdings for overlap and concentration analysis. The Norwegian tax and account layer. Decision recording and history. Norwegian language throughout. Responsive layout from phone width upward, since the thought that starts a session usually arrives on a phone.

**Explicitly out.** Options analysis, despite the user's stated confusion about calls and puts — the failure mode is too severe for a first version. Cryptocurrency. Any commerce whatsoever: version one is free, with no subscription, no payment provider and no transaction of any kind. Automated broker connections or trade execution — the furthest the product goes toward the market is a link to the user's own broker, which he then acts on himself. Real-time pricing. The "I have money and no plan" guided flow and the full Investment Policy Statement it produces — deferred not only for build cost, but because serving that user well requires eliciting goals, horizon and risk tolerance, and that is precisely the personal-circumstances data that pulls a product across the line into regulated advice. Backtesting, alerts, screening, and social features. A native mobile application. English or any non-Norwegian market.

The scope test applied throughout: if removing an item still allows the core claim to be tested — that rigorous adversarial analysis changes how this user decides — it does not belong in version one.

## Vision

The near-term ambition is to become the thing a Norwegian reaches for in the moment between hearing a stock tip and acting on it.

Beyond that, the decision record is the more interesting asset. An investor who has used Motvekt for two years possesses something almost nobody has: a written record of what they believed, why, and what subsequently happened. That archive is the mechanism by which investing finally becomes a practice that improves rather than a sequence of disconnected bets. A product that shows a user their own reasoning against reality over years is teaching them something no course can.

The council pattern generalises beyond single stocks. The same structure — adversarial perspectives, Norwegian specificity, a refusal to decide on the user's behalf — applies to fund selection, to the pension choices most Norwegians make once and never revisit, and to the largest financial decision most of them will ever take, which is property. In two to three years the ambition is a single Norwegian platform where consequential financial decisions are argued properly before they are made, having started with the smallest and most frequent of them.
