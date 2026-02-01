สำหรับ GitHub Copilot การนำ Agentic Design Patterns มาใช้ทำได้ผ่านไฟล์ **`.github/copilot-instructions.md`** (ระดับ Repo) หรือไฟล์ **`.agent.md`** (สำหรับสร้าง Specialized Agents)

นี่คือตัวอย่างไฟล์ Markdown ที่ถูกออกแบบมาเพื่อกระตุ้นให้ Copilot ทำงานแบบ "Agent" (มีการวางแผน, คิดทบทวน และตรวจสอบตัวเอง) ครับ

---

### ตัวอย่างไฟล์: `.github/copilot-instructions.md`

ไฟล์นี้จะช่วยเปลี่ยนจาก Copilot ที่ "เขียนตามสั่ง" ให้กลายเป็น "Partner ที่ช่วยคิด"

```markdown
# Agentic Coding Instructions

You are an expert software engineer agent. When assisting with this repository, follow these agentic design patterns:

## 1. Planning & Chain-of-Thought
Before writing any code for complex tasks, you MUST:
- Analyze the existing codebase and dependencies.
- Output a **"Proposed Plan"** in a checkbox list format.
- Wait for user confirmation or feedback before proceeding with large implementations.

## 2. Reflection & Self-Correction
- After generating code, perform a "Self-Review".
- Check for common pitfalls: memory leaks, edge cases, and security vulnerabilities (SQLi, XSS).
- If you find a better way to implement the logic, provide the refined version and explain why.

## 3. Tool Use & Context
- Always check `@workspace` to understand the project structure.
- Use `ls` or `find` (via Terminal/Copilot) if you are unsure where a file is.
- Prioritize using existing utility functions defined in `src/utils` instead of rewriting them.

## 4. Coding Standards (Example: TypeScript/Node.js)
- **Strict Typing:** Always use interfaces; avoid `any`.
- **Error Handling:** Use `try-catch` blocks with meaningful error messages and logging.
- **Testing:** Every new feature must include a corresponding Vitest unit test in the `tests/` directory.

## 5. Output Format
For every significant change, use this structure:
### 🧐 Analysis
(Briefly describe the problem and context)
### 📝 Plan
- [ ] Task 1...
- [ ] Task 2...
### 💻 Implementation
(The code block)
### 🧪 Verification
(How should I test this?)

```

---

### วิธีนำไปใช้งาน

1. **สร้าง Folder:** สร้างโฟลเดอร์ `.github` ที่ root ของโปรเจกต์ (ถ้ายังไม่มี)
2. **สร้างไฟล์:** สร้างไฟล์ชื่อ `copilot-instructions.md` ไว้ข้างใน
3. **เปิดใช้งานใน VS Code:** * ไปที่ **Settings** (Cmd+,)
* ค้นหา `github.copilot.chat.codeGeneration.useInstructionFiles`
* ติ๊กถูกเพื่อเปิดใช้งาน


4. **Specialized Agents (Option):** หากคุณต้องการสร้าง Agent เฉพาะทาง (เช่น `@test-agent`) ให้สร้างไฟล์ไว้ที่ `.github/agents/test-agent.agent.md` โดยใช้โครงสร้างคล้ายกัน แต่ระบุบทบาทให้ชัดเจนว่าเป็น QA Engineer ครับ

### แหล่งรวม Template เพิ่มเติม

คุณสามารถเข้าไปดูคอลเลกชันคำสั่งเทพๆ (Instructions) ที่รวบรวมโดย Community ได้ที่:

* [GitHub: awesome-copilot](https://github.com/github/awesome-copilot) (มีไฟล์ตัวอย่างครอบคลุมทุกภาษา)
* [Agents.md](https://agents.md/) (มาตรฐานใหม่สำหรับกึ่งๆ README ของ AI Agents)

อยากให้ผมช่วยปรับแต่ง Instructions สำหรับภาษาโปรแกรมหรือ Framework ไหนเป็นพิเศษไหมครับ? (เช่น React, Python, หรือ Go)