ดูโครงสร้าง skill ที่มีอยู่แล้ว เพื่อเขียน skill ของเราในรูปแบบเดียวกันCreated a file, read a fileCreated a file, read a fileนี่คือ markdown-to-gherkin.SKILL.md ที่สร้างขึ้น โครงสร้างของ Skill file ประกอบด้วย:
Front Matter — name และ description บอก Agent ว่าควรเรียก skill นี้เมื่อไหร่
Conversion Rules — กฎการแปลงที่ชัดเจน เช่น Give → Given, ซ้ำ Scenario → เรียงใหม่, Then ตัวที่ 2 → And
Full Example — Input/Output จริงจากตัวอย่างของคุณ เพื่อให้ AI เห็น pattern ชัดเจน
Validation Checklist — เช็คก่อน save ว่า output ถูกต้องครบ
Naming Convention — บอก output filename ให้ Agent รู้ว่าต้องตั้งชื่อไฟล์ว่าอะไร

เมื่อ Agent อ่าน skill นี้ก่อน มันจะรู้ทันทีว่า:

ต้องแปลงยังไง (rules)
output ควรหน้าตาเป็นอย่างไร (example)
ตั้งชื่อไฟล์ว่าอะไร (naming)

โดย Agent ไม่ต้อง "เดา" เองเลย