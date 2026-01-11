## วิธีใช้ `#codebase` ใน GitHub Copilot Chat

`#codebase` ช่วยให้ Copilot วิเคราะห์ทั้งโปรเจคเพื่อตอบคำถามที่เกี่ยวข้องกับ codebase ของคุณ

## ตัวอย่างการใช้งาน

### 1. **ถามเกี่ยวกับ Architecture**
```
#codebase อธิบาย architecture ของโปรเจคนี้
```
Copilot จะวิเคราะห์โครงสร้าง folder, dependencies, และบอกว่าใช้ pattern อะไร

### 2. **หา Implementation ที่มีอยู่แล้ว**
```
#codebase มีการ implement authentication อยู่แล้วหรือยัง? อยู่ file ไหน?
```
ช่วยหาว่ามี feature ที่ต้องการอยู่แล้วหรือไม่

### 3. **ถามเกี่ยวกับ Database Schema**
```
#codebase แสดง database schema ทั้งหมดที่ใช้ในโปรเจค
```
Copilot จะหา entity classes, migrations, หรือ schema definitions

### 4. **หาตัวอย่างการใช้งาน**
```
#codebase ให้ตัวอย่างวิธีเรียกใช้ UserService ที่มีอยู่ในโปรเจค
```
ดูวิธีใช้ class หรือ function ที่มีอยู่แล้ว

### 5. **วิเคราะห์ Dependencies**
```
#codebase libraries อะไรบ้างที่ใช้สำหรับ HTTP client?
```
หา dependencies ที่เกี่ยวข้อง

### 6. **Code Review แบบ Context-Aware**
```
#codebase ช่วยตรวจสอบว่า API endpoints ทั้งหมดมี error handling ครบหรือไม่
```
วิเคราะห์ code quality ตาม context ของโปรเจค

### 7. **สร้าง Code ตาม Pattern ที่มี**
```
#codebase สร้าง ProductController ใหม่ตาม pattern ของ UserController ที่มีอยู่
```
Copilot จะดูตัวอย่างที่มีและสร้างให้ตาม style เดียวกัน

### 8. **หา TODO หรือ Incomplete Code**
```
#codebase มี TODO comments หรือ functions ที่ยังไม่ implement อยู่ที่ไหนบ้าง?
```

### 9. **Migration Guide**
```
#codebase ถ้าจะ upgrade Spring Boot จาก 2.x เป็น 3.x ต้องแก้อะไรบ้าง?
```
วิเคราะห์ผลกระทบจากการเปลี่ยน version

### 10. **Generate Documentation**
```
#codebase สร้าง API documentation สำหรับ REST endpoints ทั้งหมด
```

## Tips การใช้งาน

✅ **ใช้เมื่อไร:**
- ต้องการ context จากหลาย files
- ถามเกี่ยวกับโครงสร้างโปรเจค
- ต้องการสร้าง code ที่สอดคล้องกับ codebase ที่มี

⚠️ **ข้อจำกัด:**
- โปรเจคใหญ่มากอาจใช้เวลาในการสแกน
- อาจไม่เห็น files ที่อยู่ใน `.gitignore`
- ความแม่นยำขึ้นกับขนาดและความซับซ้อนของโปรเจค

## เปรียบเทียบกับ Options อื่น

- `#file` - อ้างถึง specific file เดียว
- `#codebase` - สแกนทั้งโปรเจค
- ไม่ใส่อะไร - ใช้แค่ context จาก file ที่เปิดอยู่

ลองใช้ `#codebase` ถามอะไรเกี่ยวกับโปรเจคของคุณดูได้เลย มันจะช่วยประหยัดเวลาค้นหา code มากครับ!