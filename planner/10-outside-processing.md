# 10. Outside Processing — การจัดการแบบเต็ม

## การเข้าถึง Outside Processing

ไปที่ **Outside Processing** ในแถบด้านข้าง มีสามหน้าย่อย:

| หน้าย่อย | เส้นทาง | วัตถุประสงค์ |
|----------|------|---------|
| Orders | `/production/outside-processing/orders` | จัดการวงจรชีวิต OPO |
| Vendors | `/production/outside-processing/vendors` | ข้อมูลหลักซัพ |
| Fulfillments | `/production/outside-processing/fulfillments` | รายงานการติดตามการปฏิบัติตาม |

[image: opo-sidebar — ภาพหน้าจอของเมนูแถบด้านข้าง Outside Processing ที่ขยายออก]

---

## หน้า Orders

### เค้าโครงหน้า

- **แท็บ** ด้านบนสำหรับกรองสถานะ: All, Pending, Shipped, In Transit, Partial, Completed, Cancelled
- **ช่องค้นหา** — กรองตามรหัส WO, ชื่อซัพ หรือชื่อขั้นตอน
- ปุ่ม **Export** — ดาวน์โหลดเป็น CSV
- **ตาราง** แสดง Outside Processing Order ทั้งหมด

[image: opo-orders-page — ภาพหน้าจอเต็มของหน้า Orders แสดงแท็บ, ค้นหา และตาราง]

### ตาราง Orders

| คอลัมน์ | คำอธิบาย |
|--------|-------------|
| Thumbnail | มุมมอง Isometric ของชิ้นส่วน |
| WO Code | รหัส Work Order หลัก |
| Step | ชื่อขั้นตอนกระบวนการ (เช่น "Oxidation", "Heat Treatment") |
| Vendor | ชื่อซัพ |
| Qty Shipped | จำนวนที่ส่งให้ซัพ |
| Qty Received | จำนวนที่รับกลับ |
| Shipment Date | เมื่อชิ้นส่วนถูกจัดส่ง |
| Expected Return | เมื่อชิ้นส่วนควรกลับมา |
| Actual Return | เมื่อชิ้นส่วนกลับมาจริง |
| Status | ป้าย: pending, shipped, in_transit, partial, completed, cancelled |
| Overdue | ตัวบ่งชี้ ⚠ สีแดงถ้าเกินวันที่คาดว่าจะกลับ |

[image: opo-orders-table — ภาพหน้าจอของตาราง Orders พร้อมตัวอย่าง 4–5 แถวในสถานะต่างกัน]

---

## วงจรชีวิต OPO

```
Pending → Shipped → In Transit → Completed
                        │
                        └──→ Partial (รับบางส่วน, บางส่วนยังค้างอยู่)
```

### การบันทึกการจัดส่ง

1. ค้นหา OPO ที่มีสถานะ **Pending** ในตาราง
2. คลิกแถวหรือเมนูการดำเนินการ
3. คลิก **Record Shipment**
4. **กล่องโต้ตอบ Shipment** จะเปิดขึ้น:
   - วันจัดส่ง (ค่าเริ่มต้นเป็นวันนี้)
   - จำนวนที่จัดส่ง
   - หมายเหตุ
5. คลิก **Save**
6. สถานะเปลี่ยนเป็น **Shipped**

[image: opo-shipment-dialog — ภาพหน้าจอของกล่องโต้ตอบ Shipment พร้อมฟิลด์วันที่, จำนวน และหมายเหตุ]

### การบันทึกการรับ

1. ค้นหา OPO ที่มีสถานะ **Shipped** หรือ **In Transit**
2. คลิก **Record Receipt**
3. **กล่องโต้ตอบ Receipt** จะเปิดขึ้น:
   - วันรับ (ค่าเริ่มต้นเป็นวันนี้)
   - จำนวนที่รับ
   - หมายเหตุ
4. คลิก **Save**
5. ถ้ารับจำนวนทั้งหมด → สถานะเปลี่ยนเป็น **Completed**
6. ถ้ารับบางส่วน → สถานะเปลี่ยนเป็น **Partial**

[image: opo-receipt-dialog — ภาพหน้าจอของกล่องโต้ตอบ Receipt]

### การพิมพ์ Packing Slip

1. คลิกเมนูการดำเนินการบน OPO
2. เลือก **Print Packing Slip** (🖨)
3. Packing Slip ที่ปรับให้พิมพ์ได้จะเปิดพร้อม:
   - ที่อยู่ซัพ
   - รายละเอียด WO และขั้นตอน
   - ข้อมูลจำนวนและวัสดุ
   - Barcode สำหรับการติดตาม

[image: opo-packing-slip — ภาพหน้าจอของมุมมองพิมพ์ Packing Slip]

---

## แผ่น OPO Detail

คลิกแถว OPO ใดก็ได้เพื่อเปิดแผ่นรายละเอียดจากด้านขวา:

| ส่วน | เนื้อหา |
|---------|---------|
| ส่วนหัว | รหัส WO, ชื่อขั้นตอน, ชื่อซัพ |
| สถานะ | ป้ายสถานะปัจจุบันพร้อมตัวบ่งชี้เกินกำหนด |
| วันที่ | วันจัดส่ง, วันที่คาดว่าจะกลับ, วันที่กลับจริง |
| จำนวน | จัดส่ง, รับ, ค้างอยู่ |
| ไฟล์แนบ | ไฟล์ที่อัปโหลด (แบบ, PO ฯลฯ) |
| การดำเนินการ | Record Shipment, Record Receipt, Cancel, Print Packing Slip |

[image: opo-detail-sheet — ภาพหน้าจอของแผ่น OPO Detail]

---

## หน้า Vendors

จัดการข้อมูลหลักซัพ:

- ปุ่ม **+ Vendor** เพื่อเพิ่มซัพใหม่
- ตารางแสดง: รหัสซัพ, ชื่อ, ผู้ติดต่อ, ระยะเวลานำ, สถานะ
- การดำเนินการแก้ไขและลบ

[image: opo-vendors-page — ภาพหน้าจอของหน้า Vendors พร้อมตาราง]

### การเพิ่มซัพ

1. คลิก **+ Vendor**
2. กรอก: รหัสซัพ, ชื่อ, ผู้ติดต่อ, โทรศัพท์, อีเมล, ที่อยู่, ระยะเวลานำเริ่มต้น (วัน)
3. คลิก **Save**

[image: opo-vendor-form — ภาพหน้าจอของฟอร์มซัพ]

---

## การติดตามเกินกำหนด

OPO ที่เกินวันที่คาดว่าจะกลับถูกแจ้งเตือน:
- ป้ายสถานะสีแดงในตาราง Orders
- ไอคอน ⚠ เตือน
- ปรากฏในรายการที่ต้องดำเนินการในหน้าหลักเป็น "Late OPO Returns"
- ปรากฏเป็นแถบสีแดงในแผง Outside Processing ของบอร์ดจัดตาราง

[image: opo-overdue-indicators — ภาพหน้าจอแสดงตัวบ่งชี้เกินกำหนดในตาราง Orders]
