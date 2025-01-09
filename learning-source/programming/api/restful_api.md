## **HTTP & RESTful API Cheat Sheet**

#### **HTTP Overview**
HTTP (Hypertext Transfer Protocol) adalah protokol komunikasi yang digunakan untuk mentransfer data antara client (browser atau aplikasi) dan server melalui jaringan. HTTP bersifat stateless, artinya setiap permintaan tidak memiliki hubungan dengan permintaan sebelumnya.

**Komponen Penting HTTP:**
1. **Client**: Pihak yang membuat permintaan (browser, aplikasi).
2. **Server**: Pihak yang memproses permintaan dan memberikan respons.
3. **Request**: Permintaan yang dikirimkan oleh client ke server.
4. **Response**: Respons yang diberikan server kepada client.
5. **URI (Uniform Resource Identifier)**: Alamat sumber daya di server (contoh: `/users`).
6. **HTTP Version**: Versi protokol yang digunakan (contoh: `HTTP/1.1`, `HTTP/2`).

---
---
---
---
### **\HTTP Request**
1. **Request Line**: Menentukan tindakan yang diminta (method, URL, HTTP version).  
   - Contoh: `GET /users HTTP/1.1`
2. **Headers**: Metadata permintaan (misal: `Content-Type`, `Authorization`).
3. **Body**: Data yang dikirim (opsional, biasanya pada `POST`, `PUT`, `PATCH`).
4. **Parameters**: Tambahan data untuk request.
   - **Query Parameters**: Ditulis di URL setelah `?` (contoh: `/users?name=john`).
   - **Path Parameters**: Ditulis dalam URL path (contoh: `/users/{id}` -> `/users/123`).

---
### **\HTTP Response**
1. **Status Line**: Informasi status permintaan (HTTP version, status code, reason phrase).  
   - Contoh: `HTTP/1.1 200 OK`
2. **Headers**: Metadata tentang respons (misal: `Content-Type`, `Content-Length`).
3. **Body**: Data balasan (opsional, bisa berupa JSON, HTML, dll).

---
#### **HTTP Status Codes**
- **1xx (Informational)**: Permintaan diterima, sedang diproses.
  - Contoh: `100 Continue`, `101 Switching Protocols`.
- **2xx (Success)**: Permintaan berhasil.
  - Contoh: `200 OK`, `201 Created`, `204 No Content`.
- **3xx (Redirection)**: Aksi tambahan diperlukan.
  - Contoh: `301 Moved Permanently`, `302 Found`, `304 Not Modified`.
- **4xx (Client Error)**: Kesalahan dari sisi client.
  - Contoh: `400 Bad Request`, `401 Unauthorized`, `404 Not Found`.
- **5xx (Server Error)**: Kesalahan di sisi server.
  - Contoh: `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`.

---
#### **HTTP Request Methods**
1. **GET**: Mengambil data (idempotent, tanpa body).  
   - Contoh: `GET /users`
2. **POST**: Membuat sumber daya baru (menggunakan body).  
   - Contoh:
     ```
     POST /users
     Content-Type: application/json
     {
       "name": "John Doe"
     }
     ```
3. **PUT**: Memperbarui sumber daya secara penuh (idempotent).  
   - Contoh: `PUT /users/123`
4. **PATCH**: Memperbarui sebagian sumber daya (idempotent).  
   - Contoh: `PATCH /users/123`
5. **DELETE**: Menghapus sumber daya (idempotent).  
   - Contoh: `DELETE /users/123`
6. **OPTIONS**: Meminta informasi tentang metode HTTP yang didukung.  
   - Contoh: `OPTIONS /users`
7. **HEAD**: Sama seperti `GET`, tetapi hanya mengambil header.  
   - Contoh: `HEAD /users`
8. **TRACE**: Mengembalikan permintaan untuk debugging (jarang digunakan).  
   - Contoh: `TRACE /users`

---
#### **Perbedaan HTTP dan API yang Menggunakan HTTP**
- **HTTP**:
  - Protokol komunikasi.
  - Digunakan untuk mentransfer data dalam format apa pun (HTML, JSON, XML, dll.).
  - Berfokus pada mekanisme komunikasi (request-response).
- **API yang Menggunakan HTTP**:
  - Menggunakan HTTP sebagai medium komunikasi.
  - Memanfaatkan method HTTP (seperti `GET`, `POST`) untuk berinteraksi dengan sumber daya.
  - Biasanya menggunakan format standar untuk data seperti JSON atau XML.

**Contoh Hubungan HTTP dengan API**:
- HTTP hanya menentukan bagaimana data dikirim: "Permintaan ini akan menggunakan method `GET` untuk mengambil sesuatu dari URL tertentu."
- API menentukan logika dan aturan: "API ini menyediakan endpoint `/users` yang merespons dengan daftar pengguna jika Anda mengirimkan `GET /users`."

---
#### **Prinsip REST (Representational State Transfer)**
1. **Stateless**: Setiap permintaan bersifat independen, server tidak menyimpan status sesi client.
2. **Client-Server Architecture**: Ada pemisahan antara client (pengguna) dan server (penyedia layanan).
3. **Uniform Interface**: Interaksi dengan sumber daya menggunakan antarmuka seragam.
   - Identifikasi sumber daya melalui URI.
   - Manipulasi melalui representasi (JSON, XML).
   - Pesan bersifat self-descriptive.
   - HATEOAS (Hypermedia as the Engine of Application State).
4. **Layered System**: Mendukung lapisan tambahan seperti proxy untuk skalabilitas.
5. **Cacheability**: Data dapat di-cache untuk meningkatkan performa.
6. **Code on Demand (Opsional)**: Server dapat mengirimkan kode eksekusi ke client (contoh: JavaScript).

