มีหลายวิธีเลยครับ ขึ้นอยู่กับ tool ที่ใช้

---

## GitHub Copilot (VS Code / IntelliJ)

**วิธีที่คุณใช้อยู่แล้ว**
- แนบไฟล์ `.md` แล้ว reference ใน chat

**วิธีอื่นๆ ใน VS Code**

1. **`.github/copilot-instructions.md`** — Copilot จะอ่านไฟล์นี้ **อัตโนมัติ** ทุกครั้งที่ใช้งาน เหมาะสำหรับ project-level instructions ที่ใช้ซ้ำบ่อย

2. **`#file:` reference ใน chat** — พิมพ์ `#file:create-method-to-get-Diffrence-TimeZone.md` ใน Copilot Chat โดยตรง

3. **VS Code Prompt Files** (`.prompt.md`) — ใหม่มากๆ ใน Copilot นำไฟล์ไปไว้ใน `.github/prompts/` แล้วเรียกด้วย `/` slash command หรือ `#` reference ใน chat

---

## Cursor / Windsurf (ถ้าคุณใช้เพิ่มเติม)

- **`.cursorrules`** หรือ **`.cursorules`** — อ่านอัตโนมัติทุก session
- **`@file`** reference ใน chat

---

## แนะนำ Structure สำหรับ Project ของคุณ

```
/src/.github/
  ├── copilot-instructions.md        ← global rules (อ่านอัตโนมัติ)
  └── prompts/
      ├── create-method-timezone.prompt.md
      └── create-class-for-test.prompt.md
```

วิธีที่คุ้มค่าที่สุดคือแยก **global instructions** (coding style, project overview) ไปไว้ใน `copilot-instructions.md` แล้วให้ task-specific prompt อยู่แยกไฟล์ — จะได้ไม่ต้องแนบทุกครั้ง