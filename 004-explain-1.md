# Prompt Engineering: Skill vs Agent

อธิบายความแตกต่างและการทำงานร่วมกันผ่านตัวอย่างจริง

---

## 🧩 Skill Prompt คืออะไร?

**Skill** คือ prompt ที่สอน AI ให้ทำ **งานชิ้นเดียวได้ดีมาก** — มี input ชัด, output ชัด, ไม่ตัดสินใจเอง

```
┌─────────────────────────────────────────────────────┐
│                    SKILL PROMPT                     │
│                                                     │
│  "แปลง Test Scenario ใน Markdown                    │
│   ให้เป็น Gherkin (.feature file)"                  │
│                                                     │
│  INPUT  → test-plan.md (markdown scenarios)         │
│  OUTPUT → test.feature (Gherkin syntax)             │
│                                                     │
│  ❌ ไม่ตัดสินใจ ❌ ไม่อ่านไฟล์เอง                    │
│  ✅ แปลงได้ถูกต้อง ✅ format ตรงสเปก                │
└─────────────────────────────────────────────────────┘
```

### ตัวอย่าง Skill Prompt

```
You are a QA engineer. Convert the given Test Scenarios 
written in Markdown into valid Gherkin syntax (.feature file).

Rules:
- Each "scenario X." becomes a `Scenario:` block
- "Give/Given" → Given, "When" → When, "Then" → Then
- Fix grammar and capitalize step keywords
- Wrap everything in a Feature block named after the file

Input: Markdown test plan text
Output: Only the .feature file content, nothing else
```

---

## 🤖 Agent Prompt คืออะไร?

**Agent** คือ prompt ที่ให้ AI **วางแผนและทำหลายขั้นตอนเอง** — อ่านไฟล์, ตัดสินใจ, เรียก tool, วนซ้ำจนเสร็จ

```
┌─────────────────────────────────────────────────────┐
│                    AGENT PROMPT                     │
│                                                     │
│  "อ่าน test-plan-swap.md แล้วสร้าง                  │
│   test-swap.feature ให้ฉัน"                         │
│                                                     │
│  STEP 1: read_file("test-plan-swap.md")  ← tool     │
│  STEP 2: คิดว่าต้องแปลงยังไง           ← reasoning  │
│  STEP 3: เรียก skill แปลง              ← delegate   │
│  STEP 4: write_file("test-swap.feature") ← tool     │
│                                                     │
│  ✅ ตัดสินใจเอง ✅ ใช้ tool ✅ จัดการ flow          │
└─────────────────────────────────────────────────────┘
```

### ตัวอย่าง Agent Prompt

```
You are a QA automation agent. You have access to tools: 
read_file, write_file, list_files.

Your job:
1. Read the file: test-plan-swap.md
2. Extract all test scenarios
3. Convert them to Gherkin using the conversion rules below
4. Write the result to: test-swap.feature
5. Report what you did

[conversion rules — embedded skill]
- Each scenario → Scenario: block
- Fix "Give" → Given, keep When/Then
...

Do not ask for confirmation. Complete all steps autonomously.
```

---

## ⚙️ ทั้งสองทำงานร่วมกันอย่างไร?

```
USER: "อ่าน test-plan-swap.md แล้วสร้าง test-swap.feature"
         │
         ▼
┌─────────────────────┐
│      AGENT          │  ← ควบคุม flow ทั้งหมด
│                     │
│  1. read_file() ────┼──→ ได้ markdown content
│                     │
│  2. วิเคราะห์ ───── ┼──→ พบ 3 scenarios
│                     │
│  3. เรียก SKILL ────┼──→ แปลงเป็น Gherkin
│     (conversion)    │
│                     │
│  4. write_file() ───┼──→ test-swap.feature ✅
└─────────────────────┘
```

---

## 📄 ผลลัพธ์จากตัวอย่างของคุณ

Input (`test-plan-swap.md`) → Output (`test-swap.feature`):

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
    Then an error message should be displayed 
    And the swap should not proceed
```

> **Skill** แก้ไข "Give" → `Given`, รวม `And` ที่ถูกต้อง, จัดรูปแบบ Gherkin  
> **Agent** เป็นคนอ่านไฟล์ → ส่งให้ skill → เขียนไฟล์ผลลัพธ์

---

## 🔑 สรุปความต่าง

| | Skill | Agent |
|---|---|---|
| **หน้าที่** | ทำงานชิ้นเดียวให้ดี | ควบคุม flow หลายขั้นตอน |
| **ตัดสินใจ** | ❌ ไม่ตัดสินใจ | ✅ ตัดสินใจเอง |
| **ใช้ Tool** | ❌ | ✅ read/write file, API |
| **วนซ้ำ** | ❌ | ✅ loop จนงานเสร็จ |
| **เปรียบเหมือน** | ช่างฝีมือ | Project Manager |

**กฎง่าย ๆ:** เขียน **Skill** ก่อนเสมอ → แล้วให้ **Agent** เรียกใช้ Skill เมื่อต้องการ automation