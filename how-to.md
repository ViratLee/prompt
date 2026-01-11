สำหรับการใช้ GitHub Copilot ใน IntelliJ IDE มีวิธีจัดการ prompt files หลายแบบ:

## 1. GitHub Copilot Instructions (แนะนำ)
วาง file `.github/copilot-instructions.md` ในโปรเจคของคุณ:

```
your-project/
├── .github/
│   └── copilot-instructions.md
└── src/
```

Copilot จะอ่าน file นี้อัตโนมัติเมื่อทำงานในโปรเจค คุณสามารถใส่:
- Coding standards ของทีม
- Architecture patterns ที่ใช้
- Best practices เฉพาะโปรเจค
- Naming conventions

## 2. Workspace-specific Instructions
สร้าง `.copilot/` folder ในโปรเจค:

```
your-project/
├── .copilot/
│   ├── instructions.md
│   ├── api-guidelines.md
│   └── testing-guide.md
└── src/
```

## 3. การใช้ Prompt Files แบบ Modular

สร้าง folder สำหรับเก็บ prompts แยกตามหมวดหมู่:

```
your-project/
├── docs/
│   └── copilot-prompts/
│       ├── backend-patterns.md
│       ├── frontend-standards.md
│       ├── testing-templates.md
│       └── database-queries.md
```

แล้วอ้อถึงใน chat โดย:
- พิมพ์ `#file` แล้วเลือก file ที่ต้องการ
- หรือ drag & drop file เข้า Copilot Chat

## 4. ตัวอย่าง copilot-instructions.md

```markdown
# Project Coding Guidelines

## Tech Stack
- Backend: Kotlin + Spring Boot
- Database: PostgreSQL
- Testing: JUnit 5 + MockK

## Code Style
- ใช้ data classes สำหรับ DTOs
- Repository pattern สำหรับ database access
- Service layer ต้องมี interface

## Naming Conventions
- Controllers: `*Controller.kt`
- Services: `*Service.kt`, `*ServiceImpl.kt`
- Repositories: `*Repository.kt`

## Testing
- Unit tests ต้องครอบคลุม 80%
- ใช้ `@MockkBean` สำหรับ mocking
```

## 5. Tips เพิ่มเติม

- **Context Files**: ใช้ `#codebase` ใน Copilot Chat เพื่อให้มันสแกนทั้งโปรเจค
- **Inline Chat**: กด `Ctrl+I` (Windows/Linux) หรือ `Cmd+I` (Mac) เพื่อเปิด inline chat พร้อมอ้างถึง file
- **.gitignore**: อย่าลืม ignore sensitive prompts ถ้ามีข้อมูลที่ไม่ควร commit

คุณต้องการตัวอย่าง template สำหรับงานประเภทไหนเป็นพิเศษไหม?