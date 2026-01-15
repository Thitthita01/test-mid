# RESTful API Design

> Base URL: `/api`  
> Auth: ใช้ `Authorization: Bearer <token>` สำหรับ endpoint ที่ต้องล็อกอิน  
> Roles: `user` (ผู้ใช้ทั่วไป), `staff` (เจ้าหน้าที่)

---

## API Endpoints (Summary Table)

| HTTP Method | Endpoint | Description | Request Body | Response (Success) | Status Code |
|---|---|---|---|---|---|
| GET | /api/rooms | ดึงรายการห้องทั้งหมด (รองรับ filtering) | - | `[{room}, ...]` | 200 |
| GET | /api/rooms/:id | ดึงข้อมูลห้องเดียว | - | `{room}` | 200 |
| POST | /api/rooms | สร้างห้องใหม่ (เจ้าหน้าที่) | `{...}` | `{room}` | 201 |
| PUT | /api/rooms/:id | แก้ไขข้อมูลห้อง (เจ้าหน้าที่) | `{...}` | `{room}` | 200 |
| DELETE | /api/rooms/:id | ลบห้อง (เจ้าหน้าที่) | - | `{message}` | 200 |
| GET | /api/bookings | ดึงรายการจองทั้งหมด (เจ้าหน้าที่) | - | `[{booking}, ...]` | 200 |
| GET | /api/bookings/my | ดึงการจองของตัวเอง | - | `[{booking}, ...]` | 200 |
| POST | /api/bookings | สร้างการจองใหม่ | `{...}` | `{booking}` | 201 |
| DELETE | /api/bookings/:id | ยกเลิกการจอง (เจ้าของ/เจ้าหน้าที่) | - | `{message}` | 200 |
| PATCH | /api/bookings/:id/approve | อนุมัติการจอง (เจ้าหน้าที่) | `{status}` | `{booking}` | 200 |
| POST | /api/auth/login | Login | `{email,password}` | `{token,user}` | 200 |
| POST | /api/auth/register | Register | `{name,email,password}` | `{token,user}` | 201 |
| GET | /api/users/profile | ดูข้อมูลตัวเอง | - | `{user}` | 200 |

---


## Data Models (ตัวอย่างโครงสร้าง)
###Request Body
{
  "room_id": 101,
  "booking_date": "2026-01-15",
  "start_time": "09:00",
  "end_time": "12:00",
  "purpose": "ประชุมโครงการ",
  "attendees": 8
}

### Response (201 Created)

{
  "room_id": 1,
  "room_name": "Room A",
  "capacity": 20,
  "location": "Building 1, Floor 3",
  "equipment": ["Projector", "Whiteboard"],
  "status": "available",
  "createdAt": "2026-01-15T04:00:00.000Z",
  "updatedAt": "2026-01-15T04:00:00.000Z"
}
