# คู่มือ End-to-End: จาก Quote ถึงการส่งมอบ

คู่มือนี้ติดตามคำสั่งซื้อจริงหนึ่งรายการ — **Hydraulic Manifold Block 2 ชิ้นสำหรับ Bosch** — ผ่านทุกโมดูล ทุกจุดส่งต่อระหว่างบทบาท และทุกหน้าจอใน TAM3D อ่านคู่มือนี้ก่อนหากคุณเพิ่งเริ่มใช้ระบบ จะเห็นภาพว่าทุกอย่างเชื่อมโยงกันอย่างไร

---

## คำสั่งซื้อ

**ลูกค้า:** Bosch
**ชิ้นงาน:** Hydraulic Manifold Block (เหล็ก Steel 4140, ความคลาดเคลื่อนแคบ ±0.01mm)
**จำนวน:** 2 ชิ้น
**กำหนดส่งมอบ:** 10 วันทำการนับจากวันนี้
**กระบวนการ:** CNC Milling (3 Setups) → Anodizing (ซัพภายนอก) → CMM Inspection → Packing

---

## ตัวละครในเรื่อง

| บุคคล | บทบาท | หน้าที่ในคำสั่งซื้อนี้ |
|--------|------|---------------------------|
| นนท์ | ฝ่ายขาย | สร้าง Quote, แปลงเป็น SO |
| กฤต | ผู้วางแผน | สร้าง WO, จัดตาราง, ติดตาม |
| พี่โบ้ | ช่างเครื่อง | กัดชิ้นงาน |
| เอิร์ธ | ผู้ตรวจสอบ QC | ตรวจสอบและลงชื่อรับรอง |
| ซัพภายนอก | Outside Processing | ชุบ Anodize ชิ้นงาน |

---

## เฟส 1 — ฝ่ายขายสร้าง Quote

**ใคร:** นนท์ (ฝ่ายขาย)
**ที่ไหน:** Sales → Quotes

### 1.1 สร้าง Quote

นนท์ไปที่ **Sales → Quotes → Create**

กรอกข้อมูล:
- ลูกค้า: Bosch
- รหัส Quote: สร้างอัตโนมัติเป็น `QT-2026-001`
- ระยะเวลา: 30 วัน
- หมายเหตุ: "Hydraulic Manifold Block, Steel 4140, ±0.01mm tolerance"

เพิ่มรายการสินค้า:
- ชื่อสินค้า: Hydraulic Manifold Block
- จำนวน: 2
- ราคาต่อหน่วย: (ราคาที่เจรจาแล้ว)
- กระบวนการ: CNC Milling Op10, CNC Milling Op20, CNC Milling Op30, Anodizing, CMM Inspection, Packing

[image: quote-create — ฟอร์มสร้าง Quote ที่มี Bosch เป็นลูกค้าและกรอกรายการสินค้าแล้ว]

### 1.2 ตรวจสอบสัญญาณ Delivery Promise

ก่อนส่ง Quote นนท์ตรวจสอบ **Delivery Promise Signal** บนหน้ารายละเอียด Quote สัญญาณแสดงเป็นสีเขียว — โรงงานมีกำลังการผลิตเพียงพอที่จะส่งมอบภายใน 10 วันทำการ

หากแสดงเป็นสีแดง นนท์จะเจรจาวันส่งมอบที่ช้าลงก่อนส่ง

[image: delivery-promise-green — สัญญาณ Delivery Promise สีเขียวบนหน้ารายละเอียด Quote]

### 1.3 แชร์ Quote ให้ Bosch

นนท์คลิก **Share** → คัดลอกลิงก์สาธารณะ → ส่งให้ผู้ติดต่อฝ่ายจัดซื้อของ Bosch

Bosch ดู Quote ได้ที่ `/share/quote/:token` — ไม่ต้องเข้าสู่ระบบ จะเห็นรายการสินค้า ราคา และประมาณการส่งมอบ

[image: quote-share-page — หน้าแชร์ Quote สาธารณะที่ลูกค้าเห็น]

### 1.4 Bosch ตอบรับ — แปลงเป็น Sales Order

Bosch ยืนยัน นนท์เปิด Quote → คลิก **Convert to Sales Order**

ระบบสร้าง:
- Sales Order `SO-2026-001` สถานะ `Confirmed`
- รายการสินค้าเชื่อมโยงกับรายการใน Quote ผ่าน `source_quote_item_id`
- ลูกค้า: Bosch, วันครบกำหนด: 10 วันทำการนับจากวันนี้

[image: so-created — Sales Order SO-2026-001 สถานะ Confirmed]

**ส่งต่อ:** นนท์แจ้งกฤต (ผู้วางแผน) ว่า SO-2026-001 พร้อมเข้าสู่การผลิต

---

## เฟส 2 — ผู้วางแผนสร้าง Work Order

**ใคร:** กฤต (ผู้วางแผน)
**ที่ไหน:** Sales → Sales Orders → SO-2026-001, จากนั้น Production

### 2.1 สร้าง Work Order จาก SO

กฤตเปิด **Sales → Sales Orders** → ค้นหา `SO-2026-001` → เปิด

บนรายการ Hydraulic Manifold Block คลิก **Create Work Order**

ระบบกรอกข้อมูลอัตโนมัติ:
- ชื่อสินค้า: Hydraulic Manifold Block
- จำนวน: 2
- ขั้นตอนจากกระบวนการที่กำหนดใน Quote (Op10, Op20, Op30, Anodizing, CMM Inspection, Packing)
- รหัส WO: สร้างอัตโนมัติเป็น `WO-2026-00001`

กฤตตรวจสอบและตั้งค่า:
- วัสดุ: Steel 4140 (MAT-0003)
- เส้นทางกระบวนการ: `RT-MANIFOLD-3OP-01` (เส้นทางสำเร็จรูปสำหรับตระกูลชิ้นงานนี้)
- วันครบกำหนด: สืบทอดจาก SO
- ลำดับความสำคัญ: Normal

คลิก **Create** WO ถูกสร้างในสถานะ `draft`

[image: wo-create — ฟอร์มสร้าง Work Order ที่มีขั้นตอนกรอกอัตโนมัติจาก Quote]

### 2.2 ตรวจสอบขั้นตอน

กฤตเปิด `WO-2026-00001` → ตรวจสอบ 6 ขั้นตอน:

| ลำดับ | ขั้นตอน | ประเภทเครื่องจักร | เวลาประมาณ | ประเภท |
|-----|------|---------------|------------|------|
| 10 | CNC Milling Op10 | 5-Axis CNC Mill | 3.0 ชม. | In-house |
| 20 | CNC Milling Op20 | 5-Axis CNC Mill | 2.5 ชม. | In-house |
| 30 | CNC Milling Op30 | 5-Axis CNC Mill | 1.5 ชม. | In-house |
| 40 | Anodizing | — | 24.0 ชม. | Outside Processing |
| 50 | CMM Inspection | CMM | 0.5 ชม. | In-house |
| 60 | Packing | Packing Station | 0.2 ชม. | In-house |

ขั้นตอนที่ 40 (Anodizing) มี `is_outside_service = true` ระบบสร้าง **Outside Processing Order** (OPO) อัตโนมัติ เชื่อมโยงกับซัพ Anodizing เริ่มต้น

[image: wo-steps — รายการขั้นตอน Work Order แสดง 6 ขั้นตอนพร้อมตัวบ่งชี้ OPO ที่ขั้นตอน 40]

### 2.3 Release Work Order

กฤตคลิก **Release** สถานะ WO เปลี่ยนจาก `draft` → `released`

ตอนนี้ WO ปรากฏใน Unscheduled Sidebar บน Scheduling Board

---

## เฟส 3 — ผู้วางแผนจัดตารางการผลิต

**ใคร:** กฤต (ผู้วางแผน)
**ที่ไหน:** Production → Scheduling Board

### 3.1 เปิด Scheduling Board

กฤตไปที่ **Production → Scheduling Board** บอร์ดแสดง:
- **Lane 1 (Timeline Grid):** แถวเครื่องจักร × คอลัมน์ชั่วโมง 08:00–20:00
- **Lane 2 (Outside Processing Panel):** แถบ Gantt ของซัพ
- **Lane 3 (QC Queue Panel):** การ์ดตรวจสอบแบ่งตามวัน

ใน **Unscheduled Sidebar** `WO-2026-00001` แสดงขั้นตอน In-house 3 รายการ (Op10, Op20, Op30) พร้อมจัดตาราง ขั้นตอนที่ 40 (Anodizing) แสดงเป็นแถวข้อมูล — เป็น OPO ไม่ใช่งานเครื่องจักร

[image: scheduling-board-unscheduled — Scheduling Board พร้อมขั้นตอนของ WO-2026-00001 ใน Unscheduled Sidebar]

### 3.2 จัดตาราง Op10

กฤตลาก **CNC Milling Op10** จาก Sidebar ไปวางบนแถว 5-Axis CNC Mill (EQP-0005) ที่วันจันทร์ 08:00

แถบงานปรากฏบน Timeline ครอบคลุม 08:00–11:00 (3 ชั่วโมง)

[image: op10-scheduled — แถบ Op10 วางบน 5-Axis Mill ที่วันจันทร์ 08:00]

### 3.3 จัดตาราง Op20 และ Op30

กฤตลาก **CNC Milling Op20** ไปวางบนเครื่องเดียวกันที่วันจันทร์ 11:00 (ต่อจาก Op10 ทันที) ระบบบังคับลำดับ — Op20 ไม่สามารถเริ่มก่อน Op10 เสร็จ

จากนั้นลาก **CNC Milling Op30** ที่วันจันทร์ 13:30 (หลังพักกลางวัน 30 นาที)

Timeline วันจันทร์:
```
08:00 ──────── Op10 (3.0 ชม.) ──────── 11:00
11:00 ──── Op20 (2.5 ชม.) ──── 13:30
13:30 ── Op30 (1.5 ชม.) ── 15:00
```

[image: all-ops-scheduled — ทั้งสาม Op ถูกจัดตารางบน Timeline วันจันทร์]

### 3.4 OPO ปรากฏใน Outside Processing Panel

หลังจาก Op30 ถูกจัดตารางให้เสร็จวันจันทร์ 15:00 **Outside Processing Panel** (Lane 2) แสดง Anodizing OPO อัตโนมัติ:

- ซัพ: Anodizing Co. (VDR-0002)
- วันส่งชิ้นงาน: วันอังคาร (วันทำการถัดไปหลัง Op30 เสร็จ)
- วันคาดว่าได้รับคืน: วันพฤหัส (Lead Time 2 วันทำการ)
- สถานะ: Pending (แถบสีเทา)

[image: opo-panel — Outside Processing Panel แสดง Anodizing OPO เป็นแถบสีเทา Pending]

### 3.5 CMM Inspection ปรากฏใน QC Queue Panel

**QC Queue Panel** (Lane 3) แสดงการ์ดสำหรับ `WO-2026-00001` ในคอลัมน์วันพฤหัส — วันที่ชิ้นงานชุบ Anodize คาดว่าจะกลับมาและพร้อมสำหรับ CMM Inspection

[image: qc-queue — QC Queue Panel แสดงการ์ด WO-2026-00001 ในคอลัมน์วันพฤหัส]

---

## เฟส 4 — ช่างเครื่องดำเนินการกัดชิ้นงาน

**ใคร:** พี่โบ้ (ช่างเครื่อง)
**ที่ไหน:** `/operator` (Operator Home) หรือ Operator Panel

### 4.1 ช่างเครื่องเข้าสู่ระบบ

เช้าวันจันทร์ พี่โบ้เปิด `/operator` บนแท็บเล็ต กรอก PIN 4 หลัก หน้า Dashboard แสดงคิวงานของเขา

[image: operator-home — Operator Home Dashboard พร้อมการ์ดคิวงานแสดง WO-2026-00001]

### 4.2 เริ่ม Op10

พี่โบ้แตะ **Task Queue** → เห็น `WO-2026-00001 — CNC Milling Op10` อยู่บนสุด (จัดตารางสำหรับเครื่องนี้ กะนี้)

แตะที่งาน → เปิดรายละเอียดขั้นตอน เห็น:
- ชิ้นงาน: Hydraulic Manifold Block
- งาน: CNC Milling Op10
- คำแนะนำ: "Face, bore pattern, top features. Probe X/Y/Z zero on datum A."
- เวลาประมาณ: 3.0 ชม.

แตะ **Start** สถานะขั้นตอนเปลี่ยนเป็น `in_progress` สถานะ WO เปลี่ยนจาก `released` → `in_progress`

[image: operator-step-start — Operator Panel รายละเอียดขั้นตอนพร้อมปุ่ม Start]

### 4.3 First Article Inspection (FAI)

หลังกัดชิ้นแรกเสร็จ พี่โบ้ Hold ขั้นตอนไว้และแจ้งเอิร์ธ (ผู้ตรวจสอบ QC) ว่าชิ้นแรกพร้อมสำหรับ FAI

*(ดู [HMLV-06: First Article Inspection](./planner/hmlv-06-first-article-inspection.md) สำหรับขั้นตอน FAI เต็มรูปแบบ)*

เอิร์ธตรวจสอบชิ้นแรก — ทุกมิติอยู่ในค่า Tolerance FAI ผ่าน

พี่โบ้กลับมาทำ Op10 ต่อและกัดชิ้นที่สอง รายงานเสร็จ: จำนวน 2

### 4.4 เสร็จ Op10, เริ่ม Op20

พี่โบ้แตะ **Complete** ที่ Op10 สถานะขั้นตอนเปลี่ยนเป็น `completed`

Op20 พร้อมใช้งานทันทีในคิวงาน เขาจับยึดชิ้นงานใหม่ (พลิกบน Datum Face ของ Op10) แตะ **Start** ที่ Op20

[image: op20-start — คิวงานแสดง Op20 พร้อมใช้งานหลัง Op10 เสร็จ]

### 4.5 เสร็จ Op20 และ Op30

รูปแบบเดียวกัน Op20 เสร็จ → Op30 พร้อม → พี่โบ้กัดโปรไฟล์ด้านข้าง → รายงานเสร็จ

ขั้นตอนกัดทั้งสามขั้นตอนตอนนี้เป็น `completed` แล้ว WO ยังคงเป็น `in_progress` — กำลังรอขั้นตอน Anodizing

---

## เฟส 5 — Outside Processing (Anodizing)

**ใคร:** กฤต (ผู้วางแผน) ติดตาม; ซัพทำงาน
**ที่ไหน:** Production → Outside Processing

### 5.1 ส่งชิ้นงานไปซัพ

เช้าวันอังคาร กฤตเปิด **Production → Outside Processing**

ค้นหา OPO ของ `WO-2026-00001` — Anodizing, สถานะ: Pending

กฤตพิมพ์ **Packing Slip** (ปุ่มบนหน้ารายละเอียด OPO) และแนบไปกับการจัดส่ง

คลิก **Mark as Shipped** สถานะ OPO เปลี่ยนเป็น `Shipped` แถบใน Outside Processing Panel เปลี่ยนเป็นสีส้ม

[image: opo-shipped — Outside Processing Panel พร้อมแถบสีส้ม Shipped สำหรับ WO-2026-00001]

### 5.2 ติดตามบน Scheduling Board

Outside Processing Panel แสดงแถบ Anodizing ครอบคลุมวันอังคาร → วันพฤหัส กฤตเห็นภาพรวมได้ทันทีว่าชิ้นงานส่งออกไปแล้วและคาดว่าจะกลับวันพฤหัส

หากวันพฤหัสผ่านไปโดยชิ้นงานไม่กลับ แถบจะเปลี่ยนเป็นสีแดง (เกินกำหนด) กฤตจะติดต่อซัพโดยตรง

### 5.3 ชิ้นงานกลับจากซัพ

วันพฤหัส ชิ้นงานชุบ Anodize มาถึง กฤตเปิด OPO → คลิก **Mark as Completed** สถานะ OPO เปลี่ยนเป็น `Completed`

ขั้นตอน Anodizing (ขั้นตอนที่ 40) บน WO ถูกปลดบล็อก ขั้นตอนที่ 50 (CMM Inspection) พร้อมใช้งาน

[image: opo-completed — OPO ถูกทำเครื่องหมายเป็น Completed, ขั้นตอน 50 พร้อมใช้งาน]

---

## เฟส 6 — การตรวจสอบคุณภาพ

**ใคร:** เอิร์ธ (ผู้ตรวจสอบ QC)
**ที่ไหน:** Quality → Inspections

### 6.1 CMM Inspection ปรากฏในคิว

QC Queue Panel บน Scheduling Board แสดง `WO-2026-00001` ในคอลัมน์วันพฤหัส เอิร์ธเห็นบน Dashboard ของเธอ

### 6.2 สร้างบันทึกการตรวจสอบ

เอิร์ธไปที่ **Quality → Inspections → Create**

กรอกข้อมูล:
- โครงการ: (เชื่อมโยงกับโครงการของ SO-2026-001 หากมี หรือเชื่อมโยงกับ WO โดยตรง)
- Work Order: WO-2026-00001
- ขั้นตอน: CMM Inspection (ขั้นตอนที่ 50)
- จำนวนตัวอย่าง: 2 (ทั้งสองชิ้น — ตรวจ 100% สำหรับชิ้นงาน Tolerance แคบ)
- จำนวนที่ตรวจ: 2
- จำนวนข้อบกพร่อง: 0
- ผลลัพธ์: **Pass**

[image: inspection-create — ฟอร์มสร้างการตรวจสอบที่มีผลลัพธ์ Pass สำหรับ WO-2026-00001]

### 6.3 การตรวจสอบผ่าน — เสร็จขั้นตอน

เอิร์ธบันทึกผลการตรวจสอบ ผลลัพธ์เชื่อมโยงกับ WO

เธอทำเครื่องหมายขั้นตอนที่ 50 (CMM Inspection) เป็น `completed` บน WO

ขั้นตอนที่ 60 (Packing) พร้อมใช้งาน

### 6.4 หากการตรวจสอบไม่ผ่าน?

หากเอิร์ธพบข้อบกพร่องด้านมิติบนชิ้นหนึ่ง:

1. ตั้ง Result: Fail, Defect Count: 1, Defect Type: Dimensional
2. ไปที่ **Quality → NCR → Create**
3. เชื่อมโยงกับ WO-2026-00001 และผลการตรวจสอบที่ไม่ผ่าน
4. ตั้ง Disposition: Rework (หากข้อบกพร่องแก้ไขได้โดยกัดใหม่) หรือ Remake (หากชิ้นงานเป็นเศษ)
5. Resolve NCR → ระบบรีเซ็ตขั้นตอนที่ได้รับผลกระทบ → พี่โบ้กัดใหม่

*(ดู [HMLV-04: Engineering Change](./planner/hmlv-04-engineering-change-mid-production.md) และ [คู่มือ QC: Rework & Remake](./qc/07-rework-remake.md) สำหรับรายละเอียดเต็มรูปแบบ)*

---

## เฟส 7 — Packing และเสร็จสิ้น

**ใคร:** พี่โบ้ (ช่างเครื่อง) หรือเจ้าหน้าที่คลังสินค้า
**ที่ไหน:** Operator Panel หรือโดยตรงบน WO

### 7.1 แพ็คชิ้นงาน

พี่โบ้ (หรือช่างประจำสถานี Packing) เริ่มและเสร็จขั้นตอนที่ 60 (Packing) รายงานจำนวน: 2

### 7.2 WO เสร็จสิ้นอัตโนมัติ

เมื่อทั้ง 6 ขั้นตอนอยู่ในสถานะสิ้นสุด (completed หรือ skipped) WO จะเปลี่ยนเป็น `completed` อัตโนมัติ

ป้ายสถานะ WO ในรายการ Work Orders เปลี่ยนเป็นสีเขียว

[image: wo-completed — Work Order WO-2026-00001 แสดงสถานะ Completed]

### 7.3 สถานะ SO อัปเดต

ระบบตรวจสอบ: WO ทั้งหมดที่เชื่อมโยงกับ SO-2026-001 เป็นสถานะสิ้นสุดหรือยัง? ใช่ — WO-2026-00001 เป็น WO เดียวและ completed แล้ว

สถานะ SO-2026-001 เปลี่ยนจาก `In Production` → `Completed` อัตโนมัติ

[image: so-completed — Sales Order SO-2026-001 แสดงสถานะ Completed]

---

## เฟส 8 — การส่งมอบและการตรวจสอบย้อนกลับ

**ใคร:** นนท์ (ฝ่ายขาย) ยืนยันการส่งมอบ; ทุกคนสามารถดูการตรวจสอบย้อนกลับ
**ที่ไหน:** Sales → Sales Orders, Production → Traceability

### 8.1 ใบรับสินค้าขาออก

ก่อนจัดส่ง คลังสินค้าสร้าง **Outbound Receipt** ใน Inventory:

- ไปที่ **Inventory → Outbound → Create**
- วัสดุ: Hydraulic Manifold Block (สำเร็จรูป)
- จำนวน: 2
- อ้างอิง: WO-2026-00001, SO-2026-001

บันทึกนี้บันทึกการจัดส่งจริงและลดสต็อกสินค้าสำเร็จรูป

### 8.2 ดูการตรวจสอบย้อนกลับทั้งหมด

ทุกคนสามารถไปที่ **Production → Traceability** แล้วค้นหา `WO-2026-00001` หรือ `SO-2026-001`

มุมมองการตรวจสอบย้อนกลับแสดงสายงานทั้งหมด:

```
SO-2026-001 (Bosch)
  └── WO-2026-00001 (Hydraulic Manifold Block × 2)
        ├── ขั้นตอน 10: CNC Milling Op10 ✅ Completed — พี่โบ้ — จันทร์ 08:00–11:00
        ├── ขั้นตอน 20: CNC Milling Op20 ✅ Completed — พี่โบ้ — จันทร์ 11:00–13:30
        ├── ขั้นตอน 30: CNC Milling Op30 ✅ Completed — พี่โบ้ — จันทร์ 13:30–15:00
        ├── ขั้นตอน 40: Anodizing ✅ Completed — Anodizing Co. — อังคาร–พฤหัส
        ├── ขั้นตอน 50: CMM Inspection ✅ Completed — เอิร์ธ — พฤหัส 14:00 — Pass
        └── ขั้นตอน 60: Packing ✅ Completed — พฤหัส 15:30
```

[image: traceability — หน้าตรวจสอบย้อนกลับแสดงสายงานทั้งหมดของ SO-2026-001]

---

## สรุป: จุดส่งต่อระหว่างบทบาท

```
ฝ่ายขาย (นนท์)
  สร้าง Quote QT-2026-001
  ตรวจสอบ Delivery Promise Signal → สีเขียว
  แชร์ให้ Bosch → Bosch ตอบรับ
  แปลงเป็น SO-2026-001
        ↓ ส่งต่อให้
ผู้วางแผน (กฤต)
  สร้าง WO-2026-00001 จากรายการใน SO
  ตรวจสอบขั้นตอน (OPO สร้างอัตโนมัติสำหรับ Anodizing)
  Release WO
  จัดตาราง Op10/Op20/Op30 บน Scheduling Board
  ติดตาม OPO ใน Outside Processing Panel
  ส่งชิ้นงานไปซัพ (วันอังคาร)
  รับชิ้นงานกลับ (วันพฤหัส)
        ↓ ส่งต่อให้
ช่างเครื่อง (พี่โบ้)
  เข้าสู่ระบบผ่าน PIN ที่ /operator
  ทำ Op10 → FAI → Op20 → Op30
  รายงานเสร็จแต่ละขั้นตอน
        ↓ ส่งต่อให้
ผู้ตรวจสอบ QC (เอิร์ธ)
  สร้างบันทึกการตรวจสอบ
  CMM วัดทั้งสองชิ้น → Pass
  เสร็จขั้นตอน 50
        ↓ ส่งต่อให้
ช่างเครื่อง / คลังสินค้า
  แพ็คชิ้นงาน → ขั้นตอน 60 เสร็จ
  WO เสร็จอัตโนมัติ → SO เสร็จอัตโนมัติ
        ↓
ฝ่ายขาย (นนท์)
  เห็น SO-2026-001 เป็น Completed
  ส่งมอบให้ Bosch
  สร้าง Outbound Receipt ใน Inventory
```

---

## พฤติกรรมของระบบที่ควรสังเกต

**การสร้าง OPO อัตโนมัติ** เมื่อกฤตสร้าง WO ที่มีขั้นตอน Anodizing ระบบสร้าง OPO อัตโนมัติ กฤตไม่ต้องไปที่ Outside Processing แล้วสร้างเอง

**การบังคับลำดับขั้นตอน** พี่โบ้ไม่สามารถเริ่ม Op20 ก่อน Op10 เสร็จ ระบบบล็อกไว้ ป้องกันไม่ให้ช่างข้ามขั้นตอนหรือทำงานผิดลำดับ

**WO และ SO เสร็จอัตโนมัติ** เมื่อขั้นตอนสุดท้ายเสร็จ WO เปลี่ยนเป็น Completed อัตโนมัติ เมื่อ WO เสร็จ SO เปลี่ยนเป็น Completed อัตโนมัติ ไม่ต้องอัปเดตสถานะเอง

**Delivery Promise Signal** สัญญาณบน Quote ตรวจสอบกำลังการผลิตของโรงงานก่อนที่นนท์จะรับปากวันส่งมอบ หากโรงงานมีภาระงานเกิน จะแสดงสีแดง — กระตุ้นให้คุยกันก่อนรับปาก

**Cross-lane Hover Linking** บน Scheduling Board การเลื่อนเมาส์ไปที่ `WO-2026-00001` ใน Lane ใดก็ได้ (Timeline, OPO Panel, QC Queue) จะไฮไลท์ข้าม Lane ทั้งสามพร้อมกัน กฤตเห็นภาพรวมของคำสั่งซื้อหนึ่งรายการโดยไม่ต้องสลับมุมมอง

---

## สิ่งที่คำสั่งซื้อนี้ไม่ได้ครอบคลุม

คู่มือนี้ใช้เส้นทาง Happy Path สำหรับสถานการณ์ข้อยกเว้นที่เกิดขึ้นทุกวันในโรงงาน HMLV ดูที่:

| สถานการณ์ | คู่มือ |
|----------|-------|
| FAI ไม่ผ่าน ต้องแก้ไข Setup | [HMLV-06: First Article Inspection](./planner/hmlv-06-first-article-inspection.md) |
| ลูกค้าโทรขอเร่งระหว่างผลิต | [HMLV-02: Hot Job / Rush Order](./planner/hmlv-02-hot-job-rush-order.md) |
| ซัพ Anodizing ส่งล่าช้า | [ผู้วางแผน: Outside Processing Panel](./planner/08-outside-processing-panel.md) |
| CMM Inspection ไม่ผ่าน ชิ้นหนึ่งต้อง Remake | [QC: Rework & Remake](./qc/07-rework-remake.md) |
| ลูกค้าต้องการ 1 ชิ้นตอนนี้ อีก 1 ชิ้นทีหลัง | [HMLV-03: Partial Shipment](./planner/hmlv-03-partial-shipment.md) |
| แบบรุ่นใหม่มาถึงหลัง Op10 | [HMLV-04: Engineering Change](./planner/hmlv-04-engineering-change-mid-production.md) |
