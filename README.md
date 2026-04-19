# Identity Auth Service - Thiet ke chi tiet

## 1. Vai tro
Quan ly danh tinh nguoi dung va xac thuc cho toan he thong WebTour.

Muc tieu:
- Dang nhap an toan.
- Quan ly role va quyen truy cap.
- Ho tro mo rong social login.

## 2. Nhom chuc nang

### 2.1 Xac thuc
- Dang ky tai khoan.
- Dang nhap mat khau.
- Refresh token.
- Dang xuat 1 thiet bi hoac tat ca thiet bi.
- Quen mat khau, dat lai mat khau.

### 2.2 Phan quyen
- Role:
  - Customer.
  - Staff.
  - Admin.
- Permission matrix theo module core.

### 2.3 Quan tri tai khoan
- Khoa/mo tai khoan.
- Danh dau email da xac minh.
- Quan ly trang thai KYC co ban neu can mo rong.

### 2.4 Social SSO (giai doan 2)
- Google login.
- Facebook login.
- Apple login.

## 3. CRUD bat buoc
- CRUD User.
- CRUD Role.
- CRUD Permission.
- CRUD UserRole assignment.
- CRUD Session/RefreshToken metadata.
- CRUD Auth Audit Log.

## 4. Model du lieu chinh
- users:
  - id, email, phone, passwordHash, status, createdAt.
- roles:
  - id, code, name.
- permissions:
  - id, resource, action.
- user_roles:
  - userId, roleId.
- refresh_tokens:
  - tokenId, userId, deviceId, expiresAt, revokedAt.
- auth_audit_logs:
  - userId, eventType, ip, userAgent, createdAt.

## 5. API de xuat
- POST /auth/register
- POST /auth/login
- POST /auth/refresh
- POST /auth/logout
- POST /auth/forgot-password
- POST /auth/reset-password
- GET /auth/me
- POST /auth/admin/users/:id/lock
- POST /auth/admin/users/:id/unlock

## 6. Bao mat
- Hash password bang Argon2 hoac BCrypt.
- JWT access token ngan han.
- Refresh token rotating.
- Gioi han thu dang nhap sai.
- 2FA TOTP cho admin (khuyen nghi).

## 7. Event phat ra
- UserRegistered.
- UserLocked.
- PasswordChanged.
- UserLoggedIn.

Su dung event de:
- Notification Service gui mail.
- Analytics Service cap nhat so lieu auth funnel.

## 8. Techstack de xuat
- Node.js + NestJS.
- PostgreSQL hoac MongoDB (chon 1 de on dinh).
- Redis cho session blacklist va rate limiter auth.
- JWT + OAuth2/OpenID Connect.

## 9. KPI
- Login success rate > 98% (khong tinh user sai mat khau).
- p95 login latency < 300ms.
- Ty le token refresh loi < 1%.

## 10. Roadmap
- Tuan 1: register/login/refresh/logout.
- Tuan 2: role permission + audit log.
- Tuan 3: social login + 2FA admin.
