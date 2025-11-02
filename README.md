# LinkedIn Detective

LinkedIn Detective is a custom GPT suite that evaluates whether a LinkedIn profile is legitimate or suspicious. It scores legitimacy, explains the rationale, and flags risks without pretending to “verify” identities. Use it to triage profiles before outreach, hiring, or partnership steps.

## What’s in this repo

* `linkedin_detective.json` — core evaluator that aggregates signals and issues a score, verdict, rationale, and recommendation
* `linkedin_red_flags_detector.json` — sub-agent focused on obvious warning signs (fake photos, unverifiable companies, inflated titles)
* `career_timeline_verifier.json` — sub-agent that checks chronology, overlaps, progression, and employer plausibility

## Quick start

1. Open ChatGPT’s “Create a GPT”.
2. Upload the three JSON files.
3. Name the main GPT “LinkedIn Detective”. Optionally reference the other two as helper GPTs in the Instructions or Tools.
4. Save and start testing with the example prompts below.

## Why this exists

Most “profile checks” are gut feel. This suite turns instincts into a repeatable rubric with a scored output and crisp next steps.

## How it works

* The core GPT collects signals: completeness, timeline plausibility, network authenticity, and red flags
* The red flags detector focuses on high-signal anomalies
* The timeline verifier validates chronology and advancement
* The core model combines results into a 0–100 legitimacy score and a verdict

## Inputs

You can paste a LinkedIn URL or a text summary of the profile. For privacy and policy reasons, the GPT only analyzes what you provide and will not scrape the web.

### Recommended input template

```
Profile:
- URL: <optional>
- Headline:
- About summary:
- Experience (company, title, dates, bullets):
- Education:
- Skills/endorsements:
- Activity summary (posts, comments, cadence):
- Notable artifacts (certs, projects, publications):
```

## Output schema

```json
{
  "legitimacy_score": 0,
  "verdict": "Legitimate | Suspicious | Fake",
  "rationale": [
    "Concise reason 1",
    "Concise reason 2",
    "Concise reason 3"
  ],
  "recommendation": "Safe to engage | Connect with caution | Request verification | Avoid"
}
```

## Example prompts

* Analyze this LinkedIn profile and tell me if it looks legitimate or fake
* Give me a legitimacy score and explain your reasoning for this LinkedIn profile
* What red flags or inconsistencies stand out in this LinkedIn profile
* Compare these two LinkedIn profiles and tell me which seems more authentic

## Scoring rubric

* 80–100: Strong signals across completeness, timeline, and network. Minor or no issues
* 60–79: Mostly plausible with small gaps or light inconsistencies. Proceed with caution
* 40–59: Multiple unanswered questions, shallow network, or shaky employers. Verification needed
* 0–39: Clear anomalies, synthetic patterns, or fake elements. Do not engage

## Red flags catalog

* AI/stock profile photo, face mismatch across images
* Unverifiable employers or universities, domains with no footprint
* Rapid jumps to senior roles with thin history
* Overlapping roles without plausible justification
* Low or unnatural network and engagement patterns
* Keyword-stuffed About section with generic jargon and no specifics

## Timeline checks

* Chronology is sequential and dates align
* Tenure lengths make sense for level and industry
* Education timing matches early roles
* Employers are real and active during claimed dates

## Limitations and guardrails

* No scraping. The GPT only assesses provided content
* Not a background check or KYC tool
* No legal or hiring decisions. Output is advisory
* No doxxing, private data exposure, or defamation
* When uncertain, it marks items as “unverifiable”

## Suggested workflow

1. Collect profile data in the input template
2. Run the red flags detector first if the profile looks thin
3. Run the career timeline verifier for complex histories
4. Run LinkedIn Detective to get the final score and recommendation
5. Decide your next step: connect, request evidence, or walk away

## Customization

Edit thresholds and weights in `linkedin_detective.json`:

* Increase the impact of `red_flags` for high-risk roles
* Lower the minimum connection count for niche industries
* Add sector-specific checks (e.g., open-source contributions for dev roles)

## Roadmap

* Optional evidence requests (e.g., link to public talk, published work)
* Sector-specific detector packs
* Team workflow playbook and scoring dashboard template

## Ethics and compliance

* Respect privacy and platform terms
* Avoid biased signals (photo quality, name, location)
* Prioritize transparent criteria and human review for decisions

## License

MIT. See `LICENSE` if included by your repo setup.
