# 15. เลขที่รันนิ่ง (Running Numbers)

## การเข้าถึงหน้า Running Numbers

ไปที่ **System → Running Numbers** หรือเปิด `/system/running-numbers` เฉพาะ Admin เท่านั้น

[image: running-numbers-full — ภาพหน้าจอเต็มของหน้า Running Numbers แสดงตารางการตั้งค่า]

---

## วัตถุประสงค์

Running Numbers ควบคุมรูปแบบรหัสที่สร้างอัตโนมัติสำหรับทุก Entity ในระบบ เมื่อคุณสร้าง Work Order, Sales Order, Quote ฯลฯ ใหม่ รหัสจะถูกสร้างอัตโนมัติตามกฎเหล่านี้

---

## ตารางการตั้งค่า

แต่ละประเภท Entity มีแถวของตัวเอง:

| คอลัมน์ | คำอธิบาย |
|--------|-------------|
| Entity Type | รหัสนี้สำหรับอะไร (เช่น "Work Order", "Sales Order") |
| Prefix | คำนำหน้ารหัส (เช่น "WO", "SO", "QT") |
| Separator | อักขระระหว่างส่วน (เช่น "-") |
| Year Format | "YYYY" (4 หลัก) หรือ "YY" (2 หลัก) |
| Sequence Length | จำนวนหลัก (เช่น 5 → "00001") |
| Current Value | หมายเลขลำดับที่ใช้ล่าสุด |
| Preview | ตัวอย่างรหัสถัดไปที่จะสร้าง |

[image: running-numbers-table — ภาพใกล้ของตารางการตั้งค่าพร้อมประเภท Entity 5–6 รายการ]

---

## ประเภท Entity

| Entity | รูปแบบเริ่มต้น | ตัวอย่าง |
|--------|---------------|---------|
| Work Order | `WO-YYYY-NNNNN` | `WO-2026-00001` |
| Sales Order | `SO-YYYY-NNN` | `SO-2026-001` |
| Quote | `QT-YYYY-NNN` | `QT-2026-001` |
| Project | `PRJ-YYYY-NNN` | `PRJ-2026-001` |
| Material | `MAT-NNNN` | `MAT-0001` |
| Equipment | `EQP-NNNN` | `EQP-0001` |
| Tool Definition | `TLD-NNNN` | `TLD-0001` |
| Tool Instance | `TLI-NNNN` | `TLI-0001` |
| Process Route | `PR-NNN` | `PR-001` |
| Quality Inspection | `QI-YYYY-NNN` | `QI-2026-001` |
| NCR | `NCR-YYYY-NNN` | `NCR-2026-001` |
| Vendor | `VDR-NNNN` | `VDR-0001` |

---

## การแก้ไขรูปแบบรหัส

1. คลิกปุ่ม **Edit** (✏) บนแถว Entity
2. กล่องโต้ตอบจะเปิดพร้อมฟิลด์รูปแบบ
3. แก้ไข Prefix, Separator, Year Format หรือ Sequence Length
4. **Preview** จะอัปเดตแบบเรียลไทม์เมื่อคุณเปลี่ยนการตั้งค่า
5. คลิก **Save**

[image: running-numbers-edit — ภาพหน้าจอของกล่องโต้ตอบแก้ไขพร้อมฟิลด์รูปแบบและ Preview แบบสด]

---

## การรีเซ็ตลำดับ

1. คลิกปุ่ม **Reset** (↺) บนแถว Entity
2. ยืนยันในกล่องโต้ตอบ
3. ค่าปัจจุบันรีเซ็ตเป็น 0
4. รหัสถัดไปที่สร้างจะเริ่มจาก 1

> **คำเตือน:** รีเซ็ตลำดับเฉพาะเมื่อคุณแน่ใจว่าจะไม่เกิดความขัดแย้ง (เช่น ต้นปีใหม่)

[image: running-numbers-reset — ภาพหน้าจอของกล่องโต้ตอบยืนยันการรีเซ็ต]

---

## วิธีการสร้างรหัส

เมื่อสร้าง Entity ใหม่:
1. ระบบอ่านการตั้งค่า Running Number สำหรับประเภท Entity นั้น
2. เพิ่มค่าปัจจุบันแบบ Atomic
3. ประกอบรหัส: `{prefix}{separator}{year}{separator}{padded_sequence}`
4. รหัสถูกเก็บบันทึกในระเบียนใหม่

กระบวนการนี้เป็น Atomic — ไม่มีสองระเบียนที่จะได้รหัสเดียวกัน แม้ในการสร้างพร้อมกัน
