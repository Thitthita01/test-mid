# RESTful API Endpoints: ระบบจองห้องประชุม
> Base URL: `/api/v1`  
> Content-Type: `application/json`  
> Auth: `Authorization: Bearer <token>`  
> Roles: `user`, `staff` (เจ้าหน้าที่)

---

## 1) Resources หลัก
- **Rooms**: ห้องประชุม
- **Bookings**: การจอง
- **Users/Auth**: login, register, profile

---

## 2) Rooms (ห้องประชุม)

### 2.1 ดึงรายการทั้งหมด (พร้อม filtering)
**GET** `/rooms`

**Query Params (ตัวอย่างที่ใช้บ่อย)**
- `search` (ค้นหาชื่อห้อง/อาคาร)
- `building`, `floor`
- `capacityMin`, `capacityMax`
- `features` (comma-separated) เช่น `projector,whiteboard`
- `status` เช่น `active|inactive`
- `page` (default 1), `limit` (default 20)
- `sort` เช่น `name`, `-createdAt`

**Example**
`GET /api/v1/rooms?capacityMin=10&features=projector,video_conf&page=1&limit=10&sort=name`

**200 Response**
```json
{
  "data": [
    {
      "id": "room_101",
      "name": "Meeting Room A",
      "building": "B1",
      "floor": 3,
      "capacity": 12,
      "features": ["projector", "whiteboard"],
      "status": "active"
    }
  ],
  "meta": { "page": 1, "limit": 10, "totalItems": 1, "totalPages": 1 }
}
