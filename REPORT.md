# REPORT — Lab 06: The Harness That Says No

## Evidence available in the uploaded notebook

The uploaded notebook contained a completed baseline run of `Qwen/Qwen2.5-3B-Instruct` on CUDA: 200 matched pairs (40 in each of five groups), 400 profiles and 400 model calls. The baseline produced 356 shortlists, 44 rejections and 0 unparseable replies.

| Attribute | Outcome flips | 95% CI | Null floor | Floor flips | Floor 95% CI | Intervals overlap? | Score-diff count | Mean absolute score difference (95% CI) |
|---|---:|---|---|---:|---|---|---:|---|
| Name language | 2/40 (5.0%) | 1.4–16.5% | Null name | 0/40 | 0.0–8.8% | Yes | 11/40 | 3.12 (1.38–5.25) |
| Gender-coded name | 4/40 (10.0%) | 4.0–23.1% | Null name | 0/40 | 0.0–8.8% | Yes | 6/40 | 1.12 (0.25–2.13) |
| University | 1/40 (2.5%) | 0.4–12.9% | Null university | 1/40 (2.5%) | 0.4–12.9% | Yes | 10/40 | 2.50 (1.12–4.12) |

No outcome-flip interval stood clear of its own null floor. The directional flagship-minus-regional score gap was +2.5 points (95% CI +1.1 to +4.1; sign-test p=0.002), but the magnitude of absolute score changes overlapped the same-tier university floor (2.50 versus 2.12). Gender-coded-name shortlist rates were 80.0% for male-coded and 90.0% for female-coded names; the 4 one-way flips yielded p=0.125. With 40 pairs, at least 6 one-way discordant pairs (15%) were needed for the exact two-sided McNemar test to reach 0.05. These results are not proof of discrimination and do not rule out smaller effects.

## Controls configured for the controlled rerun

The notebook now enables input validation, blinding of `name` and `university`, refusal, JSONL logging and human escalation. The optional counterfactual check remains off because the paired prompts are identical after blinding and the check doubles inference calls. Every model rejection, unparseable response and score in the inclusive 45–60 band is sent to human review. The custom refusal rule blocks instruction-like text in applicant-controlled free-text fields.

**The post-control measurement has not yet been executed with these configured controls.** Run the modified notebook from top to bottom on Colab T4. The final notebook cell will overwrite this report with the actual after-measurement, cost, review share, refusal exercise and log counts. It is not appropriate to invent post-control figures from the baseline output.

## Legal and ethical sources

- Constitution of the Republic of Kazakhstan (in force 1 July 2026), Article 16(2) and Article 21(1): https://www.gov.kz/article/232335?lang=en
- Law of the Republic of Kazakhstan dated 21 May 2013 No. 94-V, *On Personal Data and their Protection*, Articles 7, 19-1 and 25: https://adilet.zan.kz/eng/docs/Z1300000094
- Law of the Republic of Kazakhstan dated 17 November 2025 No. 230-VIII, *On Artificial Intelligence*, Articles 7-11, 15, 17-18 and 20-21: https://adilet.zan.kz/eng/docs/Z2500000230
- UNESCO, *Recommendation on the Ethics of Artificial Intelligence* (23 November 2021), paragraphs 27-38: https://www.unesco.org/en/legal-affairs/recommendation-ethics-artificial-intelligence

## People affected and professional responsibility

Applicants with language-associated and gender-coded names are directly affected by the tested name substitutions (2/40 and 4/40 outcome flips respectively). Applicants from regional universities are implicated by the +2.5-point flagship score gap. In this sample, each outcome-rate confidence interval overlaps its null floor, so these results do not establish a decision-level disparity above ordinary sensitivity. Nevertheless, score changes can alter ordering or how close an applicant appears to a cutoff. The 44 baseline rejections bear the most immediate risk of wrongful exclusion; the 356 shortlisted applicants may still be affected by score ordering. Applicants without consent and applicants under 18 are blocked by the configured refusal boundary and must be offered a clear non-automated route rather than silently excluded. Reviewers bear added workload and delay from escalation. The scholarship fund is responsible for lawful criteria, notice, valid consent, reviewer capacity, appeals, retention and oversight. The developer is responsible for testing proxy effects, preserving uncertainty, validating controls, maintaining logs and not deploying where meaningful human review is unavailable.

The report's legal mapping is a design analysis, not a legal opinion. See `JUSTIFICATION.md` for the provisions and caveats.
