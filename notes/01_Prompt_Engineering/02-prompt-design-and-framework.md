# 1️⃣ What Is a Prompt Framework?

## Simple Definition
**A prompt framework is:**
> A structured checklist that ensures your prompt is clear, complete, and predictable.

**Think of it like:**
*   Test case template
*   Bug report format
*   Gherkin structure

> **📌 Frameworks prevent:**
> *   Missing requirements
> *   Ambiguous AI outputs
> *   Inconsistent responses

---

# 2️⃣ SMART Prompt Framework

## What SMART Stands For
| Letter | Meaning | QA Interpretation |
| :--- | :--- | :--- |
| **S** | Specific | Clear task |
| **M** | Measurable | Verifiable output |
| **A** | Achievable | Realistic scope |
| **R** | Relevant | QA-focused |
| **T** | Time/Format bound | Structured result |

## SMART Prompt Example (QA)

### ❌ Bad
> Generate test cases for checkout

### ✅ SMART
```text
Generate functional and negative test cases
For guest checkout flow
On e-commerce web application
Output in Gherkin format
Cover payment, validation, and error handling
```

## When QA Engineers Should Use SMART
*   ✅ Test case generation
*   ✅ Regression scope definition
*   ✅ Acceptance criteria validation

---

# 3️⃣ CLEAR Prompt Framework

## What CLEAR Stands For
| Letter | Meaning | QA Meaning |
| :--- | :--- | :--- |
| **C** | Context | App + user + platform |
| **L** | Logic | Business rules |
| **E** | Examples | Few-shot |
| **A** | Action | What AI must do |
| **R** | Result | Expected output |

## CLEAR Prompt Example (QA)

**Context:**
> User is a guest on an e-commerce website.

**Logic:**
> User must add item to cart before checkout.

**Example:**
```gherkin
Scenario: Add item to cart
Given User is on product page
When User clicks add to cart
Then Item should be added to cart
```

**Action:**
> Generate negative scenarios for this flow.

**Result:**
> Output in Gherkin format.

> **📌 CLEAR = best for consistency**

## When QA Engineers Should Use CLEAR
*   ✅ Gherkin-heavy projects
*   ✅ Automation-ready output
*   ✅ Team-shared prompts

---

# 4️⃣ CRISP Prompt Framework

## What CRISP Stands For
| Letter | Meaning | QA Meaning |
| :--- | :--- | :--- |
| **C** | Clear role | QA persona |
| **R** | Requirements | Functional rules |
| **I** | Input data | Constraints |
| **S** | Scope | What to include/exclude |
| **P** | Presentation | Output format |

## When QA Engineers Should Use CRISP
*   ✅ Security testing
*   ✅ Payment flows
*   ✅ Complex validations

---

# 5️⃣ Resources for Learning Prompting (QA-Relevant)

## What Kind of Resources Actually Help QA Engineers?

### ❌ Avoid
*   Generic “AI blogs”
*   Marketing-heavy content
*   Overly academic ML papers

### ✅ Focus on
*   Practical prompt patterns
*   Real examples
*   Iteration & failure cases

## Recommended Resource Categories

### 1. Official LLM Documentation
**Purpose:** Understand capabilities & limits of models.
*   **Examples:** Prompting guides, Model behavior explanations, Safety & limitations
> **📌 Why important for QA:** Helps you not over-trust AI outputs.

### 2. Prompt Pattern Libraries
**Purpose:** Reuse proven prompt structures.
*   **What to look for:** Task → Prompt → Output mapping, Iterative refinement examples

### 3. QA & Testing Communities
**Purpose:** Real-world usage patterns.
*   **Learn from:** How testers use AI for test design, Common mistakes, Automation-friendly prompts

### 4. [prompt guide](https://www.promptingguide.ai/)

### 5. [Github - QA Prompt Library](https://github.com/tayyabakmal1/qa-prompt-library)

### How to Use Resources Effectively
*   Read → don’t copy blindly
*   Adapt prompts to your project
*   Store refined prompts in `/prompts`
*   Version them like code

---

# 6️⃣ Prompt Generators (What They Are & How to Use)

## What Is a Prompt Generator?
**A prompt generator is:**
> A tool or meta-prompt that helps you create better prompts.

**It asks you:**
*   Role?
*   Task?
*   Context?
*   Output format?

## QA Perspective: Are Prompt Generators Useful?
*   ✅ Good for beginners
*   ✅ Avoids missing details
*   ❌ Not production-grade alone

> **📌 Think of them as:** Training wheels for prompting.

### Example: QA Prompt Generator (Manual)
```text
Answer the following to build a QA prompt:

1. What is the application type?
2. What feature needs testing?
3. Who is the user?
4. What type of testing is needed?
5. What output format is required?

Now generate a complete prompt using these answers.
```

---

# 7️⃣ Ready-to-Use QA Prompts (High-Value)
> These are copy-paste + tweak prompts you’ll use daily.

👉 **Refer to:** `prompts/` directory.

---

# 8️⃣ How NOT to Use ChatGPT / AI Tools (Critical for QA)

## ❌ Common Mistakes
*   Blind trust in AI output
*   No validation against requirements
*   Using AI as replacement for QA thinking
*   Feeding incomplete context
*   Overusing AI for trivial tasks

## 🚨 High-Risk Areas
*   Payment logic
*   Security validations
*   Compliance rules
*   Performance assumptions

> **📌 AI is probabilistic, not authoritative.**

## Golden Rule for QA
> **AI suggests — QA decides**

---

# 9️⃣ Prompt Engineering Specifically for QA

## How QA Prompting Is Different

| Generic Prompting | QA Prompting |
| :--- | :--- |
| Creative | Deterministic |
| Open-ended | Constraint-heavy |
| Subjective | Verifiable |
| Free-form | Structured |

## QA-Specific Prompting Principles
*   **Always** define role
*   **Always** define scope
*   **Always** define format
*   Prefer **negative-first** thinking
*   **Validate** output logically