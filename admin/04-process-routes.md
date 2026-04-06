# 4. Process Routes (เส้นทางกระบวนการ)

## การเข้าถึง Process Routes

ไปที่ **Knowledge → Basic Data → Process Route** หรือเข้าที่ `/knowledge/basic/process-route`

[image: process-route-list — ภาพหน้าจอเต็มของหน้ารายการ Process Route]

---

## Process Route คืออะไร?

ลำดับขั้นตอนของ Process Definition ที่ชิ้นงานต้องผ่านในโรงงาน ตัวอย่างเช่น ตัวเรือนมอเตอร์อาจมีเส้นทาง: Die Casting → Deburring → CNC Milling → Surface Treatment → QC → Packing

---

## รายการ Process Route

### แถบเครื่องมือ (Toolbar)
- ปุ่ม **+ Process Route** — เปิดกล่องโต้ตอบสร้าง
- **Search box** (ช่องค้นหา) — กรองตามรหัส Route หรือชื่อ

### คอลัมน์ในตาราง

| คอลัมน์ | คำอธิบาย |
|---------|----------|
| Route Code (รหัส Route) | สร้างอัตโนมัติ (เช่น `PR-001`) |
| Name (ชื่อ) | ชื่อ Route (เช่น "Standard CNC Route") |
| Steps (ขั้นตอน) | จำนวนขั้นตอนใน Route |
| Status (สถานะ) | ป้าย Draft / Released |
| Actions (การดำเนินการ) | ดู (👁), ลบ (🗑) |

[image: process-route-table — ภาพขยายของตารางแสดง 3-4 Route ตัวอย่าง]

---

## การสร้าง Process Route

1. คลิก **+ Process Route**
2. กล่องโต้ตอบจะเปิดพร้อมแบบฟอร์ม Route
3. กรอก:

| ฟิลด์ | จำเป็น | คำอธิบาย |
|-------|--------|----------|
| Route Code (รหัส Route) | ใช่ | สร้างอัตโนมัติหรือกรอกเอง |
| Name (ชื่อ) | ใช่ | ชื่อที่สื่อความหมาย |
| Description (คำอธิบาย) | ไม่ | หมายเหตุเกี่ยวกับ Route นี้ |
| Status (สถานะ) | ใช่ | Draft หรือ Released |

4. เพิ่มขั้นตอนโดยเลือก Process Definition จากดรอปดาวน์
5. แต่ละขั้นตอนจะได้รับหมายเลขลำดับ (เพิ่มอัตโนมัติ)
6. ลากเพื่อจัดเรียงลำดับขั้นตอนใหม่
7. คลิก **Save** (บันทึก)

[image: process-route-create-dialog — ภาพหน้าจอกล่องโต้ตอบสร้างพร้อมขั้นตอนที่เพิ่มแล้ว]

---

## การดูรายละเอียด Route

1. คลิก **ไอคอนดู** (👁) ที่แถวของ Route
2. หน้ารายละเอียดจะเปิดแสดง:
   - ส่วนหัว Route (รหัส, ชื่อ, สถานะ)
   - รายการขั้นตอนตามลำดับพร้อมชื่อกระบวนการและประเภทเครื่องจักร
   - แผนภาพลำดับงานแบบภาพ

[image: process-route-detail — ภาพหน้าจอหน้ารายละเอียด Route แสดงลำดับขั้นตอน]

---

## ตัวอย่าง Process Routes

### เส้นทางชิ้นงาน CNC มาตรฐาน
```
1. Die Casting (บริการภายนอก — ระยะเวลานำส่ง 5 วัน)
2. Deburring (Deburring Station)
3. CNC Milling (5-Axis CNC Mill)
4. Surface Treatment / Oxidation (บริการภายนอก — ระยะเวลานำส่ง 3 วัน)
5. Quality Check (CMM)
6. Packing (Packing Station)
```

### เส้นทางชิ้นงานกลึงแบบง่าย
```
1. CNC Turning (CNC Lathe)
2. Deburring (Deburring Station)
3. Quality Check (CMM)
4. Packing (Packing Station)
```

### เส้นทางชิ้นงานความแม่นยำสูงซับซ้อน
```
1. CNC Milling Rough (3-Axis CNC Mill)
2. Heat Treatment (บริการภายนอก — ระยะเวลานำส่ง 7 วัน)
3. CNC Milling Finish (5-Axis CNC Mill)
4. Grinding (Surface Grinder)
5. Wire EDM (Wire EDM)
6. Quality Check (CMM)
7. Packing (Packing Station)
```
