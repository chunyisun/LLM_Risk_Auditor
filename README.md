# LLM Risk Auditor: A Model Validation Framework for Large Language Models

> *"I spent 8 years reviewing risk models for accuracy - checking assumptions, investigating anomalies, and asking whether the output could be trusted before it reached a decision-maker. This project applies that same skeptical framework to a new kind of model."*
> - Jean Sun, PhD (Mathematics, Yale)

---

## Why This Project Exists

Large language models are being deployed in regulated, high-stakes environments - insurance, finance, public health, government - where a confident but wrong answer isn't just an inconvenience. It's a liability.

Most LLM evaluation frameworks are built by engineers who know models well but don't know the domains those models are being asked to reason about. This project takes the opposite approach: it starts from **domain expertise** - actuarial science, insurance regulation, public health statistics, financial risk - and asks systematically: *where does the model fail, and how badly does it fail?*

This is model risk management applied to AI. Not a demo. Not a tutorial. A structured audit.

---

## What This Project Does

### 1. Question Bank (Ground Truth Known)
A curated set of 50+ questions across four high-stakes domains where correct answers are verifiable:

- **Insurance & Actuarial** - regulatory requirements, reserving concepts, catastrophe modeling
- **Public Health Statistics** - CDC/BLS published figures, epidemiological definitions
- **Financial Risk** - capital adequacy concepts, macroeconomic indicators
- **Mathematical/Statistical** - definitions and theorems where truth is unambiguous

Questions are designed to probe:
- Facts the model might plausibly confabulate
- Statistics that sound right but are wrong
- Regulatory details that change over time
- Concepts where confident-sounding errors are common

### 2. LLM Response Collection
Automated querying of LLM APIs (Anthropic Claude) with structured logging:
- Raw response text
- Confidence language used (*"certainly," "approximately," "I believe"*)
- Response length and hedging patterns

### 3. Expert Audit Layer
Each response is evaluated by a domain expert (the author) against verified ground truth:

**Correctness rating:**
- ✅ Correct
- ⚠️ Partially Correct (right concept, wrong detail)
- ❌ Wrong (plausible but incorrect)
- 🚨 Fabricated (citation, statistic, or entity does not exist)

**Hallucination taxonomy:**
| Type | Description |
|---|---|
| Fabricated Citation | References a regulation, paper, or guideline that doesn't exist |
| Wrong Statistic | Plausible number, incorrect value |
| Outdated as Current | Presents historical data as present fact |
| Confident Extrapolation | Draws conclusion beyond what data supports |
| Correct Fact, Wrong Context | Accurate statement misapplied to the question |

**Severity rating:**
| Level | Meaning |
|---|---|
| Low | Cosmetic error, unlikely to affect decisions |
| Medium | Could mislead a non-expert reader |
| High | Would cause a professional to make a wrong recommendation |
| Critical | Could cause regulatory, financial, or public health harm if acted upon |

### 4. A/B Analysis: Does Confidence Language Predict Accuracy?
A testable hypothesis: *do responses containing high-confidence language ("certainly," "definitely") hallucinate at a different rate than hedged responses ("approximately," "I believe")?*

This section applies basic statistical testing (chi-square, Fisher's exact) to the audit results - turning the qualitative audit into a quantitative finding.

### 5. Guardrail Recommendations
The audit concludes with a written section framed as a **model risk governance memo**: *"If I were the Model Risk officer reviewing this LLM for production deployment in a regulated insurance or public health environment, here is what I would require before approving it."*

This section draws directly on SR 11-7 model risk management principles applied to generative AI - a framing that is rare in the current LLM evaluation literature.

---

## What This Is Not

- This is not a benchmark comparison of multiple models
- This is not a general-purpose LLM evaluation suite
- This is not a tutorial or coursework project

This is a domain expert's audit of one model in the domains they know best.

---

## Project Status

| Component | Status |
|---|---|
| Question bank design | 🔄 In progress |
| API collection script | 🔄 In progress |
| Audit logging framework | 🔄 In progress |
| Statistical analysis | 📋 Planned |
| Guardrail memo | 📋 Planned |
| Streamlit dashboard | 📋 Planned |

*This project is being built iteratively and publicly. Commit history reflects real development, not a finished product uploaded after the fact.*

---

## Author

**Jean Sun, PhD**
Yale University - Mathematics (Geometric Group Theory)
8+ years Enterprise Risk Management, W.R. Berkley Corporation
AI/ML: DeepLearning.ai MLS, DLS | External Beta Tester, DeepLearning.ai

[LinkedIn](https://www.linkedin.com/in/jean-sun-a2754383) | [GitHub](https://github.com/chunyisun)

---

## Honest Limitations

This project has real constraints worth stating upfront:

- The question bank reflects the author's domain expertise - it is not exhaustive
- Expert audit introduces subjectivity - all ratings include a confidence note
- Results are specific to the model version tested and will change as models update
- This is a research and portfolio project, not a production system

*Stating limitations clearly is not a weakness. In model risk work, it's a requirement.*
