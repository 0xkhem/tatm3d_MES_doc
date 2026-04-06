# Knowledge / Master Data (ข้อมูลหลัก)

## คืออะไร?

Knowledge คือรากฐานของระบบทั้งหมด ทุกโมดูลอื่น — Work Orders, Scheduling, Quality, Outside Processing — ต้องอาศัยข้อมูลหลักที่ตั้งค่าไว้ที่นี่ก่อน ไม่มีอะไรทำงานได้หากไม่มีข้อมูลนี้

คิดว่า Knowledge คือขั้นตอนการตั้งค่า: กำหนดส่วนประกอบพื้นฐานครั้งเดียว และส่วนที่เหลือของระบบจะใช้โดยอัตโนมัติ

## ลำดับการตั้งค่า

ลำดับการตั้งค่าที่แนะนำ (แต่ละขั้นตอนขึ้นอยู่กับขั้นตอนก่อนหน้า):

```
1. Materials              — วัสดุที่ใช้ผลิตชิ้นส่วน
2. Process Definitions    — การดำเนินงานที่ทำ (CNC Milling, Deburring ฯลฯ)
3. Equipment Types        — หมวดหมู่เครื่องจักร (5-Axis CNC Mill, CMM ฯลฯ)
4. Equipment Instances    — เครื่องจักรจริงในโรงงาน
5. Process Routes         — ลำดับขั้นตอนสำหรับประเภทชิ้นส่วน
6. Operators              — ช่างปฏิบัติงานพร้อมรหัส PIN
7. Customers              — ลูกค้าที่ผลิตชิ้นส่วนให้
8. Vendors                — ซัพสำหรับงาน Outside Service
9. Factory Modeling       — เค้าโครงทางกายภาพ (Workshops, Workstations)
10. Schedule Modeling     — ปฏิทินทำงาน (Shifts, ชั่วโมงทำงาน, วันหยุด)
```

## Materials (วัสดุ)

วัตถุดิบและชิ้นส่วนสำเร็จรูป แต่ละวัสดุมีรหัส (`MAT-0001`) ชื่อ หมวดหมู่ และหน่วยวัด วัสดุถูกอ้างอิงโดย Work Orders และ Inventory Transactions

## Process Definitions (คำจำกัดความกระบวนการ)

เทมเพลตการดำเนินงานที่ใช้ซ้ำได้ — "CNC Milling", "Deburring", "Anodizing", "QC Inspection" แต่ละคำจำกัดความเชื่อมโยงกับ Equipment Type (เพื่อให้ Scheduler รู้ว่าเครื่องจักรไหนรันได้) และสามารถตั้งค่าเป็น Outside Service ได้ (ทำให้สร้าง OPO)

## Process Routes (เส้นทางกระบวนการ)

ลำดับ Process Definitions ที่ชิ้นส่วนต้องผ่าน ตัวอย่าง:

```
Die Casting → Deburring → CNC Milling → Anodizing (outside) → QC → Packing
```

เมื่อสร้าง Work Order จาก Route ขั้นตอนจะถูกสร้างโดยอัตโนมัติตามลำดับนี้

## Equipment Types & Instances (ประเภทและเครื่องจักร)

Equipment Types คือหมวดหมู่ (เช่น "3-Axis CNC Mill") Equipment Instances คือเครื่องจักรจริง (`EQP-0001`) Scheduler มอบหมาย Operation ให้ Instance ไม่ใช่ Type

## Operators (ช่างปฏิบัติงาน)

ช่างปฏิบัติงานในหน้างานพร้อมชื่อ รหัส และ PIN 4 หลัก ช่างล็อกอินเข้า Operator Interface โดยใช้ PIN สามารถมอบหมายทักษะให้ช่างเพื่อติดตามว่าช่างคนไหนมีคุณสมบัติรันการดำเนินงานไหน

## Customers & Vendors (ลูกค้าและซัพ)

Customers คือบริษัทที่ผลิตชิ้นส่วนให้ Vendors คือผู้ให้บริการภายนอกสำหรับ Outside Processing ทั้งคู่มีข้อมูลติดต่อและสถานะ (Active/Inactive)

## Factory Modeling (การจำลองโรงงาน)

กำหนดโครงสร้างทางกายภาพของโรงงาน:
- **Factory** → **Workshops** (Bay/พื้นที่) → **Workstations** (ตำแหน่งแต่ละจุด)
- Equipment Instances ถูกมอบหมายให้ Workstations
- ใช้โดย Factory Floor Overview สำหรับแผนที่ภาพ

## Schedule Modeling (การจำลองตาราง)

กำหนดปฏิทินทำงาน:
- **Shifts** — เวลาเริ่ม, เวลาสิ้นสุด, วันในสัปดาห์
- **Work Calendar** — วันไหนเป็นวันทำงาน, วันหยุด, การหยุดงาน
- ใช้โดย Scheduling Engine เพื่อคำนวณกำลังการผลิตที่มีและข้ามวันที่ไม่ทำงาน

## Knowledge Health Dashboard

ตัวตรวจสอบความสมบูรณ์ที่แสดงว่าข้อมูลหลักไหนขาดหายหรือไม่สมบูรณ์ แจ้งเตือนสิ่งต่างๆ เช่น: "ไม่มี Process Routes ที่กำหนด", "Equipment ไม่มี Type ที่มอบหมาย", "Operators ไม่มีทักษะ" มีประโยชน์ระหว่างการตั้งค่าเริ่มต้นและการตรวจสอบเป็นระยะ
