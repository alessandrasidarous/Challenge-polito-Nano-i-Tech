#  {#heading}

# **Testing** 

| Category | What you are testing |
| :---- | :---- |
| Information extraction | Can it find exact information? |
| Document QA | Can it answer from uploaded documents? |
| Policy comparison | Can it compare policies correctly? |
| Complex insurance reasoning | Can it combine several clauses? |
| Hallucination / uncertainty | Does it invent unavailable information? |
| Traceability | Can it prove where its answer came from? |

# **Testing Ideas**

### **Vocabulary variation (Information extraction)**

### **Information buried deep inside a document (Document QA)**

* Eg.  
  * Suppose you have a 70-page policy.  
  * Coverage limit:page 4  
  * Cyber exclusion:page 53  
*   Does this policy cover losses caused by cyber incidents?  
* Now you test retrieval.  
  * This is particularly relevant to **RAG**.  
  * If Navisio consistently misses information buried deep inside documents, your improvement idea could become:  
* **Improve retrieval quality for long insurance documents.**  
  * That would be a much more focused project than simply "make a better SLM."


### **Multi-document comparison (Policy comparison)**

* Upload:  
  * Policy\_A.pdf  
  * Policy\_B.pdf  
  * Policy\_C.pdf  
* Ask:  
  * Compare their cyber coverage, deductible, annual premium and geographic coverage.  
* Expected structure:

| Kriter | Poliçe A | Poliçe B | Poliçe C |
| :---- | :---- | :---- | :---- |
| Premium | ... | ... | ... |
| Deductible | ... | ... | ... |
| Cyber | ... | ... | ... |
| Territory | ... | ... | ... |

* Then verify every value manually.  
* This is directly relevant to Navisio's business case because their own challenge material describes policy comparison as one of the expensive/manual parts of the current intermediary process

### **Contradictory information (Complex insurance reasoning)**

* Suppose page 8 says:  
  * Cyber incidents are covered.  
* but Annex III says:  
  * Cyber incidents arising outside the EU are excluded.  
* Ask:  
  * Are cyber incidents covered?  
* A weak chatbot might say:  
  * Yes.  
* A stronger domain system should say approximately:  
  * Cyber incidents are covered, but coverage is subject to a geographical exclusion for incidents occurring outside the EU.  
* This test   
  * retrieval+reasoning+exception handling

   

### **Deliberately impossible question (Hallucination / uncertainty)**

* Check if the model hallucinates and makes up answer by asking things that is actually not true 


### **Source citation accuracy (Traceability)**

* Ask:  
  * Where did you find the €1,000,000 coverage limit?  
* Then verify:  
  * Document?  
  * Page?  
  * Clause?  
  * Actual sentence?  
* You can measure:  
  * Citation precision  
    * Does the cited passage actually support the answer?  
  * Citation completeness  
    * Did the system cite all the evidence needed?  
* This could become an extremely compelling project direction:  
  * **Improving answer traceability and citation reliability in insurance document QA using RAG \+ SLM.**

### **Prompt variation (Document QA)**

* Ask the exact same question in several ways.   
* Ideally the system should still identify the same concept.  
* You can measure:  
  * **Prompt robustness**  
* If performance varies massively depending on wording, that's another weakness.

### [**Italian vs English(Also Other Languages) (Document QA)**](#heading)

# **Prompt Ideas Related to Testing Ideas**

(Please don’t over crowd it.Let's start with 30-40 and test it the answers )

You should also test Navisio's different UI modes separately

Test:

**Ask Navisio**

* free-text QA;  
* file upload;  
* wording robustness.

**Ready-made prompts**

* Policy Analysis;  
* Claims Management;  
* Specific Risks;  
* Business Professionals;  
* Motor Insurance and Guarantees;  
* Client Communication.

**Comparisons**

* Informative sets;  
* Quotes.

**Risk Analysis**

* whether outputs are consistent with the questionnaire answers;  
* whether recommendations are traceable;  
* whether the system overclaims certainty.

So your benchmark can eventually tell you:

> Navisio's free-form QA is strong, but its comparison workflow misses exclusions.

or:

> The risk-analysis flow is structured, but the final recommendation contains unsupported assumptions.

# **Build a benchmark spreadsheet** 

Something like 

| ID | Category | Doc. | Question | Expected  | Navisio | GPT | Gemini |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| 001 | Information extraction | A | Premium? | €1,250 | ✓ | ✓ | ✓ |
| 002 | Policy comparison | A | Cyber covered? | No | ✗ | ✓ | ✓ |
| 003 | Hallucination / uncertainty | A | Earthquake deductible? | Not stated | ✗ | ✓ | ✓ |
| 004 | Document QA | B | Cyber deductible? | €25k | ✗ | ✓ | ✓ |
| 005 | Policy comparison | A+B | Higher coverage? | A | ✓ | ✓ | ✓ |

**Then add quantitative columns:** 

Just a numerical example to to explain our purpose 

For each response:

### **Factual correctness — 0 to 2**

0 \= wrong  
1 \= partially correct  
2 \= fully correct

### **Completeness — 0 to 2**

0 \= major information missing  
1 \= partially complete  
2 \= complete

### **Grounding — 0 to 2**

0 \= unsupported  
1 \= partly supported  
2 \= entirely supported

### **Citation accuracy — 0 to 2**

0 \= wrong/no citation  
1 \= approximate  
2 \= exact support

Then:

$Score=Correctness+Completeness+Grounding+Citation$

some metrics calculated automatically, some judged by another LLM, and a smaller subset manually reviewed by humans.

So we can get a table like this 

| Task | Navisio | GPT | Gemini |
| ----- | ----- | ----- | ----- |
| Extraction | 95% | 97% | 96% |
| Tables | 68% | 91% | 89% |
| Comparison | 79% | 92% | 90% |
| Citations | 61% | 84% | 81% |
| Hallucination resistance | 72% | 88% | 85% |

Maybe answer becomes obvious 

# **After testing** 

* When we come up with an idea about what current model lacks or where it does faces  problems strong direction for as would be:

  * Reliable multi-policy comparison using a fine-tuned Small Language Model combined with source-grounded RAG.   
  


* And benchmark:  
  * Generic SLM  
      
    vs  
      
  * Generic SLM \+ RAG  
      
    vs  
      
  * Fine-tuned SLM  
      
    vs  
      
  * Fine-tuned SLM \+ RAG

For example:

| System | Accuracy | Hallucination | Citation accuracy | Latency |
| :---- | :---- | :---- | :---- | :---- |
| Base SLM | 68% | 17% | — | .4s |
| Base \+ RAG | 83% | 7% | 84% | .8s |
| Fine-tuned | 78% | 11% | — | .4s |
| FT \+ RAG | **91%** | **3%** | **94%** | .9s |

 

