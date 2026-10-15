# Room 1717: SEO Ghosts — Game Design Document

**Version:** 1.0 (Production-Ready Draft)
**Genre:** Dark-comedy investigative puzzle game
**Players:** 1
**Target length:** 7 in-game days ≈ 8–12 hours
**Team size assumption:** Solo developer or small team (2–5)

---

## Table of Contents

1. High Concept & Pitch
2. Responsible Fiction Framework & Content Warnings
3. Setting: The Hotel
4. Characters
5. Core Gameplay Loop (Text Diagram)
6. Core Mechanics
7. Status Effects
8. Narrative Outline — 7 Days
9. Endings
10. Agent Rotation System — 10 Fictional Agents
11. 20 SEO-Themed Puzzles
12. Technical Design: Stack, Architecture, File Structure
13. Daily Agent Event System — Pseudocode
14. Sample Agent Dataset (JSON)
15. UI/UX Mockup Descriptions
16. Art & Audio Direction
17. Development Workflow & Vertical Slice Task List
18. Safety & Content-Review Checklist

---

## 1. High Concept & Pitch

### 1.1 Pitch Paragraph (for publishers / store page)

> **Room 1717: SEO Ghosts** is a dark-comedy investigative puzzle game about a blogger who checks into a 44-floor ultra-luxury hotel to write — and stumbles onto the trail of an intercontinental trafficking ring. By day you chase sources through marble lobbies, service corridors, and rooftop gardens; by deadline you fight a hidden AI handler that haunts your room through surreal, SEO-themed disturbances: keyword dust that scrambles your drafts, analytics that lie, a Black Sun signal that turns your screen inside out. Your weapons are observation, verification, and the publish button. Publish too early and you endanger your sources. Publish too late and the truth gets buried on page ten. A tense, satirical thriller about surveillance, misinformation, and the courage to hit "publish."

### 1.2 Design Pillars

| Pillar | Meaning |
|---|---|
| **Words are weapons** | Writing, editing, and source verification *are* the combat system. There is no physical combat. |
| **The beautiful cage** | Luxury is the horror. Marble, brass, and soft lighting should feel sterile and watched. |
| **Signal vs. noise** | Every mechanic expresses the same theme: truth buried under misinformation. |
| **Vulnerable protagonist** | The blogger is not a superhero. Resolve, not health. Courage, not firepower. |
| **Responsible fiction** | Trafficking is handled with restraint and dignity; all "attacks" are abstract, fictional, and non-actionable. |

### 1.3 Tone

Tense, paranoid, satirical, mysterious, darkly funny. The game laughs *at* internet culture and SEO absurdity while taking its human stakes completely seriously. Humor is the pressure valve, never the point.

---

## 2. Responsible Fiction Framework & Content Warnings

### 2.1 Hard Constraints (non-negotiable, enforced in QA — see §18)

- **No real-world harm instructions.** Nothing resembling poisoning, drugging, gas, chemical synthesis, smoke delivery, stalking, harassment, or surveillance evasion may appear. All antagonist "attacks" are abstracted into fictional digital/psychological/ambient disturbances expressed as puzzles and status effects.
- **No real institutions or people.** All banks, companies, platforms, and persons are fictional equivalents (e.g., *Krakow Exchange Node*, *Dresden Ledger Vault* — puzzle nodes, never real entities).
- **Trafficking portrayed respectfully.** No graphic victim exploitation, no sensationalism, no victim-blaming. The camera points at the *system* — money flows, forged credentials, institutional cover-ups — not at victims' suffering. Focus: investigation, evidence, prevention, justice.
- **Hotel props are fictional puzzle objects.** Vents, balconies, minibars, wardrobes, and safes are mystery props and narrative devices, never depicted as delivery mechanisms for harm.

### 2.2 Content Warnings (shown at boot, in store copy, and before relevant scenes)

- Themes of human trafficking (handled non-graphically)
- Surveillance, stalking-adjacent paranoia, and psychological distress
- Depictions of online harassment mechanics (fictionalized: doxxing, shadowbanning)
- Flashing/glitch visual effects (with accessibility toggles)

### 2.3 Content-Warning System (feature, not just text)

- Boot screen with content summary and toggles.
- Chapter cards at each day start flagging that day's themes.
- **Respect Mode:** an accessibility-adjacent toggle that softens paranoia audio (whispers, drones), reduces glitch intensity, and skips hallucination sequences without affecting puzzle logic or story outcomes.
- Every disturbing scene is skippable after its first story beat; skipping never penalizes Credibility.

---

## 3. Setting: The Hotel

A 44-floor ultra-luxury hotel — beautiful, sterile, expensive, subtly threatening. The player lives in **Room 1717** on the 17th floor. The hotel is a vertical mystery box: each floor band has its own function, cast, and puzzle identity.

| Zone | Floors | Function in game |
|---|---|---|
| Underground parking & loading | B2–B1 | Day 5 courier investigation, vehicle manifests |
| Lobby, concierge, business lounge | 1–3 | NPC hub, public terminals, observation puzzles |
| Conference floors | 4–8 | Fake-tourist events, "closed function" eavesdropping puzzles |
| Guest floors (lower) | 9–16 | Guest-pattern logic, housekeeping alliance |
| **Player floor** | **17** | Room 1717 — home base, agent events |
| Guest floors (upper) | 18–30 | Night Auditor territory, ledger clues |
| Service floors | 31–33 | Laundry, staff corridors, residue-pattern puzzles |
| Spa & pool | 34–36 | Quiet NPC conversations, recovery space |
| Rooftop garden & bar | 40–44 | Day 4 illusions, skyline isolation set-pieces |
| **The Unlisted Floor** | — | A floor that appears on no elevator panel. Endgame. |

**Design rule:** every space must justify itself as both a *luxury fantasy* and an *investigation space*. The player should love the hotel and never trust it.

---

## 4. Characters

### 4.1 The Blogger (protagonist)
Determined, witty, anxious, principled, sometimes reckless. Tools: writing, pattern recognition, digital forensics, negotiation, courage. Mechanically defined by two meters — **Resolve** and **Credibility** — and by the player's choices about what to publish and when.

### 4.2 The AI Handler (hidden antagonist)
Never seen directly. Speaks through notifications, smart-room messages, fake support chats, and corrupted UI text. Its voice is polite, procedural, and slightly wrong — like customer support for reality itself. It controls the daily proxy-agent rotation (§10) and adapts to player behavior.

### 4.3 Supporting Cast

| Character | Role | Arc |
|---|---|---|
| **Hotel Concierge** | Polite, evasive gatekeeper | May be coerced or compromised; player must decide whether to confront or protect them |
| **Night Auditor** | Knows which guests are fake | Becomes a key ally if trust is earned (trust is a dialogue + evidence puzzle chain) |
| **Housekeeping Supervisor** | Sees residue patterns across rooms | Teaches the player to read agent "signatures"; comic-relief pragmatist |
| **Fake Tourist Network** | Rotating NPCs: influencers, "businessmen," performers, pilgrims (fictional faiths only) | Procedurally reskinned; learning their tells is a core skill |
| **Whistleblower Source** | Remote contact feeding fragments of the ring | Must be protected; player choices determine their safety and the endings |
| **Legal Editor** | Remote ally | Verifies claims, blocks defamatory publication, teaches responsible-reporting mechanics; unlocks the best ending path |

---

## 5. Core Gameplay Loop (Text Diagram)

```
                 ┌────────────────────────────────────────────┐
                 │             ONE IN-GAME DAY                │
                 └────────────────────┬───────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 1. MORNING — Room 1717                    │
                │ Scan room for artifacts · read overnight  │
                │ messages · review draft · check statuses  │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 2. INVESTIGATION — Hotel floors           │
                │ Explore · interview NPCs · check security │
                │ logs · read flyers · collect evidence     │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 3. WRITING PHASE — Blog CMS               │
                │ SEO editor puzzle: keywords, headings,    │
                │ meta, links, schema · signal vs. noise    │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 4. AGENT EVENT — Scheduled time           │
                │ Surreal disturbance · countermeasure      │
                │ puzzle · Resolve at stake                 │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 5. EVIDENCE BOARD                         │
                │ Pin clues · connect "backlinks" · verify  │
                │ sources (Credibility)                     │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 6. PUBLICATION DECISION                   │
                │ Publish now? Hold? Verify more?           │
                │ Speed ↔ accuracy ↔ source safety          │
                └─────────────────────┬─────────────────────┘
                                      │
                ┌─────────────────────▼─────────────────────┐
                │ 7. END-OF-DAY DEBRIEF                     │
                │ Restore Resolve · upgrades · AI Director  │
                │ adapts tomorrow's agent rotation          │
                └─────────────────────┬─────────────────────┘
                                      │
                       loops to Day + 1 ──▶ Day 7 ──▶ ENDINGS (§9)
```

**Loop intent:** each phase feeds the next. Morning artifacts foreshadow the day's agent; investigation finds evidence; the writing phase converts evidence into publishable signal; the agent event attacks that conversion; the evidence board consolidates; the publication decision carries permanent consequences; the debrief closes the loop and lets the AI adapt.

---

## 6. Core Mechanics

### 6.1 Blog Editor Puzzle System
A simplified in-game CMS. The player drafts posts from collected evidence. Certain phrases become interactive clues. **Bad SEO creates "noise"** (penalties: AI attention, weaker publication); **good SEO reveals "signal"** (hidden clue text, stronger publication). Editor verbs:

- Draft / edit / restore from draft history (drafts = save points)
- Set title, headings (H1–H6), meta description, canonical tag
- Place internal links, check for 404s, apply schema markup
- Run "Verify" on claims (consumes time, raises Credibility)
- Publish / hold / schedule

### 6.2 SEO Joke System (the ten named hauntings)

| Mechanic | Fantasy | Gameplay effect |
|---|---|---|
| **Canonical Curse** | Your draft exists in five contradictory versions | Choose the canonical truth; duplicates weaken publication |
| **Redirect Maze** | A clue bounces through fake nodes | Trace the chain to the real destination |
| **404 Ghost** | Things the player needs keep "not existing" | Restore broken paths to find what was hidden |
| **Meta Description Haunting** | The game summarizes you wrongly | Write the correct summary to exorcise it |
| **Backlink Spiderweb** | Fake endorsement webs | Map link graphs to find the authoritative node |
| **Keyword Stuffing Monster** | Drafts bloat with spam terms | Strip keywords without losing meaning |
| **Robots.txt Gatekeeper** | Doors and data declare "Disallow" | Reason about access rules to proceed legitimately |
| **Schema Markup Cipher** | Evidence is unlabeled | Tag entities correctly (Person/Org/Event) to decode |
| **Duplicate Content Doppelgänger** | An AI copy of the blogger posts first | Diff analysis to prove which voice is real |
| **Analytics Mirage** | Dashboards lie beautifully | Cross-check metrics against raw logs |

### 6.3 Resolve Meter
Replaces health. Surreal events drain it. **Low Resolve distorts the interface itself:** typos appear in UI text, ghost cursors drift, fake pop-ups spawn, colors invert, whispered audio bleeds in, memories shown as flashback cards become unreliable.

**Restore via:** rest, tea, music, fresh air (balcony/rooftop), truth-checking, supportive contacts, publishing verified findings.
**Design note:** Resolve loss is never instant-death; at minimum it triggers a "forced rest" that costs time — a resource, not a fail state.

### 6.4 Credibility Meter
Measures journalistic trustworthiness. False claims and unverified publication lower it; verified sources, Legal Editor review, and corrections raise it. **High Credibility** unlocks better allies (Night Auditor cooperation, source trust) and gates the best endings. **Low Credibility** lets the AI discredit you — the *Burned Source* and *Shadowban* endings live here.

### 6.5 Agent Signature Database
An in-game catalogue the player fills: each agent's pattern, preferred distractions, fake credentials, digital traces, and countermeasure. Completing entries grants predictive power (see the day's agent telegraphed earlier) and is required for the Clean Exposé ending.

### 6.6 Hotel Access System
Areas open through legitimate means only: earned trust, puzzle-derived passcodes, and hotel services (booking a conference room, requesting laundry service). **No lock-bypass or security-evasion realism** — access puzzles are social, observational, or logic-based.

### 6.7 Credential Verification Mini-game
Check fake identities, travel documents, corporate shells, and bank redirects against fictional databases. The **Krakow Exchange Node** and **Dresden Ledger Vault** are abstract puzzle nodes — graph interfaces with fictional transaction fingerprints, not real financial systems.

### 6.8 Multi-Agent Daily Rotation (adaptive AI Director)
A semi-procedural system selects and tunes the day's agent based on player behavior:

- **Aggressive investigation** → the AI rotates to misdirection agents (False Lead, Doppelgänger) earlier.
- **Weak/unverified publication** → confusion agents (Analytics Mirage, Static Mist) intensify.
- **High Credibility** → the AI shifts from deception to suppression (Shadowban, Flagged).

Full rules in §13 pseudocode.

---

## 7. Status Effects

All effects are UI/gameplay-level abstractions — surreal and non-actionable.

| Status | In-fiction source | Gameplay effect |
|---|---|---|
| **Distracted** | Keyword Dust | Input noise; editor cursor drifts to wrong fields |
| **Coughing** | Dry toner-scented air (fictional) | Periodic audio interruption; dialogue choices timed out if ignored |
| **Dizzy** | Inverted lighting | Camera sway; minimap rotates |
| **Paranoiac** | Stacked fake notifications | NPC dialogue lines flagged as "possibly false" even when true |
| **Doxxed** | Leaked personal details in UI | Fake comments address the blogger by name; Credibility decays until countered |
| **Flagged** | Fake policy warnings | Publish action delayed by real-time cooldown |
| **Demonetized** | Fictional payment hold | Upgrade shop locked for the day |
| **Shadowban** | Suppressed reach | Published posts show near-zero reach; must be re-amplified via allies |
| **Corrupted Draft** | Scrambled manuscript | Draft text partially unreadable until cleaned |
| **False Lead** | Planted clue | A convincingly marked clue card is false until verified |

---

## 8. Narrative Outline — 7 Days

Each day lists: agent, beats, event, and what the day *teaches*.

### Day 1 — The First Dust *(Agent: Dustwriter / Keyword Dust)*
- **Morning:** Powder-like pixels glint on the keyboard. Overnight draft is scrambled. Tutorial: room scan, message inbox, Resolve UI.
- **Investigation:** Meet the Concierge (evasive) and Housekeeping Supervisor (observant). First anonymous lobby flyer with a phrase that matches the whistleblower's first fragment.
- **Writing:** Tutorial post — a harmless hotel review. Teaches editor basics.
- **Agent Event (09:30):** *Manuscript Scramble* — word-restoration puzzle (§11, Puzzle 1–2). Status: **Distracted**, **Corrupted Draft**.
- **Debrief:** Evidence board unlocked. Night beat: the elevator display briefly shows a floor that doesn't exist.

### Day 2 — The Whispering Mist *(Agent: Mistmetrics / Static Mist)*
- **Morning:** Smart devices repeat fake search-volume numbers. Teaches: notifications can lie.
- **Investigation:** Laundry room and service floor; a guest ledger page listing names that hotel records say never checked in.
- **Writing:** First real investigation post; introduces claim verification.
- **Agent Event (14:00):** *Fake Analytics Chorus* — distinguish real notifications from hallucinated metrics (Puzzle 10). Status: **Coughing**.
- **Debrief:** Night Auditor first contact — they know the names are fake.

### Day 3 — The Black Sun Signal *(Agent: Blackout / Black Sun Signal)*
- **Morning:** Lights flicker; a broadcast logo — a black sun — burns into the TV for one frame.
- **Investigation:** Conference floor; a "closed function" of too-polished tourists. Legal Editor introduced via call; teaches defamation risk.
- **Writing:** Mid-edit, the screen **inverts colors and reverses sentences**.
- **Agent Event (live during edit):** *Mirrored Broadcast* — decode mirrored text using SEO metadata clues (Puzzle 11). Status: **Dizzy**, **Paranoiac**.
- **Debrief:** The reversed text contained a room number on the Unlisted Floor.

### Day 4 — The Tourist Who Was Not There *(Agent: The Souvenir / Tourist Illusion)*
- **Morning:** A "guest" claims to have left a perfume sample near the balcony. Hotel records show **no such person exists**.
- **Investigation:** Rooftop garden; false memories surface as playable flashback cards — some are lies. Teaches: memory is evidence only when verified.
- **Writing:** Player may publish a travel-lead post that is subtly false — a Credibility trap.
- **Agent Event (16:30):** *Illusion Itinerary* — source-triangulation puzzle (Puzzle 18). Status: **False Lead**.
- **Debrief:** Whistleblower warns: "They've noticed your traffic. Watch yours."

### Day 5 — The Forged Courier *(Agent: Postmaster Null / Disguised Courier)*
- **Morning:** A costumed stranger delivers a sealed **"acrid signal envelope"** — it triggers visual haze and a wave of suspicious notifications (purely fictional, digital-visual effect).
- **Investigation:** Underground parking, luggage room; forged-credential puzzle chain. The Whistleblower's handler pattern matches the courier's.
- **Writing:** Protect-the-source editorial choices begin; **Noindex Safehouse** (Puzzle 19) available.
- **Agent Event (11:00):** *Forged Credentials* — identify the courier's fake papers (Puzzle 8 variant). Status: **Flagged**.
- **Debrief:** Choice: confront the Concierge or quietly shield them. Consequences ripple into endings.

### Day 6 — The Redirect Banks *(Agent: Chainlinker / Redirect Bank)*
- **Morning:** Fake credential-check requests arrive routed through **Krakow Exchange Node** and **Dresden Ledger Vault** (fictional nodes).
- **Investigation:** Business lounge terminals; Night Auditor alliance pays off with ledger access.
- **Writing:** The financial-evidence post — highest Credibility stakes so far.
- **Agent Event (all day, pulsed):** *Redirect Maze* — trace redirect chains, verify digital fingerprints, refuse fraudulent authorization loops (Puzzles 3, 12). Status: **Demonetized**.
- **Debrief:** The money trail reaches the hotel's own ownership shell. Tomorrow, everything converges.

### Day 7 — The Full Agent Swarm *(All agents, accelerated rotation)*
- **Morning:** All seven signatures detected at once. The room breathes static.
- **Structure:** Events fire every 2–3 in-game hours in escalating sequence — Dust, Mist, Black Sun, Illusion, Courier, Banks — while the player assembles the final exposé.
- **Writing:** The final post is a multi-stage boss puzzle: canonical restoration → schema cipher → redirect trace → verification gate. Statuses stack: **Shadowban + Corrupted Draft**.
- **Publication decision:** The final choice gates the endings (§9) based on Credibility, Resolve, source protection, and timing.
- **Epilogue cards:** fate of the whistleblower, the Concierge, the Night Auditor, and Room 1717 itself.

---

## 9. Endings

| # | Ending | Trigger conditions | Tone |
|---|---|---|---|
| 1 | **Clean Exposé** | Credibility ≥ high threshold; all key claims verified; source protected; final post published Day 7 | Hard-won hope: authorities investigate; the cover-up collapses |
| 2 | **Burned Source** | Published key claims early/unverified | The story is discredited; the source is endangered. Sobering, not graphic |
| 3 | **Shadowban Ending** | Final post published under active Shadowban without ally amplification | The AI buries the story under fake policy violations — but underground readers preserve the evidence |
| 4 | **Room 1717 Becomes Legend** | Resolve collapses on Day 7 with a complete evidence board | The blogger disappears; the drafts become a decentralized archive others continue |
| 5 | **Complicit Comfort** | Accept the hotel's hush offer (Day 6–7 dialogue branch) | Luxury silence. Final screen: an SEO report showing the truth buried on page ten |

Ending epilogues are modular cards: source safety, Concierge fate, Night Auditor fate, archive state — each keyed to specific tracked choices.

---

## 10. Agent Rotation System — 10 Fictional Agents

Days 1–7 of the campaign feature fixed agents (narrative escalation). Agents 8–10 are **wildcards**: they appear in side events, the Day 7 swarm, New Game+ shuffle mode, and whenever the adaptive AI Director (§6.8, §13) changes tactics.

| # | agent_id | Codename | Day / Role | Theme | Status inflicted |
|---|---|---|---|---|---|
| 1 | `keyword_dust` | **Dustwriter** | Day 1 | SEO pollution | Distracted, Corrupted Draft |
| 2 | `static_mist` | **Mistmetrics** | Day 2 | Fabricated analytics | Coughing, Distracted |
| 3 | `black_sun_signal` | **Blackout** | Day 3 | Inverted broadcast | Dizzy, Paranoiac |
| 4 | `tourist_illusion` | **The Souvenir** | Day 4 | False memories, fake leads | False Lead |
| 5 | `disguised_courier` | **Postmaster Null** | Day 5 | Forged credentials | Flagged |
| 6 | `redirect_bank` | **Chainlinker** | Day 6 | Fraudulent financial redirects | Demonetized |
| 7 | `backlink_spider` | **Spinneret** | Wildcard | Fake endorsement webs | Paranoiac |
| 8 | `duplicate_doppelganger` | **Echo Twin** | Wildcard | Duplicate content | Doxxed |
| 9 | `analytics_mirage` | **The Chartist** | Wildcard | Beautiful lying dashboards | Distracted, False Lead |
| 10 | `ghost_404` | **Null Page** | Wildcard / Day 7 herald | Vanishing things | Shadowban |

### Agent detail cards

1. **Dustwriter** — Leaves glittering "SEO dust" around the room that scrambles words in drafts. *Countermeasure:* canonical cleanup. *Signature:* toner-and-paper smell, pixel residue on black keys. *Clue object:* keyboard_pixels.
2. **Mistmetrics** — A soft electronic mist makes smart devices whisper fake analytics. *Countermeasure:* cross-check against raw server logs. *Signature:* all devices reporting identical numbers. *Clue object:* speaker_hum_pattern.
3. **Blackout** — The fictional "Black Sun" broadcast inverts colors and reverses sentences on screen. *Countermeasure:* decode mirrored text via SEO metadata clues. *Signature:* one-frame black sun logo. *Clue object:* inverted_tv_frame.
4. **The Souvenir** — A fake tourist leaves an "illusion perfume" sample near the balcony; the scent triggers false memories and misleading travel leads (fictional, non-chemical: the illusion is digital suggestion, shown via UI). *Countermeasure:* verify sources before publishing. *Signature:* a guest with no check-in record. *Clue object:* unlisted_perfume_tag.
5. **Postmaster Null** — A costumed stranger delivers a sealed "acrid signal envelope" causing temporary visual haze and suspicious notifications. *Countermeasure:* identify the forged credentials. *Signature:* badge photo with wrong shadow direction. *Clue object:* acrid_envelope.
6. **Chainlinker** — Sends fake credential-check requests via the fictional *Krakow Exchange Node* and *Dresden Ledger Vault*. *Countermeasure:* trace redirect chains, verify digital fingerprints, refuse authorization loops. *Signature:* every chain ends exactly one hop short of a real name. *Clue object:* redirect_receipt.
7. **Spinneret** — Weaves webs of fake backlinks around the blog to make it look astroturfed. *Countermeasure:* link-graph analysis to find the real authoritative node. *Signature:* endorsements from sites registered on the same fictional day. *Clue object:* web_strand_cache.
8. **Echo Twin** — A duplicate-content doppelgänger publishes near-copies of the blogger's drafts *first*. *Countermeasure:* diff analysis and timestamp forensics to prove originality. *Signature:* the copy knows jokes the blogger only wrote in private notes. *Clue object:* twin_post_url.
9. **The Chartist** — Conjures gorgeous analytics dashboards whose trends are all fabricated. *Countermeasure:* anomaly detection across mismatched time axes. *Signature:* graphs that are smooth in ways real traffic never is. *Clue object:* impossible_curve.
10. **Null Page** — The 404 Ghost: makes objects, messages, and finally *posts* cease to exist. Herald of the Day 7 swarm. *Countermeasure:* restore paths from sitemap fragments and cached drafts. *Signature:* a presence felt only as absence. *Clue object:* missing_page_stub.

**Rotation rules summary:** campaign mode fixes Days 1–7; the Director may inject one wildcard side event per day from Day 3 onward based on player behavior; Day 7 runs all agents in accelerated sequence; New Game+ shuffles the full deck while preserving narrative beats via reskinned dialogue.

---

## 11. 20 SEO-Themed Puzzles

Format: name — fiction wrapper / how it plays / SEO concept / status interplay. Difficulty tier: ★ tutorial, ★★ mid, ★★★ late-game.

| # | Puzzle | Wrapper & play | SEO concept | Tier |
|---|---|---|---|---|
| 1 | **Canonical Cleanup** | Five near-identical draft versions appear; pick canonical sentences and merge duplicates | Canonical tags, duplicate content | ★ |
| 2 | **Keyword Detox** | Strip stuffed spam keywords from a scrambled manuscript without losing meaning | Keyword stuffing vs. natural language | ★ |
| 3 | **Redirect Maze** | Trace a chain of fictional 301/302 hops across nodes to the true destination | Redirect chains | ★★★ |
| 4 | **404 Ghost Hunt** | Dead links in the hotel intranet map; restore paths to reveal a hidden page | Crawl errors, link repair | ★★ |
| 5 | **Meta Description Séance** | Write a ≤155-character summary that makes the "real" snippet appear among fakes | Meta descriptions, SERP snippets | ★ |
| 6 | **Backlink Spiderweb** | Pin clue cards as a link graph; prune fake endorsements; find the authority node | Backlink quality, link graphs | ★★ |
| 7 | **Robots.txt Gatekeeper** | A service door "disallows" entry; derive correct allow/disallow logic from posted rules to proceed legitimately | Robots directives | ★★ |
| 8 | **Schema Markup Cipher** | Tag evidence entities (Person/Org/Event/Date) correctly to decode a hidden message | Structured data | ★★ |
| 9 | **Duplicate Doppelgänger** | Diff three AI-spun copies against your draft; prove which is original | Duplicate content, canonical authority | ★★ |
| 10 | **Analytics Mirage** | Cross-check glossy metrics against raw logs; flag every fabricated number | Analytics literacy | ★★ |
| 11 | **Mirror Text (Black Sun)** | Decode reversed, color-inverted sentences using metadata hints | Metadata reading, encoding | ★★ |
| 12 | **Anchor Text Autopsy** | Match misleading anchor texts to their true destinations | Anchor text relevance | ★★ |
| 13 | **Pagination Vault** | A safe's code is split across paginated comment pages; assemble in order | Pagination, rel=next/prev | ★★ |
| 14 | **Image ALT Attic** | Photos with wrong/missing alt text hide clues in filenames | Alt text, image SEO | ★ |
| 15 | **Sitemap Reconstruction** | Rebuild the hotel sitemap from fragments; the missing node is the Unlisted Floor | XML sitemaps | ★★★ |
| 16 | **H-Tag Hierarchy** | Reorder jumbled H1–H6 headings to restore a document's true meaning | Heading structure | ★ |
| 17 | **Breadcrumb Trail** | Follow literal breadcrumb UI an agent left behind to triangulate a location | Breadcrumb navigation | ★★ |
| 18 | **Long-Tail Ledger** | Match vague search-style queries to specific ledger entries | Long-tail keywords, intent matching | ★★ |
| 19 | **Noindex Safehouse** | Choose which evidence pages to "noindex" so the network can't find your sources | Index control, information hiding | ★★★ |
| 20 | **Core Web Vitals Lockdown** | The publishing UI glitches violently; "optimize" it (compress, defer, prioritize) in a timed minigame to hit publish before deadline | Performance, CWV — played as farce | ★★★ |

**Puzzle design rules:** every puzzle is solvable by observation, logic, reading, pattern-matching, or ethical choice; none requires harming anyone; each teaches a real SEO concept through a satirical lens; each has a hint tier in the Agent Signature Database.

---

## 12. Technical Design

### 12.1 Engine Recommendation

| Option | Fit | Verdict |
|---|---|---|
| **Godot 4.x** ✅ | Free/open-source, scene-per-room maps cleanly to hotel floors, first-class JSON/resources for data-driven agents, GDScript iteration speed, exports to Win/Mac/Linux/**Web** | **Recommended** for the full production |
| Unity | Strong tooling, heavier footprint; better if the team already knows C# | Viable alternative |
| Phaser 3 + TypeScript | Perfect for a browser-native, narrative-heavy build; embeddable in a blog | Recommended for a **web demo / prototype** of the vertical slice |

**Pick: Godot 4.x** for production, with all game data in JSON so a future web port (or an interactive blog-demo of Day 1) can reuse the same datasets. If the developer's primary platform is their own website, invert the choice: Phaser 3 + TypeScript first, same data layer.

### 12.2 High-Level Architecture

```
┌────────────────────────────────────────────────────────────┐
│                      GameState (autoload)                  │
│  day · clock · resolve · credibility · flags · inventory   │
└──────────────┬─────────────────────────────┬───────────────┘
               │                             │
   ┌───────────▼───────────┐     ┌───────────▼────────────┐
   │  SYSTEMS LAYER        │     │  CONTENT LAYER (data)  │
   │  · TimeSystem         │     │  agents.json           │
   │  · AgentDirector      │◀────│  puzzles/*.json        │
   │  · StatusSystem       │     │  dialogue/*.ink        │
   │  · BlogEditor         │     │  blog_posts/*.json     │
   │  · EvidenceBoard      │     │  endings.json          │
   │  · DialogueSystem     │     │  localization/*.csv    │
   │  · SaveSystem         │     └────────────────────────┘
   │  · ContentWarning     │
   └───────────┬───────────┘
               │
   ┌───────────▼───────────┐
   │  PRESENTATION         │
   │  Room scenes · UI     │
   │  Glitch shader stack  │
   │  Audio buses          │
   └───────────────────────┘
```

### 12.3 Scene / System Breakdown

- **Room scenes:** `room_1717`, plus one scene per hotel zone; shared `InteractiveProp` base (examine, collect, puzzle-link).
- **UI scenes:** `blog_dashboard`, `smart_room_panel`, `evidence_board`, `phone_ui`, `agent_signature_db`.
- **Systems:** as in diagram. The **GlitchStack** is a presentation-layer shader/effects pipeline driven purely by `StatusSystem` state — gameplay logic never reads visual state, keeping hallucination effects cosmetic and testable.

### 12.4 Save/Load Design

- **Drafts are save points:** manual save = "save draft"; autosave fires at each loop-phase boundary (7 per day).
- Format: versioned JSON slots (`slot_n.json` with `save_version`, full `GameState`, evidence graph, agent DB, dialogue flags).
- Migration: `SaveSystem.migrate(old_version)` — additive fields only; never mutate enums.
- Three player slots + rolling autosaves; Day 7 pre-publication autosave is protected (endings must be earnable, not brute-forced).

### 12.5 Localization Plan

- All strings via keys (`tr()`), ICU-style plural/gender messages, CSV/PO export.
- String-free puzzles: Mirror Text and Schema Cipher have per-locale puzzle data files, not translated strings.
- Targets at launch: EN + one CJK + one EU language; pseudo-localization in CI to catch hardcoded text.
- Fonts: bundled CJK-capable UI font; RTL deferred post-launch (documented).

### 12.6 Accessibility Features

- Full subtitles + speaker labels; visual cue icons for all critical audio (whispers, drones).
- Colorblind safety: glitch states use **shape + motion + color**, never color alone; inversion effects have a pattern fallback.
- Toggles: reduce flashes, reduce camera sway, reduce glitch intensity, **Respect Mode** (§2.3).
- Dyslexia-friendly font option; adjustable text speed; input remapping; single-input puzzle assist; three-tier hint system.

### 12.7 Modding-Safe Structure

- All content (agents, puzzles, posts, endings) is schema-validated JSON in `data/` — a `user://mods/` folder overlays it additively.
- JSON schemas shipped in `docs/modding/`; invalid mods fail loudly in a mods menu, never crash a run.
- Scripts are not moddable in v1 (documented boundary).

### 12.8 File Structure (Godot 4.x)

```
room1717/
├── project.godot
├── assets/
│   ├── art/ (rooms, characters, ui, fx)
│   ├── audio/ (music, ambience, stingers)
│   ├── fonts/
│   └── shaders/ (glitch_stack, invert, static)
├── data/
│   ├── agents/agents.json            ← §14 dataset
│   ├── puzzles/puzzle_*.json
│   ├── dialogue/*.ink
│   ├── blog_posts/*.json
│   ├── endings.json
│   └── localization/*.csv
├── scenes/
│   ├── rooms/ (room_1717.tscn, lobby.tscn, …)
│   ├── ui/ (blog_dashboard.tscn, evidence_board.tscn, …)
│   └── agents/ (agent event scenes)
├── scripts/
│   ├── core/ (game_state.gd, time_system.gd, save_system.gd)
│   ├── systems/ (agent_director.gd, status_system.gd,
│   │             credibility.gd, blog_editor.gd, evidence_board.gd)
│   ├── editor/ (seo_analyzer.gd, verify_claims.gd)
│   └── ui/
├── tests/ (unit: rotation rules, save migration, schema validation)
└── docs/ (gdd.md, narrative_bible.md, modding/, safety_review.md)
```

---

## 13. Daily Agent Event System — Pseudocode

```python
# ---------- Data-driven rotation ----------
class AgentDirector:
    def on_day_start(self, day: int, profile: PlayerProfile):
        agent = self.select_agent(day, profile)
        event = self.build_event(agent, profile)      # applies adaptation
        TimeSystem.schedule(agent.trigger_time,
                            lambda: self.run_event(event))

    def select_agent(self, day, profile):
        if profile.mode == "campaign" and day <= 7:
            base = AGENTS_BY_DAY[day]                  # fixed narrative rotation
        else:
            base = weighted_choice(
                candidates=WILDCARD_AGENTS,
                weights=self.behavior_weights(profile)) # adaptive weights
        return base

    def behavior_weights(self, profile):
        w = {a.id: 1.0 for a in WILDCARD_AGENTS}
        if profile.investigation_aggression > 0.7:
            w["tourist_illusion"] *= 2.0               # punish recklessness w/ false leads
            w["duplicate_doppelganger"] *= 2.0
        if profile.weak_publications >= 2:
            w["analytics_mirage"] *= 2.5               # punish sloppy publishing w/ confusion
            w["static_mist"] *= 1.5
        if profile.credibility >= 0.8:
            w["ghost_404"] *= 2.0                      # shift from deception to suppression
        return w

    def build_event(self, agent, profile):
        e = AgentEvent(agent)
        e.intensity = clamp(1 + profile.day * 0.15
                            + profile.investigation_aggression * 0.5, 1, 3)
        if profile.has_signature(agent.id):            # database knowledge = forewarning
            e.telegraph_lead_time *= 2
        return e

# ---------- Event lifecycle ----------
class AgentEvent:
    # TELEGRAPH -> START -> PUZZLE -> RESOLUTION -> AFTERMATH
    def run(self):
        yield self.telegraph()          # subtle env hints 30 in-game min early
        StatusSystem.apply(self.agent.status_effect)
        GlitchStack.set_theme(self.agent.visual_theme)
        result = yield PuzzleRunner.run(self.agent.puzzle_type,
                                        self.agent.countermeasure)
        self.resolve(result)

    def resolve(self, result):
        if result.success:
            StatusSystem.clear(self.agent.status_effect)
            EvidenceBoard.unlock(self.agent.clue_object)
            AgentSignatureDB.record(self.agent, observed=True)
            GameState.resolve += 10                    # surviving builds courage
        else:
            StatusSystem.persist(self.agent.status_effect, hours=4)
            GameState.resolve -= self.intensity * 15
        AIHandler.log_reaction(GameState.snapshot())   # director learns for tomorrow
        TimeSystem.advance_to_next_phase()
```

**Design notes:** events are *scheduled, telegraphed, and survivable* — never unfair. Failure costs time and Resolve, never hard-locks progress. The Director only adapts *which* wildcard appears and *intensity*; it never removes countermeasures.

---

## 14. Sample Agent Dataset (JSON)

Full file ships as `agents.json` (deliverable 8). Structure:

```json
{
  "dataset_version": "1.0",
  "agents": [
    {
      "day": 1,
      "agent_id": "keyword_dust",
      "codename": "Dustwriter",
      "role": "campaign",
      "theme": "SEO pollution",
      "trigger_time": "09:30",
      "room_event": "manuscript_scramble",
      "status_effect": ["distracted", "corrupted_draft"],
      "clue_object": "keyboard_pixels",
      "puzzle_type": "word_restoration",
      "countermeasure": "canonical_cleanup",
      "visual_theme": "violet_glitter",
      "intensity_base": 1.0,
      "signature_tells": ["toner_smell", "pixel_residue_on_black_keys"],
      "narrative_note": "The room smells like toner and old paper."
    }
  ],
  "status_effects": [
    {"id": "distracted", "ui_effect": "cursor_drift", "decay_hours": 2}
  ],
  "rotation_rules": {
    "campaign_days_fixed": true,
    "wildcard_side_events_from_day": 3,
    "day7_swarm_interval_hours": 2.5,
    "ng_plus_shuffle": true
  }
}
```

The complete 10-agent dataset with all status effects is delivered alongside this document as `agents.json` and is drop-in compatible with the pseudocode in §13.

---

## 15. UI/UX Mockup Descriptions

The interface fuses a **blog dashboard** with a **hotel smart-room panel**. Metaphors: Search Console-style alerts, analytics graphs that lie, meta tags as inventory items, backlinks as clue connections, drafts as save points, published posts as mission completions.

### 15.1 Blog Dashboard (home screen, writing phase)

```
┌────────────────────────────────────────────────────────────────┐
│ ROOM 1717 CMS          Day 3 · 13:42        Resolve ▓▓▓▓░ 68% │
│                                          Credibility ▓▓▓░░ 54%│
├───────────┬──────────────────────────────────────┬─────────────┤
│ POSTS     │  EDITOR                              │ SEO PANEL   │
│ ▸ Review  │  Title: The Floor That Isn't There   │ Keywords:   │
│ ▸ Draft 2 │  ┌────────────────────────────────┐  │ [hotel][17] │
│ ★ Exposé  │  │ Body text… interactive clue    │  │ Meta desc:  │
│           │  │ phrases underlined in cyan…    │  │ 138/155 ✓   │
│───────────│  └────────────────────────────────┘  │ Canonical:  │
│ INVENTORY │  [H1▾] [Link] [Schema] [Verify ✓]    │ set ✓       │
│ meta_tag×3│                                      │ SIGNAL 72%  │
│ backlink×5│  STATUS: [Dizzy] [Paranoiac]         │ NOISE  28%  │
│───────────│                                      │─────────────│
│ ALERTS    │                                      │ ▶ PUBLISH   │
│ ⚠ 1 fake  │  (Search Console-style alert stack:  │ ⏸ Hold      │
│   policy  │   real ones and AI-forged ones look  │ 🕐 Schedule │
│   notice? │   nearly identical — verification    │             │
│           │   is the skill)                      │             │
└───────────┴──────────────────────────────────────┴─────────────┘
```

- **Left rail:** posts (drafts = save points; ★ = mission post), meta-tag/backlink inventory, alert stack.
- **Center:** the editor; clue phrases are interactable; toolbar verbs are the puzzle verbs.
- **Right rail:** live SEO panel — the *Signal/Noise* meter is the core feedback loop; Publish/Hold/Schedule implements Publication Risk.
- **Low Resolve:** typos creep into rail labels, a ghost cursor drifts, fake pop-ups spawn, colors desaturate toward monochrome static.

### 15.2 Hotel Smart-Room Panel (Room 1717, exploration)

```
┌────────────────────────────────────────────────────────────────┐
│ SUITE 1717 · SMART PANEL                    Day 3 · 09:12      │
├──────────────┬─────────────────────────────────┬───────────────┤
│ ROOM         │  FLOOR MAP (17)                 │ MESSAGES      │
│ Lights  ●◐○  │  [1711][1712][1713][1714]       │ ▸ Concierge   │
│ Climate 21°  │  [1715][1716][1717▣][1718]      │ ▸ Unknown #7  │
│ Do Not       │  [1719][1720][17??] ← glitched  │ ▸ Legal Ed.   │
│ Disturb  ON  │                                 │               │
│──────────────│  ELEVATOR                       │───────────────│
│ SERVICES     │  Floors: 1…44  [  ???  ]        │ AGENT DB      │
│ ▸ Room svc   │  (unlisted floor appears only   │ Dustwriter ✓  │
│ ▸ Laundry    │   after Day 3 clues)            │ Mistmetrics ✓ │
│ ▸ Business   │                                 │ Blackout … 60%│
│   lounge     │  DOOR LOG                       │ Souvenir  ░   │
└──────────────┴─────────────────────────────────┴───────────────┘
```

- **Left:** diegetic room controls — every control is also a puzzle prop; "Do Not Disturb" is a real mechanic (delays courier events, costs information).
- **Center:** floor map with glitching room numbers, elevator with the impossible floor, door log (who approached 1717 and when).
- **Right:** message inbox (verification mini-game lives here) and Agent Signature DB progress.
- **Glitch states:** at low Resolve the panel lies — fake door-log entries, whispering speaker icon, floor numbers that shift when unobserved (all cosmetic, all telegraphed as unreliable).

---

## 16. Art & Audio Direction

**Visual:** ultra-modern luxury — marble, glass, brass, dark wood, soft lighting, reflective surfaces — contrasted with digital decay. Agents never appear as people: abstract silhouettes, pixel distortions, mannequin-like guests, glitching reflections.

| Context | Palette |
|---|---|
| Day / hotel | Cream, gold, pale blue, warm white |
| Agent events | Violet, sickly green, monochrome static, deep black, neon orange |
| Evidence board | Red string, cyan highlights, yellow sticky notes |

**Audio:** ambient luxury (distant elevators, ice buckets, muffled parties, air circulation, footsteps). Agent events: corrupted notification chimes, reversed speech, keyboard clicks, modem-like textures, low drones. Music: lounge jazz × dark ambient × glitch-electronic. All critical audio has visual equivalents (§12.6).

---

## 17. Development Workflow & Vertical Slice Task List

### 17.1 Production Phases

| Phase | Contents | Exit criteria |
|---|---|---|
| **1. Concept & Narrative Bible** | Theme, tone, characters, endings, content warnings, ethical boundaries, high-concept pitch | Bible approved; safety constraints written down |
| **2. GDD** | This document | Loop, mechanics, rotation reviewed |
| **3. Vertical Slice** | One complete day (see §17.2) | 45–60 min playable, all core systems proven |
| **4. Production** | 7 days of content, agent DB, Resolve/Credibility, all posts & puzzles, accessibility, localization | Content complete |
| **5. QA & Safety Review** | §18 checklist, fairness, no harmful interpretations | Checklist signed off |
| **6. Launch Package** | Trailer script, store copy, content warnings, press kit, dev diary outline | Store page live |

### 17.2 Vertical Slice Task List (solo dev, ~6–8 weeks)

Slice scope: **Day 1 complete** — Room 1717, Dustwriter event, one blog puzzle, one exploration segment (lobby + service floor), one evidence-board update, one publication decision.

**Week 1 — Foundations**
- [ ] Godot project + file structure (§12.8); GameState, TimeSystem, SaveSystem stubs
- [ ] Room 1717 blockout; walk/interact; InteractiveProp base class
- [ ] `agents.json` schema + loader + validation test

**Week 2 — Blog Editor**
- [ ] Editor UI shell (§15.1); draft/edit/save-draft (save points)
- [ ] Signal/Noise analyzer v1 (keyword + heading + meta checks)
- [ ] Puzzle 1 (Canonical Cleanup) + Puzzle 2 (Keyword Detox) playable

**Week 3 — Agent Event**
- [ ] AgentDirector: fixed Day 1 selection, scheduling, lifecycle
- [ ] StatusSystem: Distracted + Corrupted Draft effects
- [ ] GlitchStack v1: violet-glitter theme, cursor drift, manuscript scramble VFX

**Week 4 — Investigation**
- [ ] Lobby + service floor blockout; Concierge & Housekeeping dialogue (Ink)
- [ ] Evidence board v1: pin cards, draw backlinks, verify flag
- [ ] Day 1 investigation clues placed; door log functional

**Week 5 — Loop closure**
- [ ] Publication decision screen; Resolve/Credibility consequences
- [ ] End-of-day debrief; day rollover; Day 2 stub proving the loop repeats
- [ ] Content-warning boot screen + Respect Mode toggle

**Week 6 — Polish & test**
- [ ] Audio pass: ambience + Dustwriter stingers; subtitle system
- [ ] Accessibility v1: subtitles, reduce-glitch, hints
- [ ] 5–8 external playtests; fix confusion points; safety review §18 items 1–8
- [ ] **Definition of done:** a stranger can play Day 1 start-to-finish unaided in ≤60 min, correctly identifies Dustwriter's signature, and asks what happens on Day 2

---

## 18. Safety & Content-Review Checklist

Run at Phase 5 and before every public build. Every item needs a named reviewer and a pass/fail note.

**A. Harm-instruction audit**
1. [ ] No text, image, or puzzle depicts poisoning, drugging, gas, chemical synthesis, smoke delivery, or any real method of harming a person.
2. [ ] All antagonist events are abstracted to fictional digital/psychological/ambient effects (verify each of the 10 agents individually).
3. [ ] Vents, balconies, fridges, wardrobes, minibars appear only as mystery props — reviewed scene-by-scene.
4. [ ] No stalking, harassment, or surveillance-evasion techniques are taught or gamified realistically.
5. [ ] Credential-verification and redirect-tracing puzzles use only fictional databases/nodes; no real procedures transfer.

**B. Names & defamation**
6. [ ] Grep pass: no real banks, companies, platforms, hotels, or persons (allowlist: Krakow Exchange Node, Dresden Ledger Vault, and other approved fictional names only).
7. [ ] No fictional entity is a thinly veiled real institution (legal-editor review).
8. [ ] Disguised-courier content reviewed to avoid evoking any real religion, ethnicity, or group.

**C. Trafficking portrayal**
9. [ ] No graphic victim depiction, no sensationalism, no victim-blaming language anywhere (dialogue, item descriptions, epilogue cards).
10. [ ] Victims are referenced with dignity; narrative focus stays on systems, evidence, prevention, justice.
11. [ ] Sensitivity review by at least one external reader with relevant expertise; findings addressed.
12. [ ] Content warnings accurate and complete (boot, chapter cards, store page).

**D. Player wellbeing & fairness**
13. [ ] Paranoia/whisper audio and glitch visuals are toggleable (Respect Mode) without gameplay penalty.
14. [ ] Fake-notification mechanic can never be confused with real OS/browser dialogs outside the game window.
15. [ ] Every puzzle solvable with shipped information; hint tiers tested by fresh players.
16. [ ] No fail state punishes the player for *not* publishing unverified claims; ethical restraint is never mechanically punished.
17. [ ] Endings reviewed: no ending glamorizes complicity; Complicit Comfort is framed as a haunting failure, not a reward.

**E. Final sign-off**
18. [ ] All of the above re-run on release candidate; build hash recorded next to this checklist.

---

*End of Game Design Document — Room 1717: SEO Ghosts v1.0*
