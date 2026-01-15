# RESTful API Design: ระบบจองห้องประชุม (Meeting Room Booking)
> Base URL: `/api/v1`  
> Content-Type: `application/json`  
> Auth: `Authorization: Bearer <token>`  
> Roles: `user`, `staff`  
> Timezone: `Asia/Bangkok` (แนะนำส่ง/รับเป็น ISO 8601)

---

## 1) Overview
**Resources หลัก**
- `rooms` (ห้องประชุม)
- `bookings` (การจอง)
- `auth/users` (สมัคร/ล็อกอิน/โปรไฟล์)

**Booking status (แนะนำ)**
- `pending` → `approved`
- `pending` → `cancelled`
- `approved` → `cancelled`

---

## 2) Standards & Conventions

### 2.1 Naming
- ใช้ **noun** และพหูพจน์: `/rooms`, `/bookings`
- ใช้ `{id}` ใน path: `/rooms/{roomId}`

### 2.2 Query สำหรับ List
- Pagination: `page=1`, `limit=20`
- Sorting: `sort=name`, `sort=-createdAt`
- Filtering: `search`, `status`, `capacityMin`, `features`

### 2.3 Status Codes
- `200 OK`, `201 Created`, `204 No Content`
- `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`
- `409 Conflict` (เวลา booking ชน), `422 Unprocessable Entity` (validation)

### 2.4 Error Format (Standard)
```json
{
  "error": {
    "code": "BOOKING_CONFLICT",
    "message": "Room is not available in the selected time range",
    "details": []
  },
  "requestId": "req_abc123"
}
