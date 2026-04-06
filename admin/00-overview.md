# Admin / Knowledge Manager — คู่มือผู้ใช้งาน

## ภาพรวม

คู่มือนี้ครอบคลุมการตั้งค่าและการดูแลข้อมูลหลัก (Master Data) ใน TAM3D MES บทบาท Admin มีสิทธิ์เข้าถึงทุกโมดูลอย่างเต็มรูปแบบ รวมถึงโมดูล Knowledge (ข้อมูลหลัก) และการตั้งค่า System หากข้อมูลหลักไม่ได้รับการกำหนดค่าอย่างถูกต้อง โมดูลอื่นจะไม่สามารถทำงานได้ — นี่คือชั้นพื้นฐานของระบบ

> **ผู้ใช้งาน:** ผู้ดูแลระบบ (System Administrator) ที่ตั้งค่าการใช้งานระบบใหม่ และผู้จัดการข้อมูลหลัก (Knowledge Manager) ที่ดูแลข้อมูลหลักในการดำเนินงานประจำวัน

---

### การนำทาง (Navigation)

Admin ทำงานข้ามสองส่วนในแถบด้านข้าง (Sidebar):

**Knowledge** (ข้อมูลหลัก):

| หมวดย่อย | หน้า | วัตถุประสงค์ |
|-----------|------|-------------|
| Basic Data (ข้อมูลพื้นฐาน) | Material, Process Definition, Process Route, Customer, Operator | ข้อมูลหลักที่ทุกอย่างต้องอ้างอิงถึง |
| Factory Modeling (การจำลองโรงงาน) | Factory hierarchy (ลำดับชั้นโรงงาน) | Workshop, Production Line, Workstation |
| Equipment Modeling (การจำลองเครื่องจักร) | Equipment Type, Maintenance Type, Maintenance Strategy, Abnormal Reason, Abnormal Reason Category, Equipment (instances) | การกำหนดเครื่องจักรและการตั้งค่าการบำรุงรักษา |
| Tooling (เครื่องมือตัด) | Tool Category, Tool Definition, Tool Instance | วงจรชีวิตเครื่องมือตัด CNC |
| Quality Modeling (การจำลองคุณภาพ) | Inspection items, defect categories | การตั้งค่าคุณภาพ |
| Schedule Modeling (การจำลองตารางเวลา) | Shifts, work calendar, schedule parameters | ชั่วโมงทำงานและการตั้งค่าตารางเวลา |
| Asset Modeling (การจำลองทรัพย์สิน) | Asset categories | การจำแนกทรัพย์สิน |
| Knowledge Health (สุขภาพข้อมูลหลัก) | Health dashboard | คะแนนความสมบูรณ์ของข้อมูลหลัก |

**System** (สำหรับ Admin เท่านั้น):

| หน้า | วัตถุประสงค์ |
|------|-------------|
| System Overview (ภาพรวมระบบ) | ศูนย์กลางเชื่อมต่อไปยังโมดูลย่อย |
| Factory Template (เทมเพลตโรงงาน) | สร้างข้อมูลหลักจากเทมเพลตอุตสาหกรรม |
| Users (ผู้ใช้งาน) | สร้างผู้ใช้งาน กำหนดบทบาท จัดการสิทธิ์การเข้าถึง |
| Running Numbers (เลขลำดับอัตโนมัติ) | กำหนดรูปแบบรหัสที่สร้างอัตโนมัติ |
| Company Settings (การตั้งค่าบริษัท) | ข้อมูลบริษัทและการสร้างแบรนด์ |

[image: sidebar-knowledge-system — ภาพหน้าจอแถบด้านข้างแสดงส่วน Knowledge และ System ที่ขยายเต็ม]

---

### ห่วงโซ่การอ้างอิงข้อมูล (Entity Dependency Chain)

ข้อมูลหลักต้องสร้างตามลำดับที่กำหนด เนื่องจากข้อมูลแต่ละรายการมีการอ้างอิงถึงกัน:

```
ระดับ 1 (ไม่มีการอ้างอิง):
  Materials, Customers, Equipment Types, Tool Categories,
  Abnormal Reason Categories, Maintenance Types

ระดับ 2 (อ้างอิงจากระดับ 1):
  Process Definitions (→ Equipment Type)
  Equipment Instances (→ Equipment Type)
  Tool Definitions (→ Tool Category)
  Operators (ไม่มีการอ้างอิง แต่จำเป็นสำหรับตารางกะ)
  Abnormal Reasons (→ Abnormal Reason Category)
  Maintenance Strategies (→ Maintenance Type)

ระดับ 3 (อ้างอิงจากระดับ 2):
  Process Routes (→ Process Definitions)
  Tool Instances (→ Tool Definition)
  Shifts & Work Calendar (กะทำงานและปฏิทินทำงาน)

ระดับ 4 (อ้างอิงจากระดับ 3):
  Quotes & Sales Orders (→ Customers, Process Definitions)
  Work Orders (→ Process Routes, Materials)
  Schedule Assignments (→ Equipment, Shifts)
  Shift Roster (→ Operators, Equipment, Shifts)
```

[image: dependency-chain — แผนภาพแสดงลำดับชั้นการอ้างอิงข้อมูล]

---

### ลำดับการตั้งค่าสำหรับระบบใหม่

สำหรับระบบที่ติดตั้งใหม่ ให้ปฏิบัติตามลำดับนี้:

1. **Factory Template** (ทางลัดเสริม) — สร้างข้อมูลจากเทมเพลต CNC HMLV
2. **Materials** (วัสดุ) — วัสดุที่ใช้ในการผลิต (Al 6061-T6, SS 304 เป็นต้น)
3. **Equipment Types** (ประเภทเครื่องจักร) — หมวดหมู่เครื่องจักร (CNC Lathe, 5-Axis Mill เป็นต้น)
4. **Equipment Instances** (เครื่องจักรรายตัว) — เครื่องจักรแต่ละเครื่อง
5. **Process Definitions** (คำจำกัดความกระบวนการ) — การดำเนินงาน (CNC Milling, Deburring เป็นต้น)
6. **Process Routes** (เส้นทางกระบวนการ) — ลำดับขั้นตอนสำหรับชิ้นงาน
7. **Customers** (ลูกค้า) — ลูกค้าที่ขายให้
8. **Operators** (พนักงานปฏิบัติการ) — พนักงานหน้างานพร้อมรหัส PIN
9. **Shifts & Work Calendar** (กะทำงานและปฏิทินทำงาน) — ชั่วโมงทำงาน
10. **Running Numbers** (เลขลำดับอัตโนมัติ) — การกำหนดรูปแบบรหัส
11. **Tooling** (เครื่องมือตัด) (เสริม) — หมวดเครื่องมือ, คำจำกัดความ, รายการเครื่องมือ

---

### โครงสร้างเอกสาร

1. [Factory Template & Setup Wizard (เทมเพลตโรงงานและตัวช่วยตั้งค่า)](./01-factory-template.md)
2. [Materials (วัสดุ)](./02-materials.md)
3. [Process Definitions (คำจำกัดความกระบวนการ)](./03-process-definitions.md)
4. [Process Routes (เส้นทางกระบวนการ)](./04-process-routes.md)
5. [Equipment Types (ประเภทเครื่องจักร)](./05-equipment-types.md)
6. [Equipment Instances (เครื่องจักรรายตัว)](./06-equipment-instances.md)
7. [Customers (ลูกค้า)](./07-customers.md)
8. [Operators (พนักงานปฏิบัติการ)](./08-operators.md)
9. [Factory Modeling (การจำลองโรงงาน)](./09-factory-modeling.md)
10. [Schedule Modeling (การจำลองตารางเวลา)](./10-schedule-modeling.md)
11. [Tooling Management (การจัดการเครื่องมือตัด)](./11-tooling.md)
12. [Abnormal Reasons & Maintenance (เหตุผลผิดปกติและการบำรุงรักษา)](./12-abnormal-maintenance.md)
13. [Knowledge Health (สุขภาพข้อมูลหลัก)](./13-knowledge-health.md)
14. [User Management (การจัดการผู้ใช้งาน)](./14-user-management.md)
15. [Running Numbers (เลขลำดับอัตโนมัติ)](./15-running-numbers.md)
16. [Role-Based Access Control (การควบคุมสิทธิ์ตามบทบาท)](./16-rbac.md)
