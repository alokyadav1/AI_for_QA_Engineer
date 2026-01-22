# AI for QA Engineer Learning

Repository to maintain learning progress on "AI for QA Engineer".

## Structure
- `prompts`: Collection of useful prompts for QA tasks.
- `notes`: Learning notes and resources.
- `experiments`: Code snippets and small projects.

---
> [!NOTE]
> All notes and prompts in this repository are created using ChatGPT.

# LLM Fundamentals — Part 2
*(GPT Architecture + Tokens & Context)*

## 6️⃣ GPT Architecture (High-Level, QA-Friendly)

> [!WARNING]
> We’ll not go into math or deep ML, only what a QA Engineer must know to test effectively.

### What Does “GPT” Mean?
**GPT** = Generative Pre-trained Transformer

| Term | Meaning (Simple) |
| :--- | :--- |
| **Generative** | Generates text. |
| **Pre-trained** | Trained before you use it (on huge datasets). |
| **Transformer** | The specific model architecture. |
| **Language** | Works primarily on text. |
| **Model** | A statistical pattern-matching system. |

### 6.1 Transformer (Core Idea)
A Transformer is a model that looks at all words (**tokens**) together, not one-by-one.
*   **Context:** Understands how words relate across long distances.
*   **Structure:** Maintains complex formatting (like Gherkin or JSON).
*   **Efficiency:** Processes information faster than older models.

### 6.2 Attention Mechanism
**“Which words in the prompt should I focus on more?”**

*   **Example Prompt:** *"Generate negative test cases for checkout payment failure"*
*   **Model focuses on:** `checkout`, `payment`, `failure`.

> [!TIP]
> **QA Insight:** Poor prompts = wrong attention = bad output. If your prompt is noisy, attention gets diluted and quality drops.

### 6.3 GPT Processing Flow
1.  **Tokenization:** Prompt is split into tokens.
2.  **Attention Layers:** Relationships between tokens are calculated.
3.  **Prediction:** The next token is predicted.
4.  **Recurrence:** Process repeats until the end of the response.

---

## 7️⃣ Tokens (Critical for QA)
A token is a word, part of a word, or punctuation.
*   *Example:* “authentication” → `authen` + `tication`.

### Why QA Engineers Must Care
| Reason | QA Impact |
| :--- | :--- |
| **Context Limit** | Long logs may get truncated or lost. |
| **Cost** | APIs charge per token used. |
| **Output Cutoff** | Long test suites might stop mid-file. |

### 7.1 Context Window
The maximum tokens a model can remember (Prompt + Instructions + Chat History + Response).
> **📌 Once exceeded, old info is forgotten.**

**Best Practices:**
*   ✅ Summarize long logs before pasting.
*   ✅ Extract only relevant business rules.
*   ✅ Split tasks into smaller, focused prompts.

### 7.2 Temperature
Controls randomness:
*   **Low (0–0.3):** Deterministic, consistent, logical.
*   **High (0.7+):** Creative, varied, risky.
> **📌 QA Rule:** Always prefer low temperature for testing tasks.

---

# LLM Fundamentals — Part 3
*(Local LLMs, Cost Trade-offs, Bias & Hallucination)*

## 8️⃣ Running Open-Source LLMs Locally
Instead of calling a cloud API, you run the model on your own machine.
> **Analogy:** Local test environment vs. Cloud test environment.

### Why Use Local LLMs?
*   **Data Privacy:** No sensitive logs or PII ever leave your system.
*   **Cost:** No per-token cost (unlimited usage).
*   **Offline:** Works without internet access.

### Trade-offs
| Advantage | Limitation |
| :--- | :--- |
| **Free Usage** | Requires powerful hardware (RAM/GPU). |
| **Private** | Slower than cloud-scale models. |
| **Customizable** | Generally smaller models (less reasoning). |

### QA Use Cases
*   ✅ Generate test cases from internal/sensitive docs.
*   ✅ Analyze logs containing proprietary data.
*   ✅ Experiment with prompts safely.
