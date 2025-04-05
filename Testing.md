# 🔐 Authorization Testing Table – Phase 3

## ✅ Legend:
- ✅ = Has access
- ❌ = Blocked
- ⚠️ = Needs attention (e.g., sensitive info leaked)

---

## 📋 Access Control Matrix

| Page / Feature              | Guest | Reserver | Administrator |
|----------------------------|:-----:|:--------:|:-------------:|
| `/` (index)                |  ✅   |   ✅     |      ✅       |
| └─ View resource form      |  ❌   |   ✅     |      ✅       |
| └─ Create new resource     | ❌ *1 | ❌ *2    | ✅ *3         |
| `/login`                   |  ⚠️   |   ⚠️     |      ✅       |
| `/register`                |  ✅   |   ❌     |      ❌       |
| `/profile`                 |  ❌   |   ✅     |      ✅       |
| `/admin/users`            |  ❌   |   ❌     |      ✅       |
| `/reservation`             |  ❌   |   ✅     |      ✅       |
| `/resources`               |  ❌   |   ✅     |      ✅       |
| `/api/reservations/1`      |  ⚠️   |   ✅     |      ✅       |

---

## 📝 Notes

- *1 Guest cannot create resources (not logged in)
- *2 Reserver lacks privileges to create
- *3 Admin can manage resources (**Spec 4**)

---

## ⚠️ Issues and Attention Points

- ⚠️ Sensitive information leakage detected on `/login` or `/register` endpoints  
  → Possible exposure of session cookies or lack of secure flags

- ⚠️ Reserver has unintended access to `/profile` or data not belonging to them  
  → Potential **horizontal privilege escalation** risk

- ⚠️ Unusual HTTP status codes (403/500) observed when accessing protected resources  
  → Indicates potential misconfiguration or poor error handling

- ⚠️ Possible **authentication bypass** behavior on `/login` or `/register`  
  → Review session handling and redirect logic carefully

---

✅ This table reflects all tested pages, expected functionality by role, and major findings during browser + ZAP testing.

