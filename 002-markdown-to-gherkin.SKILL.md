---
name: markdown-to-gherkin
description: "Use this skill when you need to convert test scenarios written in Markdown (e.g., from a Business Analyst's test plan) into valid Gherkin syntax (.feature files). Triggers include: any mention of '.feature file', 'Gherkin', 'BDD scenarios', 'test plan to feature', or when a user uploads/references a test-plan.md and wants a .feature output. Also use when fixing malformed Given/When/Then steps, restructuring informal QA notes into structured test cases, or generating Cucumber/Behave/SpecFlow-compatible feature files. Do NOT use for unit test generation, pytest, Jest, or any code-based test frameworks."
---

# Markdown Test Plan → Gherkin Feature File

## Overview

Business Analysts often write test scenarios in free-form Markdown. This skill converts
that content into valid Gherkin `.feature` files compatible with Cucumber, Behave, and SpecFlow.

## Quick Reference

| Task | Approach |
|------|----------|
| Read test plan | Parse Markdown headings and bullet steps |
| Convert scenarios | Map each `### scenario N.` → `Scenario:` block |
| Fix step keywords | Normalize Give/Given/When/Then/And |
| Write output | Save as `<name>.feature` |

---

## Conversion Rules

### 1. Feature Block

The top-level `Feature:` name comes from the file name or the first `##` heading in the Markdown.

```gherkin
Feature: Token Swap
```

### 2. Scenario Mapping

Each `### scenario N. <Title>` in Markdown becomes a `Scenario:` block.

```markdown
### scenario 1. Token Swap Functionality   →   Scenario: Token Swap Functionality
```

### 3. Step Keyword Normalization

| Markdown (raw) | Gherkin (corrected) | Rule |
|----------------|---------------------|------|
| `Give ...`     | `Given ...`         | Typo fix: "Give" → "Given" |
| `Given ...`    | `Given ...`         | Keep as-is |
| `When ...`     | `When ...`          | Keep as-is |
| `Then ...`     | `Then ...`          | Keep as-is |
| Multiple `Then`| `And ...`           | Second+ Then in same block → And |
| Multiple `Given`| `And ...`          | Second+ Given in same block → And |

### 4. Duplicate Scenario Numbers

If the Markdown contains duplicate `### scenario N.` numbers (a common BA mistake),
keep all scenarios — do **not** drop duplicates. Renumber them sequentially in output.

```markdown
### scenario 2. Cancel swap     →   Scenario: Cancel swap before confirmation
### scenario 2. Swap error      →   Scenario: Swap with insufficient balance
```

### 5. Trailing Punctuation & Capitalization

- Remove trailing periods from step text
- Capitalize the first word of each step after the keyword
- Trim extra whitespace

---

## Full Conversion Example

**Input: `test-plan-swap.md`**

```markdown
## Test Scenarios

### scenario 1. Token Swap Functionality
Give open swap page
Then fill in valid token amounts
When I click the swap button
Then the swap should be executed successfully and balances updated

### scenario 2. Cancel swap before confirmation
Given I have filled in valid token amounts
When I click the cancel button before confirming the swap
Then the swap should be cancelled and no changes to balances should occur

### scenario 2. Swap with insufficient balance - error displayed
Given I have filled in token amounts that exceed my balance
When I click the swap button
Then an error message should be displayed indicating insufficient balance and the swap should not proceed
```

**Output: `test-swap.feature`**

```gherkin
Feature: Token Swap

  Scenario: Token Swap Functionality
    Given I open the swap page
    And I fill in valid token amounts
    When I click the swap button
    Then the swap should be executed successfully
    And balances should be updated

  Scenario: Cancel swap before confirmation
    Given I have filled in valid token amounts
    When I click the cancel button before confirming the swap
    Then the swap should be cancelled
    And no changes to balances should occur

  Scenario: Swap with insufficient balance - error displayed
    Given I have filled in token amounts that exceed my balance
    When I click the swap button
    Then an error message should be displayed indicating insufficient balance
    And the swap should not proceed
```

---

## Step-by-Step Instructions

### Step 1: Parse the Markdown

Read the input file and identify:
- The file name (used for `Feature:` label if no top-level heading)
- All `### scenario N. <Title>` blocks
- The step lines under each block (lines starting with Give/Given/When/Then)

### Step 2: Normalize Each Scenario

For each scenario block:
1. Extract the title after `scenario N.`
2. Collect all step lines
3. Apply keyword normalization table above
4. Convert consecutive same-keyword steps to `And`

### Step 3: Write the Feature File

```
Feature: <name>
<blank line>
  Scenario: <title>
    <step keyword> <step text>
    ...
<blank line>
  Scenario: ...
```

Indentation: 2 spaces for `Scenario:`, 4 spaces for steps.

### Step 4: Validate

Check the output against these rules before saving:

- [ ] Exactly one `Feature:` at the top
- [ ] No duplicate `Scenario:` names
- [ ] Every scenario has at least one `Given`, one `When`, one `Then`
- [ ] No bare `Give` (must be `Given`)
- [ ] No step starts with a lowercase letter
- [ ] File ends with a newline

---

## Common BA Writing Mistakes & How to Fix Them

| Mistake | Fix |
|---------|-----|
| `Give` instead of `Given` | Auto-correct to `Given` |
| Steps out of order (Then before When) | Reorder: Given → When → Then |
| Duplicate scenario numbers | Renumber sequentially |
| Missing `Given` (jumps straight to `When`) | Infer context or flag for review |
| Run-on `Then` with multiple assertions | Split into `Then` + `And` |
| Scenario title has trailing period | Remove period |

---

## Output File Naming

| Input file | Output file |
|------------|-------------|
| `test-plan-swap.md` | `test-swap.feature` |
| `test-plan-login.md` | `test-login.feature` |
| `qa-scenarios-checkout.md` | `test-checkout.feature` |

Rule: strip `test-plan-` or `qa-scenarios-` prefix, replace with `test-`, change extension to `.feature`.

---

## Dependencies

- No external libraries required
- Compatible output with: Cucumber (Java/JS/Ruby), Behave (Python), SpecFlow (.NET), Godog (Go)
