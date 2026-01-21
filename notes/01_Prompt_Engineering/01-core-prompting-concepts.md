# 1️⃣ What is Prompting?

## Simple Definition

**Prompting** is the skill of telling an AI exactly what to do, how to do it, and in what format.

> **Think of AI as:** A very intelligent but very literal *junior tester*.

### The Rule
* **Vague instructions** → vague output
* **Clear instructions** → high-quality output

---

## ❌ Bad Prompt Example (QA Context)

> Generate test cases for login

**Why this fails:**
* 🚫 No role
* 🚫 No scope
* 🚫 No format
* 🚫 No constraints

## ✅ Improved Prompt

```text
Act as a Senior QA Engineer.
Generate positive and negative test cases for Login functionality using Email and Password.
Output in Gherkin format.
```

_**Result:** Same AI — completely different quality._

---

## 📌 Key Insight

> **Prompting = controlling AI behavior using language**

---

# 2️⃣ Steps to Learn Prompting (Beginner-Friendly Path)

Instead of random prompting, follow this mental framework every time.

## Step 1: Decide the Role
**Who should the AI act as?**
* QA Engineer
* Automation Engineer
* Security Tester
* Business Analyst

## Step 2: Define the Task
**What exactly do you want?**
* Generate test cases
* Review scenarios
* Find edge cases
* Refactor steps

## Step 3: Provide Context
**Give background info:**
* Application type
* User type (guest, logged-in)
* Platform (web, mobile)

## Step 4: Add Constraints
**Control output quality:**
* Format (Gherkin, table)
* Language style
* Capitalization rules
* Data placeholders

## Step 5: Validate Output
* AI output is not truth, it’s a **draft**
* → QA brain must **validate it**

> **📌 Prompting is iterative, not one-shot.**

---

# 3️⃣ Zero-Shot Prompting

## What It Means
> **Zero-shot** = AI is asked to perform a task **without any example**.

## Structure
1. **Role**
2. **Task**
3. **Constraints** (No sample provided)

## Example (QA)

```text
Act as a QA Engineer.
Generate negative test cases for password reset functionality.
```

**AI relies on:**
* Its general knowledge
* Patterns learned during training

## When QA Engineers Use Zero-Shot
* ✅ Quick test ideas
* ✅ Brainstorming scenarios
* ✅ Exploratory testing support

## Limitations
* ❌ **Output may:**
    * Miss product-specific rules
    * Be generic
    * Assume things incorrectly

> **📌 Rule of Thumb:** Zero-shot = **Speed over Precision**

---

# 4️⃣ Few-Shot Prompting

## What It Means
> **Few-shot** = You give **1–3 examples**, then ask AI to continue in the same pattern.

**AI learns from:**
* Your examples
* Structure
* Language style

## Example (QA – Gherkin)

```gherkin
Example:
Scenario: Successful login
Given User is on login page
When User enters valid email and password
Then User should be logged in successfully

Now generate 3 negative login scenarios in same format.
```

## Why This Works Better
**AI now understands:**
* Format
* Tone
* Level of detail
* Step wording style

## When QA Engineers Should Use Few-Shot
* ✅ Gherkin consistency
* ✅ Step-definition-friendly output
* ✅ Reusable prompts

> **📌 Rule of Thumb:** Few-shot = **Consistency + Control**

# 5️⃣ Chain-of-Thought Prompting (CoT)

## What It Is (Beginner Explanation)
**Chain-of-Thought prompting** asks the AI to:
> **Think step by step** before giving the final answer.

Instead of jumping to an output, the AI reasons internally in logical steps.

> **📌 Think of it as asking a Senior QA:**
> “Explain your thinking before concluding.”

## Why This Matters for QA Engineers
**QA work is logic-heavy:**
* Test coverage decisions
* Edge-case analysis
* Root cause analysis
* Scenario derivation from requirements

**Chain-of-Thought improves:**
* Accuracy
* Completeness
* Logical consistency

## Simple Example (QA)

### ❌ Without CoT
> Generate test cases for password validation.

**Output:** Random, generic list.

### ✅ With CoT
```text
Analyze password validation rules step by step.
Identify boundary conditions, negative cases, and security concerns.
Then generate test cases.
```

**Output:**
* Length boundaries
* Special characters
* Reuse of old passwords
* Injection attempts

> **📌 Key Insight:** CoT improves **thinking quality**, not just formatting.

## When QA Engineers Should Use CoT
* ✅ Complex business rules
* ✅ Payment flows
* ✅ Authorization & role logic
* ✅ Bug root-cause analysis

## When NOT to Use
* ❌ Simple formatting tasks
* ❌ Rewriting steps
* ❌ Basic data generation

---

# 6️⃣ Role-Based Prompting

## What It Is
**Role-Based Prompting** tells the AI who it should behave as.

**AI changes:**
* Vocabulary
* Depth
* Perspective
* Risk awareness

> **📌 Same question → different output based on role.**

## Example

### ❌ No Role
> Generate test cases for checkout.

**Result:** Very generic, shallow coverage.

### ✅ With Role
```text
Act as a Senior E-commerce QA Engineer with experience in payment systems.
```

**Result:**
* Payment failures
* Timeouts
* Duplicate orders
* Inventory sync issues

## Common QA Roles You Can Use
* Manual QA Engineer
* Automation Engineer
* Performance Tester
* Security Tester
* QA Lead
* SDET

## Why Role-Based Prompting Is Critical
1. AI does not know your expectations unless you specify them.
2. **Role = Context + Experience + Mindset**