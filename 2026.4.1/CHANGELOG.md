# Changelog - OpenClaw v2026.4.1

## 🔄 การเปลี่ยนแปลงจากเวอร์ชันก่อนหน้า

### ✅ เพิ่มใหม่

| Path | คำอธิบาย |
|------|-----------|
| `agents.defaults.maxConcurrent` | จำนวน agent ที่ทำงานพร้อมกันได้ (ค่าเริ่มต้น: 4) |
| `agents.defaults.subagents.maxConcurrent` | จำนวน subagent ที่ทำงานพร้อมกันได้ (ค่าเริ่มต้น: 8) |
| `plugins.entries.minimax.config` | Plugin config สำหรับ MiniMax provider |
| `messages.ackReactionScope` | กำหนด scope ของ acknowledgment reaction |

### 🔧 เปลี่ยนแปลง

| Path | เปลี่ยนจาก | เปลี่ยนเป็น |
|------|-----------|-------------|
| `agents.defaults.timeoutSeconds` | 60 | 600 |

### ⚠️ หมายเหตุสำคัญ

1. **LINE Plugin exports ขัดแย้ง** - มี exports ที่ชื่อซ้ำกับ plugin-sdk ใหม่:
   - `isSenderAllowed` → `checkLineSenderAllowed`
   - `normalizeAllowFrom` → `normalizeLineAllowFrom`
   - `downloadLineMedia` → `getLineMediaContent`
   **วิธีแก้:** ปิด LINE plugin ชั่วคราว หรือรอ fix จากทีม

2. **Config merge behavior** - การใช้ `config.patch` vs `config.apply` มีผลต่อโครงสร้าง:
   - `config.apply` = แทนที่ config ทั้งหมด
   - `config.patch` = merge กับ existing config

---

## 📊 โครงสร้าง Config แบบคร่าว

```
config.json
├── meta                    # Version metadata
├── wizard                  # Setup wizard state
├── agents.defaults         # Agent defaults
│   ├── model
│   ├── contextPruning
│   ├── compaction
│   ├── timeoutSeconds      ⚠️ เพิ่มจาก 60 → 600
│   ├── heartbeat
│   ├── sandbox
│   ├── maxConcurrent       🆕 เพิ่มใหม่
│   └── subagents.maxConcurrent  🆕 เพิ่มใหม่
├── commands
├── channels                # Telegram, Discord, LINE
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
│   ├── line                ⚠️ ปิดใช้งานชั่วคราว (export conflict)
│   └── minimax             🆕 มี config ใหม่
├── tools
│   ├── profile
│   ├── elevated
│   └── exec
└── messages                🆕 เพิ่มใหม่
    └── ackReactionScope
```
