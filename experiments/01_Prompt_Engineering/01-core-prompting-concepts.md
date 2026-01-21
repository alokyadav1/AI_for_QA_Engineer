# Experiment 1: Zero-Shot vs Few-Shot

## Overview
**Goal:** Compare Zero-Shot and Few-Shot prompting for generating test cases.
*   Generate test cases using zero-shot
*   Generate same using few-shot

**Comparison Criteria:**
*   Clarity
*   Reusability
*   Automation readiness

---

## 🧪 Generate test cases using Zero-Shot

### Prompt
```text
generate test case for a "Forgot Password" screen for site: amazon.in
```

### Output
*   **Verify UI Elements:** Check that the page contains the header "Password assistance", an input field for Email or mobile number, and a "Continue" button.
*   **Valid Email:** Enter a registered email address (e.g., user@example.com) and click Continue. Verify that the OTP page is displayed.
*   **Valid Mobile Number:** Enter a registered mobile number (e.g., 9876543210) and click Continue. Verify that the OTP is sent to the phone.
*   **Unregistered Email:** Enter an email address that is not associated with an Amazon account. Check for the error message "We cannot find an account with that email address".
*   **Invalid Format:** Enter text that is not an email or phone number (e.g., $$$) and check for validation errors.
*   **Empty Field:** Leave the field blank and click Continue. Verify the error message "Enter your email or mobile phone number".
*   **Resend OTP:** Verify that the "Resend OTP" link works if the code is not received.

---

## 🧪 Generate same test cases using Few-Shot

### Prompt
```text
Generate test cases for the "Forgot Password" screen on Amazon.in.

Please follow this exact format: ID | Test Scenario | Test Steps | Expected Result

Example 1 (Login Feature): TC_01 | Verify Valid Login | 1. Enter valid email 2. Enter valid password 3. Click Login | User is redirected to homepage.

Example 2 (Search Feature): TC_02 | Verify Empty Search | 1. Leave search bar empty 2. Click Search icon | System shows "Please enter a keyword" message.

Now generate cases for "Forgot Password":
```

### Output
| ID | Test Scenario | Test Steps | Expected Result |
| :--- | :--- | :--- | :--- |
| **TC_FP_01** | Verify UI Elements | 1. Navigate to Forgot Password page<br>2. Observe elements | Page displays "Password assistance" header, Email/Phone input field, and "Continue" button. |
| **TC_FP_02** | Verify Valid Email Flow | 1. Enter registered email (e.g. user@test.com)<br>2. Click Continue | System accepts email and redirects user to the OTP verification screen. |
| **TC_FP_03** | Verify Invalid Format | 1. Enter special characters $$$<br>2. Click Continue | System displays inline error: "Invalid email or mobile number format." |
| **TC_FP_04** | Verify Unregistered Account | 1. Enter non-existent email<br>2. Click Continue | System displays error: "We cannot find an account with that email address." |
| **TC_FP_05** | Verify Empty Input | 1. Leave field blank<br>2. Click Continue | System displays error: "Enter your email or mobile phone number." |

---

## 📊 Analysis

### 1. Zero-Shot
*   🚀 **Faster** to generate
*   📉 **Less control** over output format
*   ⚠️ **Higher chance** of errors

### 2. Few-Shot
*   🎯 **Better control** over output format
*   ✨ **Higher quality** output
*   ⏳ **More time** to generate

> **Why did this happen?** Large Language Models are essentially pattern completion engines.
> *   In **Zero-Shot**, the most common pattern for "give me a list" is a simple bulleted list.
> *   In **Few-Shot**, you established a pattern (a table with specific headers). The model recognized the pattern and completed it.

---

# Experiment 2: Prompt Iteration

**Current Prompt (Baseline):**
```text
generate test case for a 'Forgot Password' screen for site: amazon.in
```

## 🔄 Iteration 1: Adding a Persona
Giving the AI a specific role helps it access the right vocabulary and level of detail. A "User" writes differently than a "Senior QA Engineer."

### Prompt
```text
Act as a "Senior QA Automation Engineer"
generate test case for a 'Forgot Password' screen for site: amazon.in
```

### Output (Persona: Senior QA Automation Engineer)

**Test Strategy: Forgot Password Module (Amazon.in)**

**1. Functional Validation - Positive Flow**
*   **TC_01:** Verify that submitting a valid registered email triggers the OTP generation API.
*   **TC_02:** Verify that submitting a valid registered mobile number redirects to the OTP verification view.

**2. Functional Validation - Negative Flow**
*   **TC_03:** Verify validation logic for non-existent accounts (Ensure strict security: avoid "User not found" enumeration if possible, or verify specific error "We cannot find an account...").
*   **TC_04:** Verify boundary testing for the input field (Max character limit, empty strings).
*   **TC_05:** Inject invalid formats (e.g., SQL injection strings ‘ OR 1=1) to ensure input sanitization handles them gracefully.

**3. UI/UX Verification**
*   **TC_06:** Ensure the "Password assistance" header and "Continue" button are visible and interactive within the DOM.

---

## 🔄 Iteration 2: Adding Format & Constraints
Now, let's lock down the structure. We don't need to give examples (Few-Shot) to get a specific format; we can just describe the format we want.

### Prompt
```text
Act as a "Senior QA Automation Engineer"
Generate test cases for a 'Forgot Password' screen for site: amazon.in
Output the result as a JSON object with keys: id, type, description, and expected_http_status.
```

### Output
```json
{
  "test_cases": [
    {
      "id": "TC_FP_01",
      "type": "Positive",
      "description": "Submit valid registered email address to initiate password reset flow.",
      "expected_http_status": 200
    },
    {
      "id": "TC_FP_02",
      "type": "Positive",
      "description": "Submit valid registered mobile number.",
      "expected_http_status": 200
    },
    {
      "id": "TC_FP_03",
      "type": "Negative",
      "description": "Submit email with invalid format (e.g., 'user@.com').",
      "expected_http_status": 400
    },
    {
      "id": "TC_FP_04",
      "type": "Negative",
      "description": "Submit empty input field.",
      "expected_http_status": 400
    },
    {
      "id": "TC_FP_05",
      "type": "Security",
      "description": "Attempt SQL injection payload in email field.",
      "expected_http_status": 400
    }
  ]
}
```

