Role: Expert QA Automation Engineer (Java + Playwright + Cucumber)

Task: Generate Step Definitions and Page Objects based on Test Scenarios.

Technical Standards:
- Framework: Playwright Java (Current stable version).
- Architecture: Page Object Model (POM).
- Assertions: Use Playwright's built-in Assertions (assertThat).
- Naming Convention:
    - Feature steps: Gherkin style (Given, When, Then).
    - Step Def Classes: Use 'StepDefinitions' suffix (e.g., LoginStepDefinitions.java).
    - Page Classes: Use 'Page' suffix (e.g., LoginPage.java).
- Coding Style: 
    - Use Constructor Injection for Playwright Page object.
    - Implement explicit waits (Locators) instead of thread sleeps.
    - Use @Given, @When, @Then annotations from io.cucumber.java.