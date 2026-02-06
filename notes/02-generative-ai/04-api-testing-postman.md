# API Testing with Postman (Fakestore Scenario)

## 1. Introduction to API Testing

API Testing is a process of sending requests to an API and analyzing the responses to verify than the API is working as expected under various conditions.


## 2. Types of API Testing

Focus on these four in your daily work:

1.  **Functional**: "Does it work?" (e.g., Create User -> Verify User in DB).
2.  **Negative**: "Does it fail correctly?" (e.g., Create User with existing email -> Expect 409 Conflict).
3.  **Security**: "Am I allowed?" (e.g., Access Admin data as a Guest).
4.  **Load**: "Can it handle the crowd?" (e.g., 1000 users hitting search simultaneously).

## 3. What is usually tested in API?

Do not just check "it works". Check these 5 pillars:

1.  **Status Codes**: The HTTP standard signal (200 success, 400 bad request, 500 server error).
2.  **Response Payload**: Is the data accurate? (e.g., Is the price correct? Is the ID unique?)
3.  **Headers**: Are content-type (`application/json`) and auth tokens present?
4.  **Performance**: Did the response return in < 500ms?
5.  **Error Handling**: If I send a string instead of a number, does the API fail gracefully or crash?
6.  **Schema Validation**: Does the response match the expected structure?
7. **Data Integrity**: Is the data consistent across the system?
8. **Security**: Are authentication and authorization working correctly?

## 4. QA Mentality while testing APIs

- **Trust Nothing**: A `200 OK` status does NOT mean the feature works. The body might say `{"error": "failed"}`.
- **The UI is a Liar**: The UI might mask API errors. Test the raw response.
- **Break the Schema**: Send integers where strings are expected. Send empty JSONs. The API should handle it, not crash.
- **Validate the Negative**: 50% of your tests should be negative (Invalid IDs, missing tokens, bad data).

## Real QA Problem

You are the QA Engineer for an E-commerce platform. The Backend Team has released a new "Product Management" API.
They claim it's stable, but you need to verify:

1.  **Latency**: Does the product list load fast enough?
2.  **Integrity**: When we add a product, does the API actually confirm the correct data?
3.  **Automation**: Can we run these checks automatically on every deployment?

Using the UI is not an option (it's not built yet). You must verify this using **Postman**.

## Goal

Create a **Postman Collection** for `fakestoreapi.com` that:

1.  Retrieves the product catalog.
2.  Adds a new item to the catalog.
3.  Validates response data using automated scripts (JavaScript).
4.  Runs as a complete regression suite.

## Setup

- **Tool**: Postman (Desktop App or Web).
- **Target**: [FakeStoreAPI](https://fakestoreapi.com/).
- **Workspace**: Create a Collection named `FakeStore_QE`.
- **Directory**: Ensure this folder exists for your artifacts:
  ```powershell
  mkdir -p "experiments/03-postman"
  ```

## Step-by-Step Actions

### Step 1: Set Up Global Variables

Don't hardcode URLs. Use variables to switch between Dev, Staging, and Prod easily.

1.  In Postman, look for the **Eye Icon** (top right) or **Environments** on the left.
2.  Create a generic global variable (or Environment):
    - **Variable**: `baseUrl`
    - **Initial Value**: `https://fakestoreapi.com`
    - **Current Value**: `https://fakestoreapi.com`
3.  Click **Save**.

### Step 2: Smoke Test - Get All Products

Verify the API is up and serving data.

1.  **Create Request**:
    - **Name**: `Get All Products`
    - **Method**: `GET`
    - **URL**: `{{baseUrl}}/products`
2.  **Scripts** (Click the **Scripts** tab):

    ```javascript
    // 1. Basic Smoke Check
    pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
    });

    // 2. Performance Check (SLA)
    pm.test("Response time is acceptable (< 2s)", function () {
      pm.expect(pm.response.responseTime).to.be.below(2000);
    });

    // 3. Schema Check
    var jsonData = pm.response.json();
    pm.test("Response is a non-empty list", function () {
      pm.expect(jsonData).to.be.an("array");
      pm.expect(jsonData.length).to.be.above(0);
    });
    ```

3.  **Send** and verify "Test Results" (3/3 Pass).

### Step 3: Regression Test - Add Product

Verify that the POST endpoint accepts data and mirrors it back correctly.

1.  **Create Request**:
    - **Name**: `Add New Product`
    - **Method**: `POST`
    - **URL**: `{{baseUrl}}/products`
2.  **Body**:
    - Choose **raw** -> **JSON**.
    - Payload:
      ```json
      {
        "title": "QA AI Handbook",
        "price": 13.5,
        "description": "A guide to modern QA",
        "image": "https://i.pravatar.cc",
        "category": "electronic"
      }
      ```
3.  **Tests**:

    ```javascript
    var jsonData = pm.response.json();

    // 1. Check if ID was generated
    pm.test("New Product ID generated", function () {
      pm.expect(jsonData).to.have.property("id");
      // Save this ID for future use (if the API supported persistence)
      pm.collectionVariables.set("created_product_id", jsonData.id);
    });

    // 2. Data Integrity Check
    pm.test("Correct Product Title returned", function () {
      pm.expect(jsonData.title).to.eql("QA AI Handbook");
    });
    ```

    _(Note: FakestoreAPI is a mock. It returns the ID `21` usually, but doesn't persist the data to the database. This test validates the **handshake**.)_

### Step 4: Run the Suite (UI)

1.  Select the `FakeStore_QE` collection in the sidebar.
2.  Click **Run** (or "Run Collection").
3.  Uncheck "Persist Responses" (optional).
4.  Click **Run FakeStore_QE**.
5.  **Result**: You should see a report confirming all requests passed.

### Step 5: Run via CLI (Newman)

**Introduction**: [Newman](https://www.npmjs.com/package/newman) is the command-line runner for Postman. Any test you build in the UI can be run here. This is mandatory for CI/CD (Jenkins, GitHub Actions, etc.).

**Setup**:

1.  Ensure **Node.js** is installed.
2.  Install Newman globally:
    ```powershell
    npm install -g newman
    ```

**Action**:

1.  **Export** your collection from Postman (Right Click Collection -> Export -> Collection v2.1).
2.  Save it to: `experiments/03-postman/fakestore-tests.postman_collection.json`.
3.  Run the test from your VS Code terminal:

    ```powershell
    # Option 1: If baseUrl is missing, override it explicitly (COMMON FIX)
    newman run experiments/03-postman/fakestore-tests.postman_collection.json --env-var "baseUrl=https://fakestoreapi.com"

    # Option 2: If you have an exported environment file
    # newman run experiments/03-postman/fakestore-tests.postman_collection.json -e your_env_file.json
    ```

4.  **Validation**: You should see the same "Pass" results in your terminal.

### Step 6: Generate Reports (Reporters)

The CLI output is good for logs, but stakeholders need HTML reports.

1.  **Install the HTML Extra Reporter** (The standard HTML reporter is too basic, use this one):
    ```powershell
    npm install -g newman-reporter-htmlextra
    ```
2.  **Run with Reporter**:
    ```powershell
    newman run experiments/03-postman/fakestore-tests.postman_collection.json -r htmlextra
    ```
3.  **View Report**:
    - A `newman` folder will be created in your current directory.
    - Open the `.html` file inside it to see a beautiful dashboard of your test run.

## Validation Checklist

- [ ] `Get All Products` returns Status 200.
- [ ] `Add New Product` returns the created JSON object with an `id`.
- [ ] Collection Runner (UI) shows all tests passed (Green).
- [ ] **Newman** (CLI) runs the collection and passes all tests.
- [ ] **HTML Report** is generated in the `newman/` folder.
- [ ] URLs use the `{{baseUrl}}` variable, not hardcoded strings.

## Online Resources for Deep Dive

- **Official Postman Docs**: [Writing Tests](https://learning.postman.com/docs/writing-scripts/test-scripts/)
- **Newman Docs**: [Running Collections in CLI](https://learning.postman.com/docs/collections/using-newman-cli/command-line-integration-with-newman/)
- **HTML Extra Reporter**: [Newman Reporter HTML Extra](https://www.npmjs.com/package/newman-reporter-htmlextra)
- **Fakestore Docs**: [API Endpoints](https://fakestoreapi.com/docs)
- **Assertion Library**: [ChaiJS BDD](https://www.chaijs.com/api/bdd/) (Postman uses Chai under the hood)

## Git Artifacts

Export your collection and save it to git.

- **File**: `experiments/03-postman/fakestoreAPI.postman_collection.json`

For more information on Postman, visit [Postman Documentation](https://learning.postman.com/docs/)

For Learning API Testing, visit [Postman API Testing Tutorial](https://academy.postman.com/path/api-testing-path)

API Testing Basics [API Testing Basics](https://www.postman.com/api-platform/api-testing/)