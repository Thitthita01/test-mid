# RESTful API Design (Table)

> Base URL: `/api/v1`  
> Format: JSON (`Content-Type: application/json`)  
> Auth: `Authorization: Bearer <token>` (ถ้ามี)

---

## 1) Conventions

- **Resource (นาม)** ใช้พหูพจน์: `/users`, `/books`
- **ID** อยู่ใน path: `/users/{userId}`
- **Query** สำหรับ filter/sort/pagination: `?page=1&limit=20&sort=-createdAt`
- **HTTP Methods**
  - `GET` อ่านข้อมูล (ไม่ควรเปลี่ยน state)
  - `POST` สร้าง
  - `PUT` แทนที่ทั้งก้อน (ถ้าไม่ส่ง field = ถือว่าลบทิ้ง)
  - `PATCH` แก้บางส่วน
  - `DELETE` ลบ
- **Status Codes (หลักๆ)**
  - `200 OK` สำเร็จทั่วไป
  - `201 Created` สร้างสำเร็จ
  - `204 No Content` สำเร็จแต่ไม่ส่ง body (นิยมกับ DELETE)
  - `400 Bad Request` ข้อมูลไม่ถูกต้อง
  - `401 Unauthorized` ไม่ได้ล็อกอิน/โทเคนผิด
  - `403 Forbidden` ไม่มีสิทธิ์
  - `404 Not Found` ไม่พบ
  - `409 Conflict` ชนกัน เช่น unique ซ้ำ
  - `422 Unprocessable Entity` ผ่านรูปแบบแต่ validation ไม่ผ่าน
  - `500 Internal Server Error` ฝั่งเซิร์ฟเวอร์

---

## 2) Resource: Users

| # | Endpoint | Method | Description | Path Params | Query Params | Request Body (JSON) | Success Response | Status |
|---|----------|--------|-------------|------------|--------------|----------------------|------------------|--------|
| 1 | `/users` | GET | List users | - | `page,limit,search,sort` | - | `{ "data":[...], "meta":{...} }` | 200 |
| 2 | `/users/{userId}` | GET | Get user by id | `userId` | - | - | `{ "data": {...} }` | 200 |
| 3 | `/users` | POST | Create user | - | - | `{ "name":"", "email":"" }` | `{ "data": {...} }` | 201 |
| 4 | `/users/{userId}` | PATCH | Update user (partial) | `userId` | - | `{ "name":"New" }` | `{ "data": {...} }` | 200 |
| 5 | `/users/{userId}` | DELETE | Delete user | `userId` | - | - | *(no body)* | 204 |

**Example: List users**
- `GET /api/v1/users?page=1&limit=10&search=rabbit&sort=-createdAt`

**Example Response (pagination)**
```json
{
  "data": [
    { "id": "u_1", "name": "Rabbit", "email": "rabbit@mail.com", "createdAt": "2026-01-15T04:00:00Z" }
  ],
  "meta": { "page": 1, "limit": 10, "totalItems": 1, "totalPages": 1 }
}
