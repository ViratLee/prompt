สำหรับการใช้งานใน **IntelliJ IDEA** การตั้งค่าจะต่างจาก VS Code เล็กน้อยครับ เนื่องจาก IntelliJ ใช้ระบบที่เรียกว่า **"Custom Instructions"** ซึ่งปัจจุบัน GitHub Copilot รองรับการอ่านไฟล์จากโปรเจกต์โดยตรงแล้ว (Update ล่าสุดในปี 2025-2026)

คุณสามารถทำได้ **3 วิธี** ดังนี้ครับ:

---

### วิธีที่ 1: ใช้ไฟล์มาตรฐาน (แนะนำที่สุด)

IntelliJ ของเวอร์ชันปัจจุบันสามารถอ่านไฟล์คำสั่งที่วางไว้ในโปรเจกต์ได้โดยอัตโนมัติ:

1. สร้างไฟล์ชื่อ `.github/copilot-instructions.md` ไว้ที่ **Root ของ Project**
2. วางเนื้อหา Java 17 + Playwright ที่ผมให้ไว้ก่อนหน้านี้ลงไป
3. **Restart IntelliJ** หรือทำการ **Sign out/Sign in** GitHub Copilot ใหม่เพื่อให้มันโหลด Context ของไฟล์นี้ขึ้นมา
4. เมื่อคุณเริ่มพิมพ์ใน Chat หรือใช้ Inline Completion ตัว Copilot จะเห็นไฟล์นี้เป็น "Context" และปฏิบัติตามกฎทันที

---

### วิธีที่ 2: ตั้งค่าผ่านหน้า Settings (สำหรับคุมทุกไฟล์)

หากคุณต้องการให้กฎนี้ใช้กับทุกโปรเจกต์ที่เปิดใน IntelliJ หรือไฟล์ `.md` ไม่ทำงาน:

1. ไปที่ **Settings** (หรือ `Cmd + ,` บน Mac / `Ctrl + Alt + S` บน Windows)
2. ไปที่ **Languages & Frameworks** > **GitHub Copilot**
3. มองหาช่อง **Custom Instructions** (ถ้าเวอร์ชันของคุณรองรับจะมีช่อง Text Box ขนาดใหญ่ให้ใส่)
4. Copy เนื้อหาจากไฟล์ Markdown ไปวางในช่องนั้นแล้วกด **OK**

---

### วิธีที่ 3: ใช้ฟีเจอร์ "Context Selection" (เฉพาะหน้า)

หากคุณต้องการเน้นย้ำกฎบางอย่างขณะแชท (Copilot Chat):

1. เปิดหน้าต่าง **GitHub Copilot Chat** (ปกติอยู่ด้านขวา)
2. เปิดไฟล์ `.github/copilot-instructions.md` ค้างไว้ใน Editor
3. ในช่อง Chat ให้พิมพ์ `#` แล้วเลือกชื่อไฟล์ `copilot-instructions.md` หรือพิมพ์ว่า `@workspace follow the instructions in .github/copilot-instructions.md`
4. หลังจากนั้นค่อยสั่งงาน เช่น *"Create a new cucumber step def for login functionality"*

---

### ข้อควรระวังสำหรับ Java + IntelliJ

* **Version Compatibility:** ตรวจสอบว่า Plugin **GitHub Copilot** ใน IntelliJ ของคุณเป็นเวอร์ชันล่าสุดเสมอ เพราะฟีเจอร์การอ่านไฟล์ Instruction ใน IntelliJ มักจะมาหลัง VS Code เสมอ
* **Indexing:** หาก IntelliJ ยัง Index โปรเจกต์ไม่เสร็จ Copilot อาจจะไม่เห็นไฟล์ Instructions ให้รอจนแถบ Loading ด้านล่างขวาหายไปก่อนครับ
* **Project Structure:** ตรวจสอบว่าโปรเจกต์ของคุณตั้งค่า **Project SDK** เป็น Java 17 จริงๆ (ไปที่ `File > Project Structure`) เพื่อให้ Copilot แนะนำ Syntax ที่ถูกต้องตามที่กำหนดไว้ใน Instruction
