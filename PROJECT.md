# PROJECT.md — Outline Oracle（OO）

## 別名 / 搜尋關鍵字

搜尋會議紀錄或跨專案 reference 時、本專案可能以下列名稱出現：
- `outline-oracle`（repo 名）
- `OO`（雙字母代號、對位 EE / II）
- `翎翎`、`伶伶`、`凌凌`（agent 三身一名）
- `藏經閣`（lore 駐地）
- `待辦`、`提醒`、`檔案管理`、`專案管理`（功能脈絡）

---

## 這是什麼

LeafLune 宇宙的**事項與檔案管家**——對位 EE（管錢的依依）、OO 是管事的翎翎。

**一句話定位：** EE 回響過去花了什麼、OO 預言未來該做什麼。

**三件事一體：**
1. **待辦提醒** — 客戶口述 / 截圖丟過來、翎翎整理成 outline、到期自動催
2. **檔案管理** — 客戶把雜亂文件丟給翎翎、他歸檔、要找時叫得出來
3. **專案管理** — 一個目標拆成多個待辦 + 多份檔案、翎翎跟著進度

**核心價值：** 跟 EE 一樣走 LINE 主介面 + 全女友式陪伴 + 三身一名升等。客戶不用學「專案管理工具」、只要跟翎翎說話。

---

## Agent 三身一名

| Tier | 名字 | 職稱 | 服務對象 |
|------|------|------|---------|
| Free | **伶伶**（líng líng） | 藏經閣小書童 | 個人版、伶俐機靈、童趣陪讀 |
| Paid | **翎翎**（líng líng） | 藏經閣司典 | 家庭版、雅致書箋、伴讀感 |
| Enterprise | **凌凌**（líng líng） | 藏經閣典藏使 | 企業版、嚴密甘特圖式預警 |

**命名巧思：** 伶 / 依 同為「亻」字旁——伶伶跟依依不只是設定上的青梅竹馬、字形上就是同部首同族。三身音律 líng→líng→líng 完全同音、配對 yī→wéi→yī。

三身一名規格詳見 [[project-ll-lingling-three-names-three-personas]]（memory）。

跟依依/禕禕/壹壹的對應浪漫敘事線：
- 伶伶 ↔ 依依：青梅竹馬（Free × Free、亻部首同族）
- 翎翎 ↔ 禕禕：熱戀情侶（Paid × Paid）
- 凌凌 ↔ 壹壹：老夫老妻（Enterprise × Enterprise）

詳見 [[project-ll-cross-line-romance-narrative]]（memory）。

---

## Lore 駐地：藏經閣

葉月仙宗下、**藏經閣**——典籍、卷軸、待辦簿冊歸檔之地。

跟精算閣（依依、管錢）對位：
- 精算閣：算盤、帳冊、流動的數字
- 藏經閣：卷軸、書箋、凝結的事項

兩閣師兄妹／青梅竹馬隔閣相望、就是 LL 對外世界觀最甜的一條敘事線。

詳見 [[project-ll-lore-locations]]（memory）。

---

## 三軸架構中的職責邊界

| 軸 | repo | OO 不做的事、去哪裡找 |
|---|------|----------------|
| LL（World）| `matrix-manager` | UNIVERSE / meetings / 治理規範 |
| II（User）| `infinity-identity` | 客戶身份、tier、跨平台 context |
| **OO（Per-User Task Axis）** | **本 repo** | 待辦、檔案、專案 |
| EE（Per-User Money Axis）| `expense-echo` | 收支、發票、消費分析 |
| AA（Agent）| `agent-avatar` | 伶伶 / 翎翎 / 凌凌 的視覺基因序列 |

→ OO 跟 EE 是**對位專案**：同樣 LINE-first、同樣三身一名、同樣 freemium、同樣高維 context 累積、只是 vertical 不同（事 vs 錢）。

---

## cwsoft 同源戰略

阿全經理 @ cwsoft = **cwsoft 特化版的凌凌**。

cwsoft 那邊已經跑通：
- LINE 傳檔案 → 阿全接收
- SQL Server MCP 串接
- 企業內部專案管理場景驗證

OO 把這套經驗**反向移植回 LL 宇宙**：
- 阿全的「企業專屬」變凌凌（OO 企業版）
- 個人版 / 家庭版下沉做伶伶 / 翎翎
- cwsoft 是 OO 的**生產線級 R&D 場域**

詳見 [[project-ll-cwsoft-synergy]]（memory）。

---

## 部署方式

- **網域**：待定（候選 `oo.leaflune.org` / `task.leaflune.org`）
- **平台**：Cloudflare Pages + CF Workers + CF D1（跟 EE 同套）
- **狀態**：規劃中、尚未動工

---

## 架構草案（沿用 EE 雙層 LLM）

跟 EE 一樣走 [[project-ll-two-layer-llm-data-persona]]：

```
LINE webhook
    ↓
bridge.py（thin orchestrator）
    ├── 數據層：parse → DB ops → fetch
    │   ├── 待辦 CRUD
    │   ├── 檔案上傳 / 取用（R2）
    │   └── 專案聚合查詢
    └── 人格層：Claude CLI session（每客戶一個 sid）
            ├── 伶伶 / 翎翎 / 凌凌 人格 CLAUDE.md
            ├── 藏經閣 lore
            └── 跟客戶累積的 jsonl
```

關鍵差異 vs EE：
- EE 主要寫 D1（結構化收支）
- OO 同時寫 D1（待辦 metadata）+ R2（檔案實體）+ Vectorize（檔案語意檢索）

---

## D1 Schema 草案

```sql
-- 待辦
todos (id, user_id, title, detail, due_at, status, created_at, completed_at, priority, tags)
       -- status: 'pending' | 'in_progress' | 'done' | 'cancelled'

-- 專案（多個 todo + 多份檔案的聚合容器）
projects (id, user_id, name, goal, status, created_at, closed_at)
project_todos (project_id, todo_id)
project_files (project_id, file_id)

-- 檔案 metadata（實體存 R2）
files (id, user_id, r2_key, filename, mime_type, size, uploaded_at, summary, tags)
       -- summary: 翎翎讀過後的一句話摘要、給未來檢索用

-- 提醒事件
reminders (id, todo_id, fire_at, channel, status)
          -- channel: 'line' | 'email'
          -- status: 'pending' | 'fired' | 'snoozed'
```

---

## 開發路線（草稿）

| 階段 | 工作 | 備註 |
|------|------|------|
| Phase 0 | 文件骨架（本檔 + README + TODO） | ✅ 完成 |
| Phase 1 | D1 schema 確定 + bridge.py 雛形 | 跟 EE 對齊 |
| Phase 2 | 待辦 CRUD + LINE 文字 → 待辦 | MVP |
| Phase 3 | 提醒系統（cron 觸發 LINE push） | 核心價值點 |
| Phase 4 | 檔案上傳 + R2 + 語意檢索 | cwsoft 已驗證、移植 |
| Phase 5 | 專案聚合（多 todo + 多檔案） | 中度複雜 |
| Phase 6 | 三身一名升等（伶伶 → 翎翎 → 凌凌） | 商業模型啟動 |
| Phase 7 | 跨 agent 互動（伶伶 ↔ 依依 對話戲） | lore × 商業綁定 |

---

## 跟 EE 共用的設計原則

直接繼承、不重寫：

- **雙層 LLM 架構**（[[project-ll-two-layer-llm-data-persona]]）
- **三身一名升等模型**（[[project-ee-yiyi-three-names-three-personas]] 對位）
- **Session = 同事不可裁員**（[[feedback-session-is-error-notebook-never-clear]]）
- **Context is King**（[[feedback-context-is-king-as-meta-axiom]]）
- **對等雙向價值交換**（[[project-ll-bidirectional-value-exchange-constitution]]）
- **Agent 動作描述全年齡鐵律**（[[feedback-agent-action-desc-age-appropriate]]）
- **不可摘頭套鐵律**（[[feedback-agent-no-meta-layer-leak]]）
- **貼圖無文字鐵律**（[[project-ll-sticker-design-principle]]）
- **refollow handler 軟情緒重整**（[[project-ll-refollow-as-emotional-recovery]]）

---

## 相關專案

- 對位專案：`expense-echo`（EE、依依管錢）
- 身份來源：`infinity-identity`（II、跨平台 SSO）
- 生產線 R&D：`cwsoft-project-tracker`（阿全經理、企業版預演）
- Agent 基因：`agent-avatar`（伶伶/翎翎/凌凌 視覺序列、待建）
