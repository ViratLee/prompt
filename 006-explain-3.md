ได้ไฟล์ทั้งสองชิ้นแล้ว นี่คือภาพรวมว่าทั้งสองทำงานร่วมกันอย่างไร:
agent-test-plan-to-feature.md
│
│  รู้จัก tools: read_file, write_file
│  รู้จัก workflow: 6 ขั้นตอน
│  รู้จัก edge cases
│
└──► เรียกใช้ skill ตรง STEP 3
         │
         ▼
     markdown-to-gherkin.SKILL.md
         │
         │  รู้แค่ conversion rules
         │  Give → Given
         │  Then ที่ 2 → And
         │  Validate checklist
         └──► ไม่รู้จัก tools, ไม่รู้จัก workflow


ได้เลย — ถ้างานมีแค่ขั้นตอนเดียว ไม่ต้องมี Agent เลยก็ได้
เมื่อไหร่ที่ใช้แค่ Skill พอ
❌ ต้องการ Agent เมื่อ...        ✅ Skill พอเมื่อ...
─────────────────────────────    ──────────────────────────────
อ่านไฟล์เอง                      คนส่ง content มาให้แล้ว
ตัดสินใจหลายขั้นตอน              งานชิ้นเดียว input→output
เขียนไฟล์เอง                     คนรับ output ไปใช้เอง
วนซ้ำหลายไฟล์                    แปลงทีละครั้ง
กรณีของคุณ — BA ส่ง markdown มา, ต้องการ .feature กลับไป — Skill อย่างเดียวพอ

วิธีเรียกใช้ Skill โดยตรง
แค่แนบ content ของ markdown-to-gherkin.SKILL.md เป็น system prompt แล้วส่ง markdown ไปใน user message เลย:
┌─────────────────────────────────────────┐
│  SYSTEM PROMPT                          │
│  = markdown-to-gherkin.SKILL.md         │
│    (วาง content ทั้งหมดลงไปตรง ๆ)       │
└─────────────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────┐
│  USER MESSAGE                           │
│  = เนื้อหาของ test-plan-swap.md         │
└─────────────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────┐
│  OUTPUT                                 │
│  = test-swap.feature (Gherkin)          │
└─────────────────────────────────────────┘
ไม่มีชื่อ skill, ไม่มี reference, ไม่มี typo ที่จะผิดพลาด — rules อยู่ใน context โดยตรง         
--------------

ใช่เลย — นั่นแหละคือวิธีที่ถูกต้อง
วิธีใช้ใน IntelliJ + GitHub Copilot Chat
┌─────────────────────────────────────────────────┐
│  IntelliJ Copilot Chat                          │
│                                                 │
│  1. แนบไฟล์ markdown-to-gherkin.SKILL.md        │
│     (Attach file / # reference)                 │
│                                                 │
│  2. แนบไฟล์ test-plan-swap.md                   │
│                                                 │
│  3. พิมพ์ user message                          │
└─────────────────────────────────────────────────┘
User message ที่พิมพ์:
อ่าน test-plan-swap.md และแปลงเป็น Gherkin 
ตามกฎใน markdown-to-gherkin.SKILL.md
แล้วสร้างไฟล์ test-swap.feature

สิ่งที่ควรรู้เกี่ยวกับ Copilot Chat ใน IntelliJ
Copilot Chat ไม่มี "system prompt" แยกต่างหากเหมือน API — ทุกอย่างรวมอยู่ใน context เดียวกัน ดังนั้น:
❌ ไม่มี system prompt แยก
✅ แต่การ attach ไฟล์ = ใส่ content เข้า context ได้ผลเหมือนกัน

ข้อจำกัดที่ต้องระวัง
Copilot อาจไม่สร้างไฟล์ให้อัตโนมัติ — มันจะแสดง Gherkin ใน chat แทน จากนั้นคุณต้อง:
1. Copy output จาก chat
2. สร้างไฟล์ test-swap.feature เอง
3. Paste ลงไป
หรือบอกให้ชัดกว่านี้ว่า:
...แสดงแค่ content ของ test-swap.feature 
ไม่ต้องอธิบายอะไรเพิ่ม

ถ้าอยากให้สร้างไฟล์อัตโนมัติจริง ๆ
ต้องใช้ Copilot Edits (ไม่ใช่ Chat) หรือ plugin อย่าง Continue.dev ที่ให้ Agent มี tool write_file จริง ๆ — แบบนั้นถึงจะครบ loop โดยไม่ต้อง copy/paste เอง