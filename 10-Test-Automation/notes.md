# Notes

## What is Test Automation?

Test Automation is the process of executing software tests automatically using testing tools and frameworks instead of performing them manually.

It helps verify that an application works as expected after every code change and is a critical component of Continuous Integration (CI) and Continuous Delivery (CD).

---

# Why Test Automation?

Without Test Automation:

- Manual testing is time-consuming.
- Bugs may go unnoticed.
- Releases are slower.
- Human errors are more likely.

With Test Automation:

- Faster feedback
- Consistent testing
- Early bug detection
- Improved software quality
- Faster software delivery

---

# Test Automation Workflow

```text
Developer
     │
     ▼
Write Code
     │
     ▼
Git Commit
     │
     ▼
Git Push
     │
     ▼
Jenkins Pipeline
     │
     ▼
Build Application
     │
     ▼
Run Automated Tests
     │
     ▼
Generate Test Reports
     │
     ▼
Deploy (If Tests Pass)
```

---

# Types of Automated Tests

## Unit Testing

Tests individual methods or functions.

Examples:

- JUnit
- TestNG
- PyTest
- NUnit

---

## Integration Testing

Tests communication between multiple components.

Example:

```text
Application
      │
      ▼
Database
```

---

## Functional Testing

Tests complete application functionality based on business requirements.

Examples:

- Selenium
- Cypress
- Playwright

---

## Regression Testing

Ensures new code changes do not break existing functionality.

Regression tests are commonly executed before production deployments.

---

## Smoke Testing

A quick set of tests that verifies whether the application's critical functionality works correctly after deployment.

---

# Popular Testing Frameworks

| Language | Framework |
|-----------|-----------|
| Java | JUnit |
| Java | TestNG |
| Python | PyTest |
| JavaScript | Jest |
| JavaScript | Cypress |
| C# | NUnit |

---

# Jenkins Test Pipeline

```text
Source Code
      │
      ▼
Checkout
      │
      ▼
Build
      │
      ▼
Run Tests
      │
      ▼
Generate Reports
      │
      ▼
Archive Reports
      │
      ▼
Deploy
```

---

# Test Reports

After tests finish, Jenkins generates reports showing:

- Passed tests
- Failed tests
- Skipped tests
- Execution time
- Error details

JUnit reports are commonly displayed inside Jenkins.

---

# Test Results

Typical test outcomes:

| Result | Meaning |
|----------|----------|
| Passed | Test completed successfully |
| Failed | Test detected a problem |
| Skipped | Test was intentionally not executed |
| Error | Test could not complete due to an unexpected issue |

---

# Code Coverage

Code Coverage measures how much of the application's source code is executed during automated testing.

Common coverage metrics include:

- Line Coverage
- Branch Coverage
- Function Coverage
- Statement Coverage

Higher coverage improves confidence but does not guarantee bug-free software.

---

# Benefits of Test Automation

- Faster testing
- Reduced manual effort
- Repeatable test execution
- Early defect detection
- Improved software quality
- Better Continuous Integration
- Faster software releases

---

# Best Practices

- Write independent test cases.
- Keep test data separate from test logic.
- Run tests after every build.
- Fail the pipeline if critical tests fail.
- Generate readable test reports.
- Keep automated tests fast and reliable.
- Maintain test scripts alongside application code.

---

# Common Challenges

- Flaky tests
- Slow execution
- Poor test maintenance
- Environment differences
- Dependency failures
- Incomplete test coverage
- Unstable test data

---

# Test Automation in CI/CD

```text
Git Push
     │
     ▼
Jenkins
     │
     ▼
Build
     │
     ▼
Automated Tests
     │
     ▼
Reports
     │
     ▼
Deploy
```

Automated testing ensures only verified code progresses through the pipeline.

---

# Manual Testing vs Test Automation

| Feature | Manual Testing | Test Automation |
|----------|----------------|-----------------|
| Speed | Slow | Fast |
| Repeatability | Limited | Excellent |
| Human Error | Higher | Lower |
| Scalability | Limited | High |
| CI/CD Integration | Difficult | Easy |

---

# Interview Questions

### What is Test Automation?

Test Automation is the use of tools and frameworks to execute software tests automatically without manual intervention.

---

### Why is Test Automation important in CI/CD?

It provides fast feedback, detects defects early, improves software quality, and prevents faulty code from progressing through the pipeline.

---

### What is the difference between Unit Testing and Integration Testing?

Unit Testing verifies individual components in isolation, while Integration Testing verifies interactions between multiple components.

---

### What is Code Coverage?

Code Coverage measures the percentage of application code executed during testing, helping identify untested areas of the codebase.

---

### Why are JUnit reports used in Jenkins?

JUnit reports allow Jenkins to display test results, including passed, failed, and skipped tests, making it easier to analyze build quality.

---

# Key Takeaways

- Test Automation is an essential practice in Continuous Integration and Continuous Delivery.
- Automated tests improve software quality by identifying issues early.
- Jenkins integrates with frameworks such as JUnit, TestNG, and PyTest to execute tests automatically.
- Test reports and code coverage help evaluate application quality.
- Reliable automated testing enables safer and faster software releases.