# 穿戴甲客製化設計與保養 LLM Wiki 知識庫規範 (agent.md)

本文件定義本知識庫（Nail Care & Press-on Wiki）的架構規範、Obsidian 雙向連結格式、語系術語辭典、YAML Frontmatter 規則，以及後續轉換為「教學 HTML 簡報」的標準工作流程。

---

## 1. 知識庫核心定位與目標
1. **客製化穿戴甲知識資產庫**：完整沉澱從甲型測量、材質工藝、配戴卸除到日常護理的專業知識。
2. **原子化筆記 (Atomic Notes)**：每個概念獨立成篇，內含完整的上下文定義，便於重組引用。
3. **動態教學簡報生成引擎**：原生相容 Marp / Slidev Markdown 語法，能依據教學需求迅速拼裝輸出高品質 HTML 互動教學簡報。

---

## 2. 目錄架構與分工權責

```text
nail-care-wiki/
├── 00_Home_MOC/             # 知識地圖與主題 MOC (Map of Content)
│   ├── index.md             # 知識庫總導圖
│   ├── MOC_甲型與尺寸.md
│   ├── MOC_設計與工藝.md
│   ├── MOC_穿戴與卸除.md
│   ├── MOC_日常保養與修復.md
│   └── MOC_教學簡報庫.md
├── 01_甲型測量與規格/       # 尺寸測量、甲型對照、弧度修磨
├── 02_材質工藝與設計/       # 貓眼光澤、油畫堆疊、十指構圖、立體雕花
├── 03_穿戴與卸除步驟/       # 果凍膠、固態膠操作、解膠劑、安全卸除
├── 04_日常保養與問題排查/   # 4小時黃金保養、防水維護、真甲修護、收納
├── 05_教學簡報素材/         # Marp / Slidev 教學簡報規格與簡報源文件
├── assets/                  # 示範照片、圖解、圖表與設計稿
├── raw_data/                # 外部原始資料與文字草稿歸檔區
└── agent.md                 # 本系統規範指南（本檔）
```

---

## 3. Obsidian 雙向連結與語法規範

1. **內部連結 (Wikilinks)**：
   - 概念引用統一使用 `[[筆記名稱]]`。
   - 語句流暢需調整文字時使用別名：`[[筆記名稱|顯示文字]]`。
   - 禁止使用含路徑的硬編碼連結（如 `[[01_甲型/筆記]]`），以保持筆記移動時的彈性。
2. **多媒體嵌入**：
   - 圖片統一存放於 `assets/` 資料夾。
   - 引用語法：`![[檔名.jpg]]` 或 `![說明文字](../assets/檔名.jpg)`。
3. **麵包屑導航 (Breadcrumbs)**：
   - 每篇原子筆記頂部皆須標註上層 MOC 連結，例如：
     ```markdown
     > 上層主題：[[MOC_甲型與尺寸]] | 總目錄：[[index]]
     ```
4. **Callout 提示框**：
   - 關鍵注意事項使用 `[!NOTE]`、`[!TIP]`、`[!WARNING]`、`[!CAUTION]`。

---

## 4. 語系與美甲專業術語辭典（台灣習慣規範）

本知識庫一律採用**繁體中文（台灣習慣用語）**，並在必要時備註業界英文名稱。避免使用非台灣慣用詞彙：

| 規範使用術語 (Preferred) | 避免使用 / 常見對照詞 (Avoid) | 英文對照 / 定義備註 |
| :--- | :--- | :--- |
| **穿戴甲** | 穿戴美甲、貼片甲、假指甲 | Press-on Nails |
| **果凍膠** | 果凍貼、雙面貼片膠 | Jelly Sticker / Adhesive Tabs |
| **固態膠 / 固態貼片膠** | 固態膠水、固體膠 | Solid UV Gel |
| **凝膠 / 光療凝膠** | 甲油膠、指甲油光療 | Gel Polish |
| **真甲 / 原生甲** | 本甲、自甲 | Natural Nails |
| **前置保養 / 前置作業** | 甲面處理、打磨真甲 | Nail Prep (去油去水、甘皮修整) |
| **甘皮 / 指緣** | 死皮、後緣皮 | Cuticle |
| **指緣油** | 營養油、指皮油 | Cuticle Oil |
| **游離緣 / 游離線** | 游離區、肉線 | Hyponychium / Free Edge |
| **包邊** | 封邊、包頭 | Cap the Free Edge |
| **海綿拋光條 / 砂條** | 搓條、打磨條 | Buffer / Nail File |
| **櫸木棒** | 木棒、推死皮棒 | Wooden Cuticle Pusher |
| **解膠劑** | 卸膠水、解膠水 | Debonder / Nail Glue Remover |
| **甲面高點** | 甲弧度最高點 | Apex |

---

## 5. 原子筆記 YAML Frontmatter 規範

所有新建立之原子筆記與教學單元均須包含標準 Frontmatter：

```yaml
---
title: 筆記繁體中文標題
category: 甲型測量與規格 # 對應五大核心分類之一
tags:
  - 穿戴甲
  - 客製化設計
  - 保養護理
moc: "[[MOC_對應分類]]"
slide_ready: true # 是否可直接作為簡報單元
summary: 一句話摘要此篇核心概念（供簡報大綱檢索）
created: 2026-11-23
updated: 2026-11-23
---
```

---

## 6. 教學 HTML 簡報 (Marp) 生成標準

當使用者要求根據知識庫內容生成「教學簡報」時，LLM 應輸出相容 Marp 規格的 Markdown，並可一鍵匯出為獨立 HTML：

1. **簡報檔頭配置**：
   ```yaml
   ---
   marp: true
   theme: default
   paginate: true
   size: 16:9
   header: "穿戴甲客製化設計與日常保養教學"
   footer: "Nail Care & Press-on Wiki"
   style: |
     section {
       font-family: 'PingFang TC', 'Microsoft JhengHei', sans-serif;
     }
     h1 { color: #d63384; }
     h2 { color: #495057; }
   ---
   ```
2. **投影片分頁原則**：
   - 使用 `---` 明確切分每張投影片。
   - 每張投影片限一個核心概念，文字簡潔，多使用列點與圖示。
   - 首頁使用 `<!-- _class: lead -->` 居中放大標題。
   - 投影片底部使用 `<!-- note: ... -->` 附加講師口說備忘稿。
3. **輸出格式**：
   - 可直接使用 VS Code Marp 外掛或 CLI (`@marp-team/marp-cli`) 指令轉為單一 HTML 檔案：
     `npx @marp-team/marp-cli --html <presentation.md> -o <presentation.html>`

---

## 7. AI Agent 協作工作流程 (Workflow for LLM)

當使用者提供新資料或要求擴充知識庫時，AI Agent 應遵循以下 SOP：

1. **解析與標準化**：
   - 檢查用語是否符合台灣繁體中文美甲標準。
   - 提煉核心觀點，拆解為原子級筆記。
2. **寫入指定分類目錄**：
   - 依「流程生命週期」歸入 `01_` 至 `05_` 資料夾。
   - 寫入標準 YAML Frontmatter，並在內文建立與相關筆記的 `[[Wikilinks]]`。
3. **同步更新 MOC**：
   - 自動將新筆記加入對應之 `MOC_*.md` 及 `00_Home_MOC/index.md`。
4. **簡報素材準備**：
   - 檢查是否帶有 `slide_ready: true`，若需要生成簡報，將模組串聯至 `05_教學簡報素材/` 的教學投影片中。
