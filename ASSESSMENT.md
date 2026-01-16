<p align="center">
<img src="https://jobs.justice.gov.uk/portal/13/images/logo--default.svg">
</p>
<h2 align="center">HM Courts and Tribunal Service: Technical Assessment</h2>

## Project Overview

This project implements a test automation framework using **Cypress** with **Cucumber BDD** to test the login functionality of a web application. The framework is designed to test the login page on "the-internet.herokuapp.com", covering both positive and negative test scenarios.

## Technology Stack

- **Test Framework**: Cypress (latest version)
- **BDD Framework**: @badeball/cypress-cucumber-preprocessor
- **Build Tool**: @bahmutov/cypress-esbuild-preprocessor
- **Language**: JavaScript (ES6+)
- **Test Application**: https://the-internet.herokuapp.com/login

## Project Structure

```
dts-test-automation-challenge/
├── cypress/
│   ├── e2e/
│   │   ├── login/
│   │   │   └── steps.spec.cy.js     
│   │   └── login.feature    
│   ├── fixtures/
│   │   └── selectors.json          
│   └── support/
│       ├── commands.js              
│       └── e2e.js                  
├── cypress.config.js               
├── package.json                    
└── ASSESSMENT.md                   
```

## What Has Been Tested

### Test Scenarios Implemented

The framework includes comprehensive test coverage for login functionality:

#### 1. **Positive Test Scenarios** (@positive tag)
   - **Successful Login**: Validates that a user with correct credentials (username: "tomsmith", password: "SuperSecretPassword!") can successfully log in and see the success message "You logged into a secure area!"
   - **Successful Logout**: Verifies that after logging in, a user can successfully log out and see the logout confirmation message "You logged out of the secure area!"

#### 2. **Negative Test Scenarios** (@negative tag)
   - **Invalid Username**: Tests that entering an incorrect username with a valid password displays the error message "Your username is invalid!"
   - **Invalid Password**: Tests that entering a valid username with an incorrect password displays the error message "Your password is invalid!"
   - **Unauthorized Access**: Validates that attempting to access the secure area without logging in shows the message "You must login to view the secure area!"

#### 3. **Background Scenario**
   - **Page Accessibility and Content Verification**: Ensures the login page is accessible and displays all expected elements including:
     - Page title "Login Page"
     - Username field label
     - Password field label
     - Login button
     - Instructional text

### Test Execution Approach

- **BDD Methodology**: Tests are written in Gherkin syntax using feature files, making them readable by both technical and non-technical stakeholders
- **Scenario Outline**: Used for parameterized testing of multiple invalid credential combinations
- **Tag-based Organization**: Scenarios are tagged with @positive and @negative for easy filtering and execution
- **Reusable Step Definitions**: Common actions are abstracted into reusable step definitions

## Benefits of the Implementation

### 1. **Maintainability**
   - **Centralized Selectors**: All CSS selectors are stored in `selectors.json`, making it easy to update selectors when the application changes without modifying test code
   - **Reusable Steps**: Step definitions can be reused across multiple scenarios, reducing code duplication
   - **BDD Approach**: Feature files serve as living documentation that clearly describe the expected behavior

### 2. **Readability**
   - **Gherkin Syntax**: Test scenarios are written in plain English, making them understandable to business stakeholders, product owners, and developers
   - **Clear Test Structure**: Each scenario follows the Given-When-Then pattern, clearly defining preconditions, actions, and expected outcomes

### 3. **Scalability**
   - **Modular Design**: The framework structure allows for easy addition of new features and test scenarios
   - **Fixture-based Configuration**: Selectors and test data can be easily extended for additional pages and scenarios

### 4. **Reporting**
   - **Cucumber Reports**: Configured to generate both JSON and HTML reports for test execution results
   - **Test Traceability**: Feature files provide clear documentation of what is being tested

### 5. **Best Practices**
   - **Explicit Waits**: Uses Cypress's built-in retry-ability and explicit visibility checks (`.should('be.visible')`)
   - **Assertions**: Proper assertions are in place to validate expected outcomes
   - **Error Handling**: Basic error handling implemented in step definitions (e.g., switch statement with default error case)

## Design Choices and Rationale

### 1. **Cypress Framework Selection**
   - **Rationale**: Cypress provides excellent developer experience with built-in waiting mechanisms, automatic retries, and real-time test execution visibility
   - **Benefits**: Fast execution, easy debugging, and comprehensive documentation

### 2. **Cucumber BDD Integration**
   - **Rationale**: BDD approach bridges the gap between technical and non-technical team members
   - **Benefits**: Tests serve as executable specifications, improving collaboration and understanding

### 3. **Selector Externalization**
   - **Rationale**: Storing selectors in JSON fixtures separates test logic from implementation details
   - **Benefits**: Easier maintenance when UI changes, reduces code duplication

### 4. **Configuration Choices**
   - **Base URL**: Centralized base URL configuration for easy environment switching
   - **Viewport Size**: Set to 1530x960 for consistent test execution
   - **Chrome Web Security**: Disabled to allow testing across different domains if needed
   - **Default Command Timeout**: Set to 10 seconds for handling slower network conditions

### 5. **Custom Command**
   -  **Decoupled Steps**: Login steps seem common but it is decoupled to establish what step triggered the error
   -  **Message Verification**: This step is common so creating a custom command seem appropriate to verify it.

