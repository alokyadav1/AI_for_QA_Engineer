## Zero shot prompting

```
Act as a Senior QA Engineer.
Generate test cases for the 'Forgot Password' screen on Amazon.in.

Please follow this exact format: ID | Test Scenario | Test Steps | Expected Result

Now generate cases for "Forgot Password":
```
## Few Shot prompting
```
Act as a Senior QA Engineer.
Generate test cases for the 'Forgot Password' screen on Amazon.in.

Please follow this exact format: ID | Test Scenario | Test Steps | Expected Result

Example 1 (Login Feature): TC_01 | Verify Valid Login | 1. Enter valid email 2. Enter valid password 3. Click Login | User is redirected to homepage.

Example 2 (Search Feature): TC_02 | Verify Empty Search | 1. Leave search bar empty 2. Click Search icon | System shows "Please enter a keyword" message.

Now generate cases for "Forgot Password":
```

## Chain of thought prompting / Role based

```
Act as a Senior QA Engineer.

Think step by step and analyze the functionality carefully.
Identify:
- Business rules
- Positive scenarios
- Negative scenarios
- Boundary conditions
- Edge cases

After the analysis, generate test cases in Gherkin format.
Do not skip reasoning steps.

```

### Role + Few Shot + CoT

```
Act as a Senior QA Engineer.

Think step by step before answering.

Example Scenario:
Scenario: Successful login
Given User is on login page
When User enters valid credentials
Then User should be logged in

Now analyze the login functionality and generate:
- Negative scenarios
- Boundary scenarios
- Security-related scenarios

Follow the same Gherkin format.

```