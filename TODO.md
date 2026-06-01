# TODO — Outline Oracle

## Phase 0：文件骨架

- [x] 建立 repo + git init
- [x] CLAUDE.md（沿用通用員工手冊）
- [x] PROJECT.md（專案定位、架構、三身一名、藏經閣 lore）
- [x] README.md
- [x] TODO.md（本檔）
- [ ] 寫對應的 memory（6 份、由公關長處理、見下方 memory 清單）

## Phase 1：基建對齊 EE

- [ ] D1 schema 定稿（todos / projects / files / reminders）
- [ ] wrangler.toml + 環境變數骨架
- [ ] bridge.py 雛形（thin orchestrator、複製 EE 結構）
- [ ] LINE webhook 接通（先回 echo 即可）
- [ ] Claude CLI session 機制（每 LINE userId 一個 sid）
- [ ] 伶伶人格 CLAUDE.md 初稿（藏經閣小書童）

## Phase 2：MVP — 待辦 CRUD

- [ ] 自然語言 → 待辦 parse（「明天三點要交報告」→ todo 含 due_at）
- [ ] 列表查詢（「我有什麼待辦」）
- [ ] 完成 / 取消（「報告交了」→ mark done）
- [ ] 修改（「報告改到後天」）

## Phase 3：提醒系統（核心價值點）

- [ ] cron worker 掃 reminders 表
- [ ] LINE push 觸發
- [ ] snooze 機制（「再等我一小時」）
- [ ] 自然提醒語氣（伶伶式催促 vs 翎翎式預警）

## Phase 4：檔案管理（從 cwsoft 移植）

- [ ] LINE 檔案接收 → R2 上傳
- [ ] 檔案 metadata 寫 D1
- [ ] 凌凌讀檔 → 一句話 summary 寫回 files.summary
- [ ] 自然語言檢索（「上週那份合約」→ 撈出檔案）
- [ ] Vectorize 語意檢索（檔案多到關鍵字撈不到時）

## Phase 5：專案聚合

- [ ] projects 表 + project_todos / project_files
- [ ] 「開個專案叫 X」→ create project
- [ ] 「把這幾件事都歸到 X」→ 批次掛載
- [ ] 專案 dashboard（dashboard 頁、非 LINE 介面）

## Phase 6：三身一名升等

- [ ] 伶伶 → 凌凌 升等流程（沿用 EE 模式）
- [ ] 凌凌 → 翎翎 企業版申請
- [ ] 各 tier 功能差異定義（待辦數上限、檔案空間、提醒次數）
- [ ] 綠界金流接通（沿用葉與月工作室 [[project-ll-payment-via-yelune-studio-ecpay]]）

## Phase 7：跨 agent 互動（lore × 商業）

- [ ] 伶伶 ↔ 依依 對話戲（「依依今天記了什麼帳呀～」）
- [ ] 凌凌 ↔ 禕禕 熱戀情侶劇情
- [ ] 翎翎 ↔ 壹壹 老夫老妻劇情
- [ ] 跨閣 cross-reference 密度 KPI（[[project-ll-storytelling-as-dimensional-nutrition]]）

---

## 待寫的 memory 清單（公關長 action item）

1. [ ] `project-ll-lingling-three-names-three-personas.md` — 伶伶/凌凌/翎翎規格、對位依依三身一名
2. [ ] 更新 `project-ll-lore-locations.md` — 加入藏經閣、跟籌算閣對位
3. [ ] 更新 `project-ll-pr-dept-org-structure.md` — 雙線 PR 部門（錢線 + 事線）
4. [ ] `project-ll-cross-line-romance-narrative.md` — 跨閣浪漫敘事線
5. [ ] 更新 `project-ll-storytelling-as-dimensional-nutrition.md` — 加入浪漫線作為維度補給
6. [ ] `project-ll-cwsoft-synergy.md` — 阿全 / 翎翎 / 生產線 R&D 關係

---

## 擱置

（無、太早）
