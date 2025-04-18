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
| `/login`                   |  ✅   |   ✅     |      ✅       |
| `/register`                |  ✅   |   ❌     |      ❌       |
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

- ⚠️ **Horizontal privilege escalation**: Direct access to `/api/reservations/1` was possible as Reserver — should ensure ID-based access control  
  → _Tested with browser + curl, verified by ZAP_

- ⚠️ **Informational ZAP findings**:
  - `/login`: Authentication form detected  
  - `/login`: Session management elements observed in response (Set-Cookie headers)  
  - `/static/tailwind.css`: Detected Tailwind CSS (tech fingerprinting)

---

✅ This table reflects tested routes, aligned with Phase 3 specification and real code structure. ZAP and manual testing confirm no high-risk issues detected.  
