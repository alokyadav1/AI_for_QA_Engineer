## Professional Test Case Generation Prompt

```
You are an expert QA engineer. Generate comprehensive test cases for a login functionality.

Requirements:
- Username: Email format, max 100 characters
- Password: 8-20 characters, must include uppercase, lowercase, number, special character
- "Remember Me" checkbox (optional)
- "Forgot Password" link
- Login button
- Session timeout: 30 minutes
- Max login attempts: 3 (account locks after 3 failed attempts)

Generate test cases in the following format for each case:
- Test Case ID
- Test Title
- Priority (High/Medium/Low)
- Preconditions
- Test Steps (numbered)
- Test Data
- Expected Result
- Test Type (Positive/Negative/Edge)

Include:
1. Positive test cases (valid scenarios)
2. Negative test cases (invalid inputs)
3. Boundary value testing
4. Security testing scenarios
5. UI/UX validation
6. Accessibility considerations

Format output as a markdown table.
```

## E-commerce Product Search
```
Generate test cases for an e-commerce product search feature:

Features:
- Search bar (accepts text, max 200 characters)
- Auto-suggestion (shows top 5 suggestions while typing)
- Filters: Price range, Category, Brand, Rating
- Sort options: Price (low to high, high to low), Popularity, Rating
- Results display: Grid view (default), List view
- Pagination: 20 items per page

Requirements:
- Search should handle special characters
- Minimum 3 characters to trigger auto-suggestion
- No results should show "No products found" message
- Filters are cumulative (can apply multiple)

Generate 15 test cases covering all functionality.
```

## Shopping Cart

```
Act as a senior QA engineer. Create test cases for shopping cart functionality.

User Stories:
- As a user, I can add items to cart
- As a user, I can update quantity
- As a user, I can remove items
- As a user, I can see cart total
- As a user, I can apply discount codes

Constraints:
- Max quantity per item: 10
- Cart expires after 24 hours
- Discount codes are case-insensitive
- Only one discount code per order

Provide test cases in Gherkin format (Given-When-Then).
```