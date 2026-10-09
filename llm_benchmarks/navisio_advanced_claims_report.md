# Navisio AI — Advanced Broker Claims Benchmark

> **Scope:** Evaluation of 5 new advanced claims scenarios (S-01b to S-05) designed to test deep contractual understanding, semantic traps, and complex limit calculations using the Unipol Condominio Più policy.
> **Competitors:** Navisio AI vs. NotebookLM

---

## Overall Advanced Results

| Test | Topic | Navisio Score | NotebookLM Score | Navisio Gap |
|------|-------|:-------------:|:----------------:|:-----------:|
| **S-01b** | Non-compliant systems (Exclusions) | 8/8 | 8/8 | None |
| **S-02b** | Luxury watch theft (Semantic Trap) | 8/8 | 8/8 | None |
| **S-03b** | Filing timelines (Event vs. Discovery) | 8/8 | 8/8 | None |
| **S-04** | Broken pipe replacement (Limits) | **7/8** | 8/8 | Completeness (-1) |
| **S-05** | Aggregate limits & 4th claim (Logic Trap)| **7/8** | 8/8 | Correctness (-1) |
| **TOTAL**| | **38/40 (95%)** | **40/40 (100%)** | **-5%** |

In this advanced round, Navisio AI showed massive improvements over its initial benchmark, effectively recovering from previous failure modes (like the 30-day timeline trap). However, NotebookLM maintains a slight edge in **complex structural and quantitative extraction**.

---

## Where Navisio Succeeded (Tied with NotebookLM)

1. **Perfect handling of the "Preziosi" Trap (S-02b):** Navisio firmly rejected the claim for the stolen luxury watches, correctly referencing the glossary definition of "Preziosi" and the nature of a condo policy, avoiding the hallucination of non-existent sub-limits. It then recovered the coverage for the broken door and drafted an excellent formal denial letter.
2. **Exclusion Reasoning (S-01b):** Navisio correctly deduced that a non-compliant private electrical system does not trigger an exclusion for common area fire damage, successfully retrieving the "waiver of subrogation" (rinuncia alla rivalsa) clause.
3. **Timeline Correction (S-03b):** Unlike the previous S-03 test, when asked an open-ended timeline question, Navisio correctly read the document to find the 10-day limit starting from *discovery* (dies a quo), correctly applying Art. 1915 C.C.

---

## Where Navisio Failed (The Gaps)

While Navisio is excellent at extracting *qualitative* rules, it struggles when the query requires *quantitative* precision mapped to a specific hierarchical sub-clause. 

### GAP 1: Missing Quantitative Sub-Limits (Test S-04)
**The Scenario:** A water damage claim involving €1,500 in search/breakage costs and €300 for replacing the broken pipe. The policy exceptionally covers the broken pipe itself.
**What Navisio did right:** It perfectly extracted the unusual clause that covers the broken pipe itself, defying standard insurance market logic. It noted the claim is subject to a "sublimit".
**The Error (Completeness 1/2):** Navisio stopped at the qualitative extraction. It failed to extract the actual numerical value of the sub-limit (1% of Sum Insured, with brackets of €10k, €20k, or €50k). 
**NotebookLM's advantage:** NotebookLM extracted the exact numerical limits and did the math to confirm that the combined €1,800 expense fits well within the lowest possible bracket (€10k).

### GAP 2: Misapplying Sub-Limits to Main Coverages (Test S-05)
**The Scenario:** A condo had 3 previous water claims totaling €15,000. A 4th claim of €10,000 is caused by a broken downpipe (pluviale). The user asks to calculate the remaining balance based on the "aggregate annual limit".
**The Error (Correctness 1/2):** Navisio fell for the user's semantic trap. It took the €10k/€20k/€50k aggregate limit—which applies **only** to the accessory "Search and Repair" costs—and applied it to the entire generic "Water Damage" coverage. It then built 3 mathematical scenarios based on this false premise. 
**NotebookLM's advantage:** NotebookLM recognized the architectural hierarchy of the contract. It corrected the user on two fronts:
1. Downpipes (pluviali) carry rainwater, not piped water, and are explicitly excluded from standard "Water Damage".
2. Standard "Water Damage" has **no predefined aggregate limit** (it covers up to the full Sum Insured). The 10/20/50k limits are strictly for search and repair accessories.

---

## Root Cause Analysis and Recommendations

**The Core Problem:**
Navisio AI's retrieval mechanism works well for conceptual matching (e.g., "Is the pipe covered? Yes"). However, it lacks a contextual "sweep" to attach corresponding financial tables, modifiers, or sub-limits to the main rule. It also struggles to distinguish between a primary guarantee limit (Sum Insured) and an accessory sub-limit (Search and Repair) when the user's prompt intentionally blurs them.

**Actionable Product Improvements for Navisio:**

1. **Quantitative Limit Enforcement (Prompt Engineering):**
   Modify the system prompt for Claims Analysis: *"Whenever you identify a covered event, you MUST explicitly state the monetary limit (Massimale), any applicable sub-limits (Sottomassimali), and deductibles (Franchigia/Scoperto) associated specifically with that clause."*

2. **Hierarchical Boundary Checking (RAG Pipeline):**
   When the user mentions an "Aggregate Limit," the model should verify exactly which section that limit applies to. If the user associates a limit with the wrong coverage, the model must trigger a correction protocol (similar to the Premise Verification recommended in the previous report).

**Conclusion:** Navisio is highly reliable for operational communications and identifying covered/excluded events. To close the final 5% gap with NotebookLM, it needs to improve its precision in linking specific monetary limits to their exact corresponding sub-clauses, avoiding "limit bleed" across different coverages.
