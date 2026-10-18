# Navisio AI — Edge-Friendly SLM Improvement Roadmap

**Basis:** Findings from C-06–C-10 (Navisio AI vs NotebookLM), using the InsLogicBench-inspired evaluation framework.  
**Constraint:** Mainly local/edge hardware, with occasional Google Colab access.  
**Status:** Engineering recommendations and testable hypotheses, not proven internal diagnoses of Navisio's architecture.

## Executive recommendation

Build a **small, specialized insurance analysis pipeline**, not merely a smaller model trained to imitate existing answers. Start with a multilingual **3B–4B instruction-tuned SLM**, enhance retrieval and rule verification **before** training, then consider **LoRA/QLoRA** on verified Italian insurance examples. Measure contractual reliability and edge cost at every stage.

## 1. Benchmark findings to address

| Test | Observed behaviour | Improvement target |
|---|---|---|
| C-06 | Claims-made conclusion correct, but omitted notification and renewal details | Clause completeness and cross-clause retrieval |
| C-07 | Conflated location of negligent conduct with US court jurisdiction | Precise clause interpretation and exception checks |
| C-08 | Correctly handled unauthorized legal defence expenditure | Preserve procedural and numerical accuracy |
| C-09 | Correct post-termination reasoning, but omitted notification deadlines | Mandatory-condition coverage |
| C-10 | Overgeneralized insured-person definition without sufficiently reconciling specific provisions | Definition-to-condition dependency reasoning |

**Core lesson:** Finding a relevant article is not equivalent to applying it correctly. Errors may arise in retrieval, clause selection, interpretation, or answer generation; outputs alone cannot identify the internal cause.

## 2. Proposed system architecture

```text
Italian insurance PDFs + user question
                |
        Structure-aware parsing
 (policy / article / edition / PDF page)
                |
     Hybrid retrieval (BM25 + embeddings)
                |
   Reranking + linked-clause expansion
 (definitions, exclusions, exceptions,
  renewal, notices, endorsements)
                |
       Small multilingual LLM
   (structured fact/rule application)
                |
   Rule engine + citation verifier
      (True / False / Unknown)
                |
    Grounded conditional response
 (Covered / Not covered / Insufficient)
```

### Clause-aware retrieval

- Chunk by **complete contractual articles and subsections**, not just arbitrary token windows.
- Retain insurer, policy edition, article number, heading, PDF page, printed page, and cross-references as metadata.
- Combine lexical **BM25** with multilingual vector retrieval; optionally rerank top candidates using a compact reranker.
- Expand results to **linked definitions, exceptions, notice obligations, and renewal/endorsement clauses**.
- Example: retrieving AIG's *Assicurato* definition in C-10 should trigger inspection of Article 20 before asserting automatic coverage.

### Structured reasoning

Use an intermediate representation, inspired by InsLogicBench's argumentation approach:

```json
{
  "issue": "post-expiry claim eligibility",
  "facts": [{"proposition": "claim_first_received_2026_01_15", "status": "true"}],
  "supporting_clauses": ["claims-made temporal trigger"],
  "exclusions_or_exceptions": ["applicable observation or postuma extension"],
  "unknowns": ["renewal status", "endorsement status"],
  "conclusion": "INSUFFICIENT_INFORMATION",
  "reason": "Unlimited retroactivity alone does not extend the claims-made reporting window."
}
```

Use this as an auditable intermediate result, **not evidence of the model's private internal reasoning**.

### Lightweight deterministic checks

Handle dates, percentages, monetary thresholds, and mandatory conditions using code rather than free-form generation where possible. Use **three-valued logic** (`true`, `false`, `unknown`) so missing schedules or endorsements do not become assumed facts. A rule engine is not a substitute for the original policy wording or expert interpretation.

## 3. SLM candidates and deployment

| Candidate | Role | Caution |
|---|---|---|
| Qwen3-4B instruction model | Initial multilingual baseline | Test real Italian contractual language and inference cost |
| Gemma 3 4B | Independent multilingual comparison | Verify tokenizer, license, quantization, hardware compatibility |
| A 2B-class multilingual instruct model | Fallback for tight edge budgets | May need stronger retrieval/verifier to offset reduced capacity |

Start with **quantized local inference** (for example, a compatible llama.cpp/GGUF workflow). Do not commit to a model until a standardized edge benchmark measures accuracy, peak RAM/VRAM, latency and tokens/sec. Exact feasibility depends on device, context length, quantization and runtime.

**Illustrative hardware guidance, not guaranteed minima:**

- **CPU + 16 GB RAM:** try quantized 2B–4B inference; train on Colab instead.
- **6–8 GB GPU VRAM:** small-model inference, potentially carefully tuned QLoRA for 2B–4B.
- **12–16 GB GPU VRAM:** more practical LoRA/QLoRA experiments for 3B–4B, subject to context and batch size.
- **Colab:** occasional adapter training and benchmarking; export merged/quantized models for edge deployment.

## 4. Training strategy: after the untrained baseline

1. **Do not train first.** Test the base SLM with and without RAG and deterministic checks to isolate where the improvements come from.
2. When warranted, use **supervised fine-tuning with LoRA or QLoRA** on a compatible model rather than full fine-tuning.
3. Start with short examples and conservative settings (e.g., LoRA rank 8–16; batch size 1 and gradient accumulation; context around 2,048 tokens). Tune against actual GPU memory and held-out validation; these are not optimality claims.
4. Train on **verified corrections and contractual ground truth**, not blindly on uncorrected Navisio or NotebookLM outputs.
5. Keep the original C-06–C-10 scenarios out of training and use new held-out variations and policy-level splits for evaluation.

### Data design

| Category | Example target |
|---|---|
| Clause classification | Coverage, exclusions, definitions, notification and renewal clauses |
| Cross-clause interpretation | Conduct location vs court jurisdiction; insured definition vs Article 20 |
| Missing-condition detection | Unverified postuma endorsement or renewal |
| Dates and monetary reasoning | Claims-made cutoffs, 25% defense-cost limits, deductibles |
| Negative / near-miss examples | Plausible but inapplicable clauses; distinguishing *not covered* from *not established* |

Each training row should include source excerpts, the scenario, verified propositions, relevant clauses, missing facts, a justified decision, and a concise explanation. A **few hundred verified examples** can support an initial pilot; ~1,000–3,000 is a possible expansion target, not an established minimum.

## 5. Experiments needed to prove improvements

| Configuration | What the experiment isolates |
|---|---|
| Base SLM only | Starting language/reasoning capability |
| Base SLM + RAG | Retrieval effect |
| Base SLM + RAG + verifier | Structured checks / evidence validation effect |
| Fine-tuned SLM + same RAG | Effect of training |
| Fine-tuned SLM + RAG + verifier | End-to-end candidate system |

### Evaluation metrics

- **Decision validity:** supported / contradicted / insufficient information, plus error analysis.
- **Citation selection:** precision, recall and F1 against an explicitly fixed clause reference set.
- **Citation attribution:** whether each cited clause supports the specific claim attached to it.
- **Explanation coverage:** correct, partial, omitted and incorrect propositions.
- **Logical consistency:** whether the conclusion follows from premises, including exceptions and unknowns.
- **Edge performance:** runtime latency, tokens/sec, peak memory, quantization effects, energy where measurable.

Use a sufficiently large **unseen** suite of controlled scenarios, including minimal pairs where one fact changes. Do not overinterpret the five C-06–C-10 tests or treat their provisional scores as statistically reliable model rankings.

## 6. Prioritized implementation roadmap

**Phase 1 — Baseline, no training**

- Select 3B–4B multilingual candidate(s); collect edge throughput and memory measurements.
- Build a set of manually verified Italian insurance examples and clean train/validation/test splits.

**Phase 2 — Pipeline improvements, no training**

- Implement article-aware parsing, BM25+vector search, reranking and linked-clause expansion.
- Add structured extraction, a three-valued checker for dates/limits, and citation validation.
- Rerun the same held-out tests to quantify gains from architecture alone.

**Phase 3 — Parameter-efficient training**

- Fine-tune a compatible model with LoRA/QLoRA on verified Italian insurance examples.
- Compare **fine-tuned SLM + identical RAG** against **base SLM + identical RAG**.
- Check for regressions on straightforward cases such as C-08/C-09.

**Phase 4 — Edge optimization**

- Quantize and profile the chosen SLM; tune context size and retrieval budget.
- Retain external rule and citation checking even if generation is optimized.

## 7. Priority by compute cost

| Change | Expected value | Compute cost | Priority |
|---|---|---|---|
| Clause-aware retrieval | High potential | Low | 1 |
| Cross-clause expansion | High potential | Low–medium | 2 |
| Structured rules and conditional answer checking | High potential | Low | 3 |
| Citation-to-claim verification | High potential | Low–medium | 4 |
| LoRA / QLoRA fine-tuning | Requires evidence from baseline | Medium | 5 |
| Teacher-assisted data generation + human verification | Potentially useful later | Medium–high | 6 |
| Full model training from scratch | Poor match for current budget | Very high | Avoid |

## Conclusion

**Recommended first build:** A quantized multilingual 3B–4B SLM with **clause-aware RAG, linked-condition retrieval, structured reasoning, deterministic checks and verified citations**. Use occasional Colab sessions for adapter fine-tuning **only after** demonstrating which errors remain unsolved by retrieval and verification. The objective is a more reliable, explainable and edge-deployable insurance analysis system—not simply a smaller copy of the existing model.

**Next hardware detail needed:** local GPU model and VRAM, or CPU/RAM if no dedicated GPU.
