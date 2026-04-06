# 12. การตั้งค่าสาเหตุผิดปกติและการซ่อมบำรุง

## สาเหตุผิดปกติ (Abnormal Reasons)

### การเข้าถึง

ไปที่ **Knowledge → Equipment Modeling → Abnormal Reason** หรือเปิด `/knowledge/equipment/abnormal-reason`

### วัตถุประสงค์

สาเหตุผิดปกติคือหมวดหมู่ที่กำหนดไว้ล่วงหน้าสำหรับปัญหาที่ช่างปฏิบัติงานรายงานจากหน้างาน ใช้ใน:
- ฟอร์มรายงานช่างปฏิบัติงาน (หมวดหมู่ที่ตั้งไว้ล่วงหน้า)
- กล่องโต้ตอบสาเหตุ Hold (เมื่อหยุด WO ชั่วคราว)
- การติดตามรายงานผิดปกติ

### คอลัมน์ในตาราง

| คอลัมน์ | คำอธิบาย |
|--------|-------------|
| Code | รหัสสาเหตุ |
| Name | ชื่อสาเหตุ (เช่น "Tool Breakage", "Material Shortage") |
| Name (Thai) | คำแปลภาษาไทยสำหรับหน้าจอช่างปฏิบัติงาน |
| Category | machine, tooling, material, quality, safety, other |
| Severity | Critical (วิกฤต), Major (สำคัญ), Minor (เล็กน้อย) |
| Self-Resumable | ช่างปฏิบัติงานสามารถกลับมาทำงานได้เองหลังจากสาเหตุ Hold นี้หรือไม่ |
| Status | Active / Inactive |

### การสร้างสาเหตุผิดปกติ

| ฟิลด์ | จำเป็น | คำอธิบาย |
|-------|----------|-------------|
| Code | ใช่ | รหัสที่ไม่ซ้ำกัน |
| Name | ใช่ | ชื่อภาษาอังกฤษ |
| Name (Thai) | ไม่ | ชื่อภาษาไทย (แสดงในหน้าจอช่างปฏิบัติงาน) |
| Category | ใช่ | machine, tooling, material, quality, safety, other |
| Severity | ใช่ | Critical, Major, Minor |
| Self-Resumable | Toggle | ถ้าเปิด ช่างปฏิบัติงานสามารถกลับมาทำงาน WO ที่ถูก Hold ได้โดยไม่ต้องรับการอนุมัติจากผู้จัดการ |
| Status | ใช่ | Active หรือ Inactive |

[image: abnormal-reason-form — ภาพหน้าจอของฟอร์ม Abnormal Reason]

---

## หมวดหมู่สาเหตุผิดปกติ (Abnormal Reason Categories)

ไปที่ **Knowledge → Equipment Modeling → Abnormal Reason Category** หรือเปิด `/knowledge/equipment/abnormal-reason-category`

จัดการหมวดหมู่ระดับบนสุดที่จัดกลุ่มสาเหตุผิดปกติ: machine, tooling, material, quality, safety, other

[image: abnormal-reason-categories — ภาพหน้าจอของหน้า Abnormal Reason Category]

---

## ประเภทการซ่อมบำรุง (Maintenance Types)

ไปที่ **Knowledge → Equipment Modeling → Maintenance Type** หรือเปิด `/knowledge/equipment/maintenance-type`

กำหนดประเภทกิจกรรมการซ่อมบำรุง:

| ตัวอย่าง | คำอธิบาย |
|---------|-------------|
| Preventive | การซ่อมบำรุงตามกำหนดเพื่อป้องกันความเสียหาย |
| Corrective | การซ่อมแซมหลังจากเกิดความเสียหาย |
| Predictive | การซ่อมบำรุงตามสภาพ |
| Calibration | การสอบเทียบอุปกรณ์วัด |

### ฟิลด์ในฟอร์ม

| ฟิลด์ | จำเป็น | คำอธิบาย |
|-------|----------|-------------|
| Code | ใช่ | รหัสประเภท |
| Name | ใช่ | ชื่อประเภท |
| Description | ไม่ | รายละเอียด |
| Status | ใช่ | Active / Inactive |

[image: maintenance-type-form — ภาพหน้าจอของฟอร์ม Maintenance Type]

---

## กลยุทธ์การซ่อมบำรุง (Maintenance Strategies)

ไปที่ **Knowledge → Equipment Modeling → Maintenance Strategy** หรือเปิด `/knowledge/equipment/maintenance-strategy`

กำหนดตารางและกลยุทธ์การซ่อมบำรุง:

| ฟิลด์ | จำเป็น | คำอธิบาย |
|-------|----------|-------------|
| Code | ใช่ | รหัสกลยุทธ์ |
| Name | ใช่ | ชื่อกลยุทธ์ (เช่น "Daily CNC Check", "Monthly Spindle Service") |
| Maintenance Type | ใช่ | เชื่อมโยงกับประเภทการซ่อมบำรุง |
| Frequency | ไม่ | ความถี่ (รายวัน, รายสัปดาห์, รายเดือน ฯลฯ) |
| Description | ไม่ | คำแนะนำโดยละเอียด |
| Status | ใช่ | Active / Inactive |

[image: maintenance-strategy-form — ภาพหน้าจอของฟอร์ม Maintenance Strategy]
