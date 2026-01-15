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

### 4. **ESBuild Preprocessor**
   - **Rationale**: Fast bundling and modern JavaScript support
   - **Benefits**: Quick test execution and support for ES6+ syntax

### 5. **Configuration Choices**
   - **Base URL**: Centralized base URL configuration for easy environment switching
   - **Viewport Size**: Set to 1530x960 for consistent test execution
   - **Chrome Web Security**: Disabled to allow testing across different domains if needed
   - **Default Command Timeout**: Set to 10 seconds for handling slower network conditions

## Improvements That Could Be Made (Given More Time)

### 1. **Page Object Model (POM) Implementation**
   - **Current State**: Selectors are externalized but not organized into page objects
   - **Improvement**: Create dedicated page object classes for each page (LoginPage, SecureAreaPage) to encapsulate page-specific logic and selectors
   - **Benefit**: Better code organization, easier maintenance, and improved reusability

### 2. **Custom Commands Enhancement**
   - **Current State**: `commands.js` file exists but is empty
   - **Improvement**: Implement custom Cypress commands for common actions like:
     - `cy.login(username, password)` - Reusable login command
     - `cy.logout()` - Reusable logout command
     - `cy.verifyMessage(message)` - Standardized message verification
   - **Benefit**: Reduces code duplication and improves test readability

### 3. **Test Data Management**
   - **Current State**: Test data is hardcoded in feature files
   - **Improvement**: 
     - Create a separate test data file (JSON or JavaScript) for managing test credentials
     - Implement data-driven testing with external data sources
     - Support for multiple test environments (dev, staging, prod)
   - **Benefit**: Easier test data maintenance and environment-specific testing

### 4. **Enhanced Logging and Reporting**
   - **Current State**: Basic Cucumber reporting configured
   - **Improvement**:
     - Add detailed logging for test execution steps
     - Integrate with reporting tools like Allure or Mochawesome
     - Add screenshots on test failures
     - Implement video recording for test runs
   - **Benefit**: Better debugging capabilities and comprehensive test reports

### 5. **Error Handling and Retry Logic**
   - **Current State**: Basic error handling in step definitions
   - **Improvement**:
     - Implement retry logic for flaky tests
     - Add more comprehensive error messages
     - Create custom error types for different failure scenarios
   - **Benefit**: More robust tests and easier troubleshooting

### 6. **CI/CD Integration**
   - **Current State**: No CI/CD configuration
   - **Improvement**:
     - Add GitHub Actions or Jenkins pipeline configuration
     - Implement automated test execution on pull requests
     - Add test result notifications
   - **Benefit**: Automated testing in the development workflow

### 7. **Additional Test Coverage**
   - **Current State**: Focus on login functionality only
   - **Improvement**:
     - Add edge cases (empty fields, special characters, SQL injection attempts)
     - Implement accessibility testing
     - Add visual regression testing
     - Test responsive design on different viewport sizes
   - **Benefit**: More comprehensive test coverage

### 8. **Environment Configuration**
   - **Current State**: Single base URL configuration
   - **Improvement**:
     - Create environment-specific configuration files
     - Support for multiple environments (dev, staging, production)
     - Environment variable management
   - **Benefit**: Easy switching between test environments

### 9. **Test Execution Optimization**
   - **Current State**: Sequential test execution
   - **Improvement**:
     - Configure parallel test execution
     - Implement test sharding for faster execution
     - Add test prioritization (critical tests run first)
   - **Benefit**: Reduced test execution time

### 10. **API Testing Integration**
   - **Current State**: UI-only testing
   - **Improvement**:
     - Add API testing for backend validation
     - Test authentication tokens and session management
     - Validate API responses before UI testing
   - **Benefit**: Faster feedback and more comprehensive testing

### 11. **Test Utilities and Helpers**
   - **Current State**: Basic step definitions
   - **Improvement**:
     - Create utility functions for common operations
     - Add helper methods for data generation
     - Implement test data cleanup utilities
   - **Benefit**: Code reusability and cleaner test code

### 12. **Documentation**
   - **Current State**: Basic README
   - **Improvement**:
     - Add detailed setup instructions
     - Document all custom commands and utilities
     - Create a test execution guide
     - Add troubleshooting section
   - **Benefit**: Easier onboarding for new team members

## Conclusion

This test automation framework provides a solid foundation for testing login functionality using modern tools and best practices. The BDD approach makes tests readable and maintainable, while the Cypress framework ensures reliable and fast test execution. The framework is well-structured and can be easily extended to cover additional functionality and scenarios.

The implementation demonstrates proficiency in:
- **Programming**: Clean JavaScript code with ES6+ features
- **Test Automation Frameworks**: Effective use of Cypress and Cucumber
- **Web Application Testing**: Comprehensive coverage of login scenarios
- **Best Practices**: Selector externalization, reusable steps, and clear test structure

With the suggested improvements, the framework would become even more robust, maintainable, and suitable for enterprise-level test automation.