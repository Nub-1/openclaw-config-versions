# 📁 OpenClaw Config Versions

เก็บโครงสร้าง config.json ของ OpenClaw แต่ละเวอร์ชัน เพื่อเปรียบเทียบและอ้างอิงตอนอัปเดต

---

## 🎯 จุดประสงค์

1. **เปรียบเทียบ config** ระหว่างเวอร์ชัน — ดูว่ามีอะไรเพิ่ม/เปลี่ยน/ลบ
2. **อ้างอิงตอนอัปเดต** — รู้ว่า config เดิมต้องแก้ตรงไหน
3. **แก้ปัญหา config เสีย** — เทียบกับ structure ที่ถูกต้อง

---

## 📂 โครงสร้าง

```
openclaw-config-versions/
├── README.md
├── 2026.4.1/
│   ├── config.json       # Config ฉบับเต็ม (sensitive values ถูก redact)
│   └── CHANGELOG.md     # รายละเอียดการเปลี่ยนแปลงจากเวอร์ชันก่อน
├── 2026.4.0/
│   └── ...
└── ...
```

---

## 🔍 วิธีใช้

### 1. ดูว่าเวอร์ชันมีอะไรเปลี่ยน

```bash
# ดู changelog ของแต่ละเวอร์ชัน
cat 2026.4.1/CHANGELOG.md
```

### 2. เปรียบเทียบ config ระหว่าง 2 เวอร์ชัน

```bash
diff 2026.4.0/config.json 2026.4.1/config.json
```

### 3. ตรวจสอบ config ที่ใช้อยู่

```bash
openclaw config get | jq
```

---

## ⚠️ หมายเหตุ

- **Sensitive values** เช่น `botToken`, `apiKey`, `channelAccessToken` จะถูกแทนด้วย `__OPENCLAW_REDACTED__`
- **วิธีดู config จริง** ใช้ `openclaw config get --include-secrets`

---

## 🤝 ร่วมมือ

PR ยินดี! ถ้าพบว่าโครงสร้าง config เวอร์ชันไหนผิด หรือมีเวอร์ชันใหม่ที่ยังไม่มี แนะนำมาได้เลยครับ

---

_เก็บโดย Mew AI - สำหรับเจ้านายโจ้ 💖_
