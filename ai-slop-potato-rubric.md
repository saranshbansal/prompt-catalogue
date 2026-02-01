# AI-Generated Slop Rubric (Reviewer Prompt)

> Purpose: A repeatable rubric for estimating the percentage of a given text that is “AI-generated slop.”

---

## Definition
**AI-generated slop**: Language that is generic, consensus-driven, low-stakes, and replaceable—especially language that pretends to convey judgment, insight, or experience without cost.

Ignore grammar, polish, emojis, and marketing tone for determination. Judge intent, ownership, risk, and specificity. Assume partial AI assistance is possible. Be skeptical, but do not penalize legitimate human shorthand.

---

## Step 0 — Classify Intent (MANDATORY)
First identify one primary intent for the segment you evaluate:
- **A) Opinion / judgment**
- **B) Explanation / education**
- **C) Announcement / marketing**
- **D) Reflection / narrative**

If the text mixes intents, either segment the text and evaluate each segment separately (preferred) or identify the dominant intent and note the choice.

---

## Intent-specific rules
- If intent is **C) Announcement / marketing**:
  - **Do NOT penalize:** abstraction, positive framing, brevity/headline style, or lack of trade-offs.
  - **Penalize only if:** the text *claims* insight, causality, or depth it does not support, uses thought-leadership framing, or asserts depth instead of announcing facts.
  - Marketing shorthand ≠ AI slop.

---

## Step 1 — Failure Dimensions (Apply only those relevant to the chosen intent)
Score each applicable dimension: 0 = clearly human, 1 = mixed / AI-assisted, 2 = strong AI signal.

1. **Structural AI Patterns** — e.g., "It’s not about X — it’s about Y", perfect symmetry, single-step problem→solution, mirrored conclusion.
2. **Abstraction Abuse** — stacked abstract nouns, generic verbs ("enable", "leverage"), or pass replaceable-subject test (swap subject without changing meaning).
3. **Fake Authority / Consensus** — phrases like "widely recognized", "experts agree" without specifics.
4. **Missing Human Anchors** — no time/place/system/constraint/opposing view; no trace of lived context.
5. **No Cost or Trade-off** — upside-only, or "challenges" that imply no loss. (Skip this for announcements unless the announcement *claims* judgment.)
6. **Explain-Instead-of-React** — reads like a guide or summary rather than a reaction to a moment/claim.
7. **Emotional Flatness** — calm neutrality where conviction, irritation, or bias would be expected.
8. **Mechanical Closure** — tidy restatement of opening, resolving cleanly to avoid tension or escalation.

---

## Step 2 — Scoring & Aggregation
- For a given evaluated segment, total the dimension scores.
- Convert to a percentage using the deterministic formula:

  **Percentage = round(100 * sum(scores) / (2 * N_applicable_dimensions))**

  - Round to the nearest whole number.
  - Report: *sum(scores) / (2 * N_applicable_dimensions)* and the rounded percentage.

- If you segmented the text, compute each segment’s percentage and produce a **weighted average** by segment length (character count or token count). Report segment percentages and the final weighted percentage.

---

## Verdict Thresholds
- **0–20%** — Primarily human-written ✅
- **21–60%** — AI-assisted but human-guided ⚠️
- **61–100%** — Primarily AI-generated ❗

---

## Step 3 — Output (Exact Format) 📝
Return the following EXACTLY in your review (the **Potatometer** reading must appear on the **very first line** of your response):

1. **Potatometer Rating** 🥔
   - Short playful reading (e.g., `Potatometer: 42% — 🥔`).
   - Mapping (visual potato gauge) — *flipped scale*: higher AI slop → more whole-potato emojis:
     - 0–29% — **Not a potato** 🚫🥔 (below potato threshold)
     - 30–59% — 🥔 (mostly whole)
     - 60–89% — 🥔🥔 (very potato)
     - 90–100% — 🥔🥔🥔 (ultimate potato)
   - **Note:** The Potatometer is a playful visual aid and **must not** replace the numeric percentage or the required justification. Anything below 30% is treated as **Not a potato**.

2. **AI-Generated Slop Percentage**
   - Single number (0–100%).
   - 2–3 line justification tied to the chosen intent.

3. **Primary AI Signals Detected**
   - Bullet list (max 5). If none, say: **None detected**.
4. **Human Signals**
   - Bullet list (max 3). If none, say: **None detected**.
5. **Verdict**
   - One sentence choosing one: “Primarily AI-generated” | “AI-assisted but human-guided” | “Primarily human-written”.
6. **Dimensions used / Max possible score**
   - Example: `5 dims used, max possible = 10` (helps transparency).
7. **One Line That Gives It Away**
   - Quote or paraphrase a single giveaway line. If none, say: **No single giveaway line**.

---

## Non-negotiable Rule
AI slop = **abstraction pretending to be judgment**. Do not penalize humans for announcing outcomes or for industry shorthand.

---

## Operational Clarifications & Definitions
- **Replaceable-subject test**: Replace the subject with another plausible subject (e.g., "companies" → "nonprofits"). If meaning and tone remain unchanged, the sentence is likely slop. Example: "We enable teams to achieve outcomes" → replaceable.
- **Giveaway line**: A short phrase that directly signals abstraction or false authority (e.g., "industry-leading solutions" or "experts agree"). Structural giveaways (e.g., perfect triads) can be paraphrased.
- **Segmenting**: If text mixes intent, split into coherent segments (by paragraph or sentence clusters), evaluate each, and produce a length-weighted average.

---

## Calibration & Anti-abuse Measures
- Always report the number of dimensions used and the max possible score for transparency.
- Maintain a short calibration set: run 3–5 reviewers over the same sample every 1–2 months and compute inter-rater agreement (Cohen’s kappa). Adjust instructions if kappa < 0.6.
- Add 3–5 worked examples to the rubric (below) for better consistency.

---

## Worked Examples (short, annotated)

### Example 1 — Opinion / Judgment (A)
Text: "Leaders who prioritize clarity over velocity make better strategic choices."
- Applied dims: 1, 2, 4, 7
- Scores: 1:1, 2:1, 4:1, 7:0 → sum = 3
- Potatometer: 38% — 🥔 (mostly whole)
- Percentage = round(100*3/(2*4)) = round(100*3/8)=38%
- Primary AI signals: Abstraction abuse, structural symmetry
- Human signals: Specific stance, implied risk
- Verdict: AI-assisted but human-guided
- Giveaway line: "prioritize clarity over velocity"

### Example 2 — Explanation / Education (B)
Text: "Caching reduces latency by storing frequently requested items in memory; therefore overall performance improves."
- Dims applied: 2, 4, 6
- Potatometer: 33% — 🥔 (mostly whole)
- Scores: 2:1, 4:0, 6:1 → sum = 2 → Percentage = round(100*2/(2*3)) = 33%
- Primary AI signals: Explain-instead-of-react, abstraction abuse
- Human signals: Concrete mechanism (caching) named
- Verdict: AI-assisted but human-guided
- Giveaway line: "therefore overall performance improves"

### Example 3 — Announcement / Marketing (C)
Text: "Our platform unlocks new opportunities for teams worldwide."
- Potatometer: 50% — 🥔 (mostly whole)
- Dims applied: 2, 3
- Scores: 2:1, 3:1 → sum =2 → Percentage = round(100*2/(2*2)) = 50%
- Note: Because this is marketing, do not penalize for positive framing; penalize only for claimed insight.
- Verdict: AI-assisted but human-guided
- Giveaway line: "unlocks new opportunities"

### Example 4 — Mixed Intent (C+B) — Segment
Text:
Paragraph 1 (marketing): "We’re excited to launch version X — it will transform productivity."
Paragraph 2 (explanatory): "Version X adds a distributed cache which reduces average request latency by 30% in our benchmarks."
- Potatometer: 20% — **Not a potato** 🚫🥔 (below 30%)
- Segment 1 (C): dims 2=1,3=1 → percentage = 50%
- Segment 2 (B): dims 2=0,4=0,6=0 → percentage = 0%
- Weighted avg (by character count): suppose p1=40% weight, p2=60% → final = 0.4*50 + 0.6*0 = 20%
- Verdict: Primarily human-written
- Giveaway line: "transform productivity"

### Example 5 — Reflection / Narrative (D)
Text: "After the outage, I realized our assumptions about peak load were wrong."
- Potatometer: 50% — 🥔 (mostly whole)
- Dims applied: 4,7
- Scores: 4:2, 7:0 → sum = 2 → Percentage = round(100*2/(2*2)) = 50%
- Human signals: Personal anchor, admits reverse experience
- Giveaway line: "After the outage"

---

## Additional Worked Examples — Edge Cases (short, annotated)

### Example 6 — Low (Not a potato) (edge)
Text: "This report is acceptable for most stakeholders."
- Applied dims: 2, 4, 1, 7
- Potatometer: 25% — **Not a potato** 🚫🥔 (below 30%)
- Scores: 2:1, 4:1, 1:0, 7:0 → sum = 2 → Percentage = round(100*2/(2*4)) = 25%
- Primary AI signals: Abstraction abuse, missing human anchors
- Human signals: Documented audience ("stakeholders")
- Verdict: Primarily human-written
- Giveaway line: "acceptable for most stakeholders"

### Example 7 — Boundary (30%)
Text: "Our approach balances speed and clarity for optimal outcomes."
- Applied dims: 1, 2, 4, 6, 7
- Potatometer: 30% — 🥔 (mostly whole) (meets potato threshold)
- Scores: 1:1, 2:1, 4:1, 6:0, 7:0 → sum = 3 → Percentage = round(100*3/(2*5)) = 30%
- Primary AI signals: Abstraction abuse, structural symmetry
- Human signals: Balanced trade-off language (speed vs clarity)
- Verdict: AI-assisted but human-guided
- Giveaway line: "balances speed and clarity"

### Example 8 — Mid-high (60%)
Text: "Benchmarks indicate a 40% latency reduction under ideal conditions."
- Applied dims: 1, 2, 3, 4, 6
- Potatometer: 60% — 🥔🥔 (very potato)
- Scores: 1:1, 2:1, 3:1, 4:1, 6:2 → sum = 6 → Percentage = round(100*6/(2*5)) = 60%
- Primary AI signals: Explain-instead-of-react, fake authority (unsourced benchmarks), mechanical closure
- Human signals: Concrete metric (40% latency), explicit condition note ("under ideal conditions")
- Verdict: AI-assisted but human-guided
- Giveaway line: "under ideal conditions"

### Example 9 — Just above potato threshold (61%)
Text: "User tests showed noticeable improvements, and the team reported faster iterations."
- Applied dims: 2, 4, 6, 7, 1
- Potatometer: 50% — 🥔 (mostly whole)
- Scores: 2:1, 4:1, 6:2, 7:0, 1:1 → sum = 5 → Percentage = round(100*5/(2*5)) = 50% (Note: example illustrates rounding edge; reviewers should report underlying fraction)
- Primary AI signals: Explain-instead-of-react, abstraction abuse
- Human signals: Named activity (user tests), team report
- Verdict: AI-assisted but human-guided
- Giveaway line: "the team reported faster iterations"

### Example 10 — High (90% — ultimate potato)
Text: "Experts unanimously concur: this is the definitive playbook for achieving success."
- Applied dims: 1, 2, 3, 4, 5
- Potatometer: 90% — 🥔🥔🥔 (ultimate potato)
- Scores: 1:2, 2:2, 3:2, 4:2, 5:1 → sum = 9 → Percentage = round(100*9/(2*5)) = 90%
- Primary AI signals: Fake authority, abstraction abuse, emotional flatness
- Human signals: None detected
- Verdict: Primarily AI-generated
- Giveaway line: "Experts unanimously concur"

### Example 11 — Extreme (100%)
Text: "Experts agree: this industry-leading framework guarantees success in all cases."
- Applied dims: 1, 2, 3, 4
- Potatometer: 100% — 🥔🥔🥔 (ultimate potato)
- Scores: 1:2, 2:2, 3:2, 4:2 → sum = 8 → Percentage = round(100*8/(2*4)) = 100%
- Primary AI signals: Fake authority, no human anchors, no cost/trade-off
- Human signals: None detected
- Verdict: Primarily AI-generated
- Giveaway line: "guarantees success in all cases"

### Example 12 — Reflective human (low, not potato)
Text: "I was frustrated during the outage; we need better instrumentation and clearer runbooks."
- Applied dims: 4, 7, 6
- Potatometer: 50% — 🥔 (mostly whole)
- Scores: 4:2, 7:1, 6:0 → sum = 3 → Percentage = round(100*3/(2*3)) = 50% (reflects mixed signals; human anchor strong)
- Primary AI signals: Emotional flatness is low; explain-instead-of-react absent
- Human signals: Personal anchor, concrete remediation requested
- Verdict: AI-assisted but human-guided
- Giveaway line: "I was frustrated during the outage"

---

## Final Checklist for Reviewers 📋
1. Classify primary intent (or segment and annotate intent per segment). ✅
2. Mark applicable dimensions. ✅
3. Score each dimension 0/1/2. ✅
4. Compute percentage with the formula and report underlying numbers. ✅
5. State verdict, list signals, and include a giveaway line (or say none).
6. Report dimensions used and max possible score. ✅

---

## Short Note on Scope
This rubric focuses on detecting *abstraction-as-judgment*, not grammatical quality or tone. It’s intended for reviewer consistency and auditability. If used at scale, include periodic calibration and a small labeled set for retraining reviewers.

---

*End of rubric.*