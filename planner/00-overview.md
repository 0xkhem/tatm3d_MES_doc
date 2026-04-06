# Planner (ผู้วางแผนการผลิต) — คู่มือการใช้งาน

## ภาพรวม

คู่มือนี้ครอบคลุมทุกงานที่ Production Planner (ผู้วางแผนการผลิต) ปฏิบัติในระบบ TAM3D MES ตั้งแต่การตรวจสอบใบสั่งผลิตที่เข้ามา การจัดตารางงานบนเครื่องจักร การติดตามงานส่งผลิตภายนอก และการติดตามการส่งมอบตรงเวลา

### การนำทาง (Navigation)

ผู้วางแผนจะทำงานหลักในเมนูแถบด้านข้างเหล่านี้:

| หมวดเมนู | หน้าย่อย | วัตถุประสงค์ |
|-------------|-----------|---------|
| Home (หน้าหลัก) | `/home` | ศูนย์บัญชาการพร้อมรายการที่ต้องดูแลและ KPIs |
| Production → Dashboard (แดชบอร์ดการผลิต) | `/production/dashboard` | KPIs, การกระจายสถานะ, อายุงานระหว่างผลิต |
| Production → Work Orders (ใบสั่งผลิต) | `/production/work-orders` | จัดการวงจรชีวิตของ WO และความคืบหน้าของขั้นตอน |
| Production → Scheduling (การจัดตาราง) | `/production/scheduling` | กระดานจัดตารางสามเลน (เครื่องมือหลัก) |
| Production → Traceability (การตรวจสอบย้อนกลับ) | `/production/traceability` | การติดตามคำสั่งซื้อแบบครบวงจร |
| Outside Processing (งานส่งผลิตภายนอก) | `/production/outside-processing/*` | คำสั่งซื้อผู้ขาย, การจัดส่ง, การรับคืน |
| Shift Roster (ตารางกะทำงาน) | `/production/shift-roster` | การจับคู่เครื่องจักร-ผู้ปฏิบัติงาน |

[image: sidebar-production-menu — ภาพหน้าจอของแถบเมนูด้านซ้ายที่แสดงหมวด "Production" และ "Outside Processing" แบบขยาย แสดงรายการเมนูย่อยทั้งหมดที่เกี่ยวข้องกับผู้วางแผน]

---

### ขั้นตอนการทำงานประจำวันของผู้วางแผน

กิจวัตรตอนเช้าโดยทั่วไป:

```
1. ตรวจสอบ Home Page → Attention Items (มีเรื่องเร่งด่วนอะไรบ้าง?)
2. เปิด Scheduling Board → ตรวจสอบงานที่ยังไม่ได้จัดตาราง
3. มอบหมายหรือจัดตารางอัตโนมัติให้กับเครื่องจักร
4. ตรวจสอบ Outside Processing → มีงานผู้ขายส่งคืนล่าช้าหรือไม่?
5. ตรวจสอบ Work Orders → มี WO ที่เกินกำหนดหรือถูกพักไว้หรือไม่?
6. ตรวจสอบ Shift Roster → เครื่องจักรทุกเครื่องมีคนประจำหรือไม่?
```

[image: planner-daily-flow — แผนภาพแสดงขั้นตอนการทำงานประจำวันของผู้วางแผน จาก Home → Scheduling → OPO → WO review]

---

### อ้างอิงสถานะของ Work Order (ใบสั่งผลิต)

| สถานะ | สี | ความหมาย |
|--------|-------|---------|
| Draft (ร่าง) | เทา | สร้างแล้วแต่ยังไม่ปล่อยลงพื้นที่ผลิต |
| Released (ปล่อยแล้ว) | น้ำเงิน | พร้อมสำหรับการจัดตารางและการผลิต |
| In Progress (กำลังดำเนินการ) | เหลือง/อำพัน | ขั้นตอนอย่างน้อยหนึ่งขั้นตอนเริ่มแล้ว |
| On Hold (พักงาน) | แดง | หยุดชั่วคราวพร้อมระบุเหตุผล (ขาดวัสดุ, ปัญหาคุณภาพ ฯลฯ) |
| Completed (เสร็จสิ้น) | เขียว | ทุกขั้นตอนเสร็จสมบูรณ์แล้ว |
| Cancelled (ยกเลิก) | เทา | ยกเลิกแล้ว (สถานะสุดท้าย) |

### อ้างอิงสถานะของขั้นตอน (Step Status)

| สถานะ | ความหมาย |
|--------|---------|
| Pending (รอดำเนินการ) | ยังไม่เริ่ม รอขั้นตอนก่อนหน้า |
| In Progress (กำลังดำเนินการ) | กำลังทำงานอยู่ |
| Completed (เสร็จสิ้น) | เสร็จแล้ว |
| Skipped (ข้าม) | ข้ามไป (เช่น ไม่จำเป็นสำหรับล็อตนี้) |

---

### โครงสร้างเอกสาร

1. [Home Page — ศูนย์บัญชาการ](./01-home-command-center.md)
2. [Production Dashboard (แดชบอร์ดการผลิต)](./02-production-dashboard.md)
3. [Work Orders — รายการและการจัดการ](./03-work-orders.md)
4. [Work Orders — การจัดการขั้นตอน](./04-work-order-steps.md)
5. [Scheduling Board — ภาพรวมและเลย์เอาต์](./05-scheduling-board-overview.md)
6. [Scheduling Board — การมอบหมายด้วยตนเอง](./06-scheduling-manual-assignment.md)
7. [Scheduling Board — ระบบจัดตารางอัตโนมัติ](./07-auto-scheduling.md)
8. [Scheduling Board — แผงงานส่งผลิตภายนอก](./08-outside-processing-panel.md)
9. [Scheduling Board — แผงคิว QC](./09-qc-queue-panel.md)
10. [Outside Processing — การจัดการเต็มรูปแบบ](./10-outside-processing.md)
11. [Shift Roster (ตารางกะทำงาน)](./11-shift-roster.md)
12. [Production Kanban (คัมบังการผลิต)](./12-production-kanban.md)
13. [Order Traceability (การตรวจสอบย้อนกลับคำสั่งซื้อ)](./13-order-traceability.md)
14. [Schedule Adherence Report (รายงานการปฏิบัติตามตาราง)](./14-schedule-adherence.md)
