# 5. Equipment Types (ประเภทเครื่องจักร)

## การเข้าถึง Equipment Types

ไปที่ **Knowledge → Equipment Modeling → Equipment Type** หรือเข้าที่ `/knowledge/equipment/type`

[image: equipment-type-list — ภาพหน้าจอเต็มของหน้ารายการ Equipment Type]

---

## Equipment Type คืออะไร?

หมวดหมู่เครื่องจักรที่จัดกลุ่มอุปกรณ์ที่คล้ายกัน (เช่น "5-Axis CNC Mill", "CNC Lathe", "Surface Grinder") Equipment Type ถูกอ้างอิงโดย Process Definition (ประเภทเครื่องจักรใดรันการดำเนินงานใด) และโดย Equipment Instance แต่ละเครื่อง

---

## รายการ Equipment Type

### คอลัมน์ในตาราง

| คอลัมน์ | คำอธิบาย |
|---------|----------|
| Code (รหัส) | รหัสประเภทเครื่องจักร |
| Name (ชื่อ) | ชื่อประเภท (เช่น "5-Axis CNC Mill") |
| Category (หมวดหมู่) | หมวดหมู่สำหรับจัดกลุ่ม |
| Status (สถานะ) | Active / Inactive |
| Actions (การดำเนินการ) | แก้ไข (✏), ลบ (🗑) |

---

## การสร้าง Equipment Type

1. คลิก **+ Equipment Type**
2. กรอก: รหัส, ชื่อ, หมวดหมู่, คำอธิบาย, สถานะ
3. คลิก **Save** (บันทึก)

[image: equipment-type-form — ภาพหน้าจอแบบฟอร์มสร้าง Equipment Type]

---

## ประเภทเครื่องจักรมาตรฐานสำหรับโรงงาน CNC

| ชื่อ | หมวดหมู่ | คำอธิบาย |
|------|----------|----------|
| CNC Lathe (เครื่องกลึง CNC) | Machining | งานกลึง |
| 3-Axis CNC Mill (เครื่องกัด CNC 3 แกน) | Machining | งานกัดพื้นฐาน |
| 5-Axis CNC Mill (เครื่องกัด CNC 5 แกน) | Machining | งานกัด 3D ที่ซับซ้อน |
| Swiss Lathe (เครื่องกลึงสวิส) | Machining | ชิ้นงานขนาดเล็กความแม่นยำสูง |
| Surface Grinder (เครื่องเจียรราบ) | Finishing | งานเจียรผิวเรียบ |
| Cylindrical Grinder (เครื่องเจียรทรงกระบอก) | Finishing | งานเจียรผิวกลม |
| Wire EDM (เครื่อง Wire EDM) | Machining | การตัดด้วยลวดไฟฟ้า |
| Sinker EDM (เครื่อง Sinker EDM) | Machining | การกัดแบบ EDM จม |
| Bandsaw (เครื่องเลื่อยสายพาน) | Preparation | การตัดวัตถุดิบ |
| CMM (เครื่องวัดพิกัด) | Inspection | เครื่องวัดพิกัด (Coordinate Measuring Machine) |
| Deburring Station (สถานีลบครีบ) | Finishing | การลบครีบแบบแมนนวล/อัตโนมัติ |
| Packing Station (สถานีบรรจุ) | Logistics | การบรรจุขั้นสุดท้าย |
