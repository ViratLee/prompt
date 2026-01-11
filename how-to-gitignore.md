## ตัวอย่าง `.gitignore` สำหรับ Sensitive Prompts

```gitignore
# ============================================
# GitHub Copilot & AI Prompts - Sensitive Data
# ============================================

# Ignore prompts ที่มีข้อมูลส่วนตัวหรือความลับ
.github/copilot-instructions.private.md
.copilot/secrets.md
.copilot/api-keys.md
.copilot/credentials.md

# Ignore ทั้ง folder prompts ที่เป็นส่วนตัว
docs/copilot-prompts/private/
prompts/sensitive/
.ai-prompts/local/

# Ignore files ที่มี pattern เฉพาะ
*-private.md
*-secret.md
*-local.md
*.private.prompt
*.secret.prompt

# Ignore backup files ของ prompts
*.md.backup
*.prompt.bak
```

## โครงสร้าง Folder แนะนำ

```
your-project/
├── .github/
│   ├── copilot-instructions.md          # ✅ Commit (public guidelines)
│   └── copilot-instructions.private.md  # ❌ Ignore (sensitive info)
│
├── .copilot/
│   ├── general-guidelines.md            # ✅ Commit
│   ├── team-standards.md                # ✅ Commit
│   ├── api-keys.md                      # ❌ Ignore
│   └── internal-apis.md                 # ❌ Ignore
│
└── docs/
    └── copilot-prompts/
        ├── public/                       # ✅ Commit
        │   ├── coding-style.md
        │   └── testing-guide.md
        └── private/                      # ❌ Ignore ทั้ง folder
            ├── company-secrets.md
            └── client-specific.md
```

## ตัวอย่างเนื้อหาที่ควร Ignore

### ❌ ไม่ควร Commit

**api-keys.md** (ควร ignore)
```markdown
# Internal API Information

## Production API
- Endpoint: https://internal-api.company.com
- API Key: sk_live_xxxxxxxxxxxxx
- Database: prod-db.internal

## Customer Data
- Client ABC credentials: admin@abc.com / [password]
```

**client-specific.md** (ควr ignore)
```markdown
# Client XYZ Implementation

## Business Logic
- Special discount: 25% for VIP customers
- Payment gateway: Stripe account sk_xxxxx
- Admin credentials: [sensitive data]
```

### ✅ ควร Commit

**coding-style.md** (safe to commit)
```markdown
# Coding Standards

## General Guidelines
- Use Kotlin data classes for DTOs
- Follow REST API conventions
- Write unit tests for all services

## Code Review Checklist
- [ ] Tests coverage > 80%
- [ ] No hardcoded values
- [ ] Proper error handling
```

## .gitignore แบบ Advanced

```gitignore
# ============================================
# AI Prompts Management
# ============================================

# Ignore by file pattern
**/*-private.*
**/*-secret.*
**/*-internal.*
**/credentials.*
**/secrets.*

# Ignore specific folders anywhere in project
**/private/
**/secrets/
**/sensitive/
**/.local/

# Ignore files with sensitive keywords
**/copilot-*-prod.md
**/copilot-*-staging.md
**/prompt-*-customer.md

# But keep template files
!**/template-*.md
!**/example-*.md

# Ignore environment-specific prompts
.copilot/.env.local
.copilot/prompts.local.json

# Ignore generated prompts from tools
.copilot/auto-generated/
**/copilot-cache/
```

## วิธีใช้งานที่ดี

### 1. แยก Public และ Private Prompts

**copilot-instructions.md** (public)
```markdown
# General Project Guidelines

Use the coding standards in this project.
Refer to private instructions for sensitive details.
```

**copilot-instructions.private.md** (ignored)
```markdown
# Private Instructions - DO NOT COMMIT

## Production Database
- Host: prod-db.internal.company.com
- Credentials: [stored in vault]

## API Keys
- Stripe: sk_live_xxxxx
- AWS: AKIA...
```

### 2. ใช้ Environment Variables Reference

แทนที่จะเขียน:
```markdown
Database: postgresql://user:password@host/db
```

ให้เขียน:
```markdown
Database: Use ${DATABASE_URL} from environment
API Key: Use ${STRIPE_API_KEY} from .env file
```

### 3. สร้าง Template File

**prompts/template-private.md** (commit this)
```markdown
# Template for Private Prompts

Copy this to `private.md` and fill in:

## API Configuration
- Endpoint: [YOUR_API_ENDPOINT]
- API Key: [YOUR_API_KEY]

## Database
- Connection: [YOUR_DB_CONNECTION]
```

## เช็คว่า Ignore ถูกต้อง

```bash
# ดูว่า git track files อะไรบ้าง
git ls-files | grep copilot

# เช็คว่า file ถูก ignore หรือไม่
git check-ignore -v .copilot/secrets.md

# ดู status ของ untracked files
git status --ignored
```

## ถ้าเผลอ Commit ไปแล้ว

```bash
# ลบ file ออกจาก git แต่เก็บไว้ใน local
git rm --cached .copilot/secrets.md

# เพิ่มใน .gitignore
echo ".copilot/secrets.md" >> .gitignore

# Commit การเปลี่ยนแปลง
git add .gitignore
git commit -m "Remove sensitive prompts from git"
```

## Best Practices

✅ **ควรทำ:**
- แยก public/private prompts ตั้งแต่แรก
- ใช้ naming convention ที่ชัดเจน (เช่น `-private`, `-secret`)
- สร้าง template files สำหรับทีม
- Document ใน README ว่า files ไหนควร ignore

❌ **ไม่ควรทำ:**
- เก็บ API keys, passwords ใน prompts
- Commit customer/client specific information
- Hardcode production URLs หรือ credentials
- เผลอ commit แล้วค่อยลบทีหลัง

การจัดการ sensitive prompts ที่ดีจะช่วยป้องกันการ leak ข้อมูลสำคัญครับ!