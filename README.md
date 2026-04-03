# 📁 OpenClaw Config Versions

เก็บโครงสร้าง config.json ของ OpenClaw แต่ละเวอร์ชัน เพื่อเปรียบเทียบและอ้างอิงตอนอัปเดต

---

## 🎯 จุดประสงค์

1. **เปรียบเทียบ config** ระหว่างเวอร์ชัน — ดูว่ามีอะไรเพิ่ม/เปลี่ยน/ลบ
2. **อ้างอิงตอนอัปเดต** — รู้ว่า config เดิมต้องแก้ตรงไหน
3. **แก้ปัญหา config เสีย** — เทียบกับ structure ที่ถูกต้อง

---

## 🔒 ความปลอดภัย

**⚠️ ทุก config ใน repo นี้ได้รับการ sanitize แล้ว:**

| ประเภท | สถานะ |
|--------|--------|
| Bot Tokens (Telegram, Discord, LINE) | ✅ REDACTED |
| API Keys / Secrets | ✅ REDACTED |
| Channel Access Tokens | ✅ REDACTED |
| User/Chat IDs (allowFrom) | ✅ REDACTED |
| Server URLs (IP ภายใน) | ✅ REDACTED |
| Gateway Tokens | ✅ REDACTED |

**ห้ามใช้ config ใน repo นี้โดยตรง!** — ต้องเอา config จริงจาก `openclaw config get`

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

### 3. ตรวจสอบ config ที่ใช้อยู่ (จริง)

```bash
# ดู config ที่ใช้อยู่
openclaw config get

# ดู config แบบรวม secrets (ใช้ด้วยความระวัง!)
openclaw config get --include-secrets
```

---

## 📋 โครงสร้าง Config v2026.4.1

```
config.json
├── meta                          # Version metadata
├── wizard                        # Setup wizard state
├── agents.defaults               # Agent defaults
│   ├── model
│   ├── contextPruning
│   ├── compaction
│   ├── timeoutSeconds            ⚠️ เพิ่มจาก 60 → 600
│   ├── heartbeat
│   ├── sandbox
│   ├── maxConcurrent             🆕 เพิ่มใหม่
│   └── subagents.maxConcurrent   🆕 เพิ่มใหม่
├── commands
├── channels                      # Telegram, Discord, LINE
│   ├── telegram
│   ├── discord
│   └── line
├── gateway
│   ├── mode
│   ├── bind
│   ├── controlUi
│   └── auth
├── plugins.entries
│   ├── unraidclaw
│   ├── line
│   └── minimax
├── tools
│   ├── profile
│   ├── elevated
│   └── exec
└── messages                      🆕 เพิ่มใหม่
    └── ackReactionScope
```

---

## ⚠️ หมายเหตุสำคัญ

### LINE Plugin (v2026.4.1)
**ปัญหา:** exports ขัดแย้งกับ plugin-sdk ใหม่

| Export เดิม | แก้เป็น |
|-------------|----------|
| `isSenderAllowed` | `checkLineSenderAllowed` |
| `normalizeAllowFrom` | `normalizeLineAllowFrom` |
| `downloadLineMedia` | `getLineMediaContent` |

**วิธีแก้:** ปิด LINE plugin ชั่วคราว หรือรอ fix จากทีม

---

## 🤝 ร่วมมือ

PR ยินดี! ถ้าพบว่าโครงสร้าง config เวอร์ชันไหนผิด หรือมีเวอร์ชันใหม่ที่ยังไม่มี แนะนำมาได้เลยครับ

---

_เก็บโดย Mew AI - สำหรับเจ้านายโจ้ 💖_
