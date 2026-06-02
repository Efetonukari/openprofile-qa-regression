
# OpenProfile QA Regression Suite

Product: Open Profile — https://staging.open-profile.hng14.com  
Environment: Staging  
**QA Engineer: Efetonukari  
**Date:** June 2, 2026  

---

## 🧪 What This Repository Contains

This repository contains the full regression test suite for the 
OpenProfile MVP, covering authentication flows, profile management, 
search, and end-to-end user journeys.

---

## 📁 Test Coverage

| Module | Endpoints Tested | Status |
|---|---|---|
| Auth - Register | POST /api/v1/users | ✅ Covered |
| Auth - Login | POST /api/v1/auth/login | ✅ Covered |
| Auth - Get User | GET /api/v1/auth/me | ✅ Covered |
| Auth - Logout | POST /api/v1/auth/logout | ✅ Covered |
| Auth - Refresh Token | POST /api/v1/auth/refresh-token | ✅ Covered |
| Profiles - Get Content | GET /api/v1/profiles/content | ✅ Covered |
| Profiles - Dashboard | GET /api/v1/profiles/dashboard | ✅ Covered |
| Search | GET /api/v1/search | ✅ Covered |
| Users - List | GET /api/v1/users | ✅ Covered |

---

## 🔗 Postman Collection

Access the full test suite here:  
https://www.postman.com/galactic-astronaut-992253/stage-7/collection/ugoh9n8/stage-7-copy?action=share&source=copy-link&creator=33078126

---

## ▶️ How to Run Tests

### Option 1 — Run in Postman (Recommended)
1. Click the Postman link above
2. Fork the collection to your workspace
3. Set these collection variables:
   - `baseUrl` = `https://api.staging.open-profile.hng14.com`
   - `userEmail` = your test email
   - `userPassword` = your test password
4. Click **Run collection**

### Option 2 — Run via Newman (CLI)
```bash
# Install Newman
npm install -g newman

# Run the collection
newman run openprofile-regression.json \
  --env-var "baseUrl=https://api.staging.open-profile.hng14.com" \
  --env-var "userEmail=your@email.com" \
  --env-var "userPassword=yourpassword" \
  --reporters cli,json
```

---

## 📊 Test Execution Order

Run requests in this exact order for proper API chaining:
POST /api/v1/users          → Register
POST /api/v1/auth/login     → Login (saves token automatically)
GET  /api/v1/auth/me        → Verify session
GET  /api/v1/profiles/content → Get profile
GET  /api/v1/search?q=test  → Search users
POST /api/v1/auth/logout    → End session

---

## ✅ Pass/Fail Summary

| Test Case | Result |
|---|---|
| TC-001: Register new user | ✅ Pass |
| TC-002: Login with valid credentials | ✅ Pass |
| TC-003: Get current user | ✅ Pass |
| TC-004: Get profile content | ✅ Pass |
| TC-005: Logout user | ✅ Pass |
| TC-006: Search users | ✅ Pass |

---

## 🐛 Known Bugs

| Bug ID | Description | Severity |
|---|---|---|
| BUG-001 | Login response time exceeded 3s (3355ms) | Low |
