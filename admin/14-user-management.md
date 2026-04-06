# 14. การจัดการผู้ใช้ (User Management)

## การเข้าถึงหน้าจัดการผู้ใช้

ไปที่ **System → Users** หรือเปิด `/system/users` เฉพาะ Admin เท่านั้น

[image: user-management-full — ภาพหน้าจอเต็มของหน้า User Management แสดงตารางผู้ใช้และสรุปบทบาท]

---

## เค้าโครงหน้า (Page Layout)

### สรุปบทบาท
ด้านบน การ์ดแสดงจำนวนผู้ใช้ต่อบทบาท

### ตารางผู้ใช้

| คอลัมน์ | คำอธิบาย |
|--------|-------------|
| Username | ชื่อผู้ใช้สำหรับเข้าสู่ระบบ (รูปแบบ: `name@mes.vulcorn.com`) |
| Display Name | ชื่อที่แสดงของผู้ใช้ |
| Role | ป้ายบทบาทที่กำหนด |
| Status | Active / Disabled |
| Created | วันที่สร้างบัญชี |
| Actions | แก้ไขบทบาท, สลับสถานะ |

[image: user-management-table — ภาพหน้าจอของตารางผู้ใช้พร้อมตัวอย่าง 4–5 ผู้ใช้ในบทบาทต่างกัน]

---

## การสร้างผู้ใช้

1. คลิก **+ User**
2. กรอกข้อมูลในกล่องโต้ตอบ:

| ฟิลด์ | จำเป็น | คำอธิบาย |
|-------|----------|-------------|
| Username | ใช่ | จะถูกจัดรูปแบบเป็น `username@mes.vulcorn.com` |
| Password | ใช่ | รหัสผ่านเริ่มต้น |
| Display Name | ไม่ | ชื่อที่เป็นมิตร |
| Role | ใช่ | เลือกจาก: Admin, Sales, Planner, Operator, QC Inspector, Warehouse, Maintenance, Production Manager |

3. คลิก **Create**

[image: user-management-create — ภาพหน้าจอของกล่องโต้ตอบ Create User]

---

## การเปลี่ยนบทบาทผู้ใช้

1. คลิกเมนูการดำเนินการ (⋯) บนแถวผู้ใช้
2. เลือก **Change Role**
3. เลือกบทบาทใหม่จาก Dropdown
4. ยืนยัน

---

## การปิดใช้งาน/เปิดใช้งานผู้ใช้

1. คลิกเมนูการดำเนินการ (⋯) บนแถวผู้ใช้
2. เลือก **Disable** (หรือ **Enable** ถ้าปิดใช้งานอยู่แล้ว)
3. ผู้ใช้ที่ปิดใช้งานไม่สามารถเข้าสู่ระบบได้ แต่ข้อมูลของพวกเขาจะถูกเก็บรักษาไว้

---

## บทบาทที่มีให้เลือก

| บทบาท | ระดับการเข้าถึง |
|------|-------------|
| Admin | เข้าถึงได้ทุกอย่างรวมถึงการตั้งค่าระบบ |
| Sales | เข้าถึง Sales ได้เต็มที่; อ่านอย่างเดียวสำหรับ Production และ Knowledge |
| Planner | เข้าถึง Production, Scheduling, OPO ได้เต็มที่; อ่านอย่างเดียวสำหรับ Sales, Inventory, Knowledge |
| Operator | เข้าถึง Work Orders และ Kanban ได้เต็มที่; อ่านอย่างเดียวสำหรับ OPO, Quality, Knowledge |
| QC Inspector | เข้าถึง Quality ได้เต็มที่; อ่านอย่างเดียวสำหรับ Work Orders และ Knowledge |
| Warehouse Staff | เข้าถึง Inventory ได้เต็มที่; อ่านอย่างเดียวสำหรับ Knowledge |
| Maintenance Technician | เข้าถึง Equipment ได้เต็มที่; อ่านอย่างเดียวสำหรับ Knowledge |
| Production Manager | เข้าถึง Production และ OPO ได้เต็มที่; อ่านอย่างเดียวสำหรับ Sales, Inventory, Quality, Equipment, Knowledge |

ดู [Role-Based Access Control](./16-rbac.md) สำหรับเมทริกซ์การเข้าถึงแบบเต็ม
