# Requirement Analysis Guide

This guide provides detailed instructions for extracting requirements from Gherkin scenarios and mapping them to test cases.

## Analysis Process

### Step 1: Parse Gherkin Scenarios

For each scenario in the user story, identify:
- **Given**: Preconditions (setup/context)
- **When**: Actions (user interactions/triggers)
- **Then**: Expected outcomes (assertions/results)

### Step 2: Extract Requirements

Break down each scenario into discrete, testable requirements:

**Example scenario:**
```gherkin
Scenario: User submits login form
Given the user is on the login page
When the user enters valid credentials
And clicks the login button
Then the dashboard is displayed
And a welcome message appears
```

**Extracted requirements:**
1. System should accept valid credentials in login form
2. Login button should trigger authentication
3. System should navigate to dashboard on successful login
4. System should display welcome message after login

### Step 3: Map Requirements to Test Cases

Combine related requirements into efficient test cases:

**Strategy 1: Sequential Flow**
If requirements follow a natural sequence, combine them:
- Requirement 1 + 2 + 3 + 4 → "Verify Successful Login Flow" (single test case)

**Strategy 2: Isolated Testing**
If requirements need separate validation:
- Requirement 1 → "Verify Credential Input"
- Requirement 2 → "Verify Login Button Functionality"
- Requirement 3 → "Verify Dashboard Navigation"
- Requirement 4 → "Verify Welcome Message Display"

**Prefer Strategy 1 when possible** to minimize test case count while maintaining coverage.

## Requirement Numbering

Use hierarchical numbering: `<Scenario>.<Requirement>.<TestCase>`

**Example:**
```
Scenario 1: Login validation
  1.1 Email field should accept valid format
    1.1.1 Verify email validation with valid input
    1.1.2 Verify email validation with invalid input
  1.2 Password field should be masked
    1.2.1 Verify password masking
```

## Table Format

### Requirements Analysis Table

```
| Scenario Name | Requirement | Test Case |
|---------------|-------------|-----------|
| Scenario 1: <Name> | 1.1 <First requirement> | 1.1.1 <Test case title> |
|  | 1.2 <Second requirement> | 1.2.1 <Test case title> |
|  |  | 1.2.2 <Another test case for same requirement> |
|
| Scenario 2: <Name> | 2.1 <First requirement> | 2.1.1 <Test case title> |
```

**Formatting rules:**
- Use empty cells (`|  |`) to continue requirements/test cases
- Use empty row with just `|` to separate scenarios
- Keep requirement descriptions action-oriented
- Keep test case titles clear and specific

### Detailed Test Cases Table

```
| Test Case ID | Test Scenario | Expected Result | Test Data |
|--------------|---------------|-----------------|-----------|
| 1.1.1 | Enter valid email in email field | Email is accepted and validation passes | user@example.com |
| 1.1.2 | Enter invalid email in email field | Validation error message is displayed | invalid-email |
```

**Guidelines:**
- Test Case ID matches the numbering from requirements table
- Test Scenario describes the action being tested
- Expected Result is specific and verifiable
- Test Data lists required input (use "N/A" if none needed)

## Combining Requirements Examples

### Example 1: UI Element Validation

**Multiple requirements:**
- Button should exist
- Button should be enabled
- Button should have correct color
- Button should have correct label

**Combined test case:**
"Verify Submit Button Properties"
1. Observe submit button
2. Check button is enabled
3. Verify button color matches design
4. Verify button label is correct

### Example 2: Field Validation

**Multiple requirements:**
- Field should accept input
- Field should validate format
- Field should show error on invalid input
- Field should clear error on valid input

**Combined test case:**
"Verify Email Field Validation Flow"
1. Enter text in email field
2. Enter invalid email format
3. Observe validation error message
4. Enter valid email format
5. Verify error message disappears

### Example 3: Navigation Flow

**Multiple requirements:**
- User can click navigation link
- System navigates to target page
- Target page displays correct content
- Navigation history is updated

**Combined test case:**
"Verify Dashboard Navigation from Login"
1. Click dashboard link
2. Observe page navigation
3. Verify dashboard content is displayed
4. Verify browser URL updated

## Anti-Patterns

### ❌ Over-granular test cases
Creating separate test cases for every small aspect:
- "Verify button exists"
- "Verify button color"
- "Verify button enabled state"
- "Verify button label"

### ✅ Better approach
One comprehensive test case:
- "Verify button properties" (checks existence, color, state, label in one test)

### ❌ Under-specified requirements
Vague requirement descriptions:
- "System should work correctly"
- "Button should function"
- "Page should load"

### ✅ Better approach
Specific, testable requirements:
- "System should display validation error when email format is invalid"
- "Submit button should trigger form submission when clicked"
- "Login page should load within 2 seconds"

## Quality Checklist

Before finalizing requirement analysis:
- [ ] All Gherkin scenarios are represented
- [ ] Each requirement is testable and specific
- [ ] Requirements are numbered hierarchically
- [ ] Test cases combine requirements where logical
- [ ] Test case count is minimized without sacrificing coverage
- [ ] Requirement descriptions are clear and action-oriented
- [ ] Test case titles clearly indicate what is being tested
- [ ] Tables are properly formatted with empty cells and separators
