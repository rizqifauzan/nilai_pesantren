# Auth Strategy

## 🔐 Authentication Overview

Sistem authentication menggunakan kombinasi:
1. **Default Admin Credentials** di `.env` untuk akses awal
2. **Database Users Table** untuk verifikasi dan otorisasi

---

## 📋 Database Schema: `users`

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin') NOT NULL DEFAULT 'admin',
    status ENUM('active', 'inactive') NOT NULL DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `id` | BIGINT PK | Primary key auto-increment |
| `username` | VARCHAR(50) UNIQUE | Username untuk login |
| `password` | VARCHAR(255) | Password terenkripsi (bcrypt) |
| `role` | ENUM('admin') | Role pengguna (hanya admin) |
| `status` | ENUM('active', 'inactive') | Status akun |
| `created_at` | TIMESTAMP | Waktu pembuatan |
| `updated_at` | TIMESTAMP | Waktu terakhir update |

---

## ⚙️ Default Admin Configuration (.env)

```env
# Admin Default Credentials
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin123
```

---

## 🔑 Default Admin Account

| Field | Value |
|-------|-------|
| Username | `admin` |
| Password | `admin123` |
| Role | `admin` |
| Status | `active` |

**⚠️ PENTING:** Segera ubah password default setelah first login!

---

## 🔐 Password Hashing

Password di-hash menggunakan **bcrypt** dengan salt rounds = 10.

```php
// Example: Hash password
$hashedPassword = password_hash($plainPassword, PASSWORD_BCRYPT);

// Verify password
if (password_verify($inputPassword, $storedHash)) {
    // Login berhasil
}
```

---

## 🔄 Auth Flow

```
1. User input username & password
2. Cek credentials di .env (ADMIN_USERNAME, ADMIN_PASSWORD)
   ↓ Jika match
3. Login berhasil, generate token/session
   ↓ Jika tidak match
4. Cek di database users table
   ↓ Jika match & status=active
5. Login berhasil, generate token/session
   ↓ Jika tidak match
6. Login gagal
```

---

## 🎯 Rules

1. **Admin** - Akses penuh ke semua fitur sistem
2. Hanya role `admin` yang diizinkan (sesuai request)
3. User dengan status `inactive` tidak bisa login
4. Password default harus diganti setelah first login

---

## 💡 Rekomendasi Penggunaan

### 1. First Login Flow
```
Admin baru deploy sistem
    ↓
Login dengan admin/admin123 (dari .env)
    ↓
Redirect ke halaman ubah password
    ↓
Password default diganti
    ↓
Simpan hash password baru ke DB users table
```

### 2. User Management
- Hanya admin yang bisa login (sesuai design)
- Tambah/ubah user admin melalui CLI atau direct DB insert
- Password user baru harus di-hash sebelum insert ke DB

### 3. Keamanan
- **Selalu gunakan HTTPS** di production
- Password di .env adalah fallback, primary auth di DB
- Set `.env` password berbeda dari password di DB
- Gunakan environment variable yang kuat untuk JWT_SECRET

### 4. Endpoint Contoh
```
POST /api/auth/login
  Body: { "username": "admin", "password": "admin123" }
  Response: { "token": "xxx", "user": {...} }

POST /api/auth/change-password
  Body: { "current_password": "admin123", "new_password": "xxx" }

GET /api/auth/me
  Header: Authorization: Bearer {token}
```

### 5. Migrasi Default Admin ke DB
```php
// Saat first run, insert default admin ke DB jika belum ada
if (!User::where('username', env('ADMIN_USERNAME'))->exists()) {
    User::create([
        'username' => env('ADMIN_USERNAME'),
        'password' => bcrypt(env('ADMIN_PASSWORD')),
        'role' => 'admin',
        'status' => 'active'
    ]);
}
```
