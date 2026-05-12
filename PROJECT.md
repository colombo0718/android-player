# PROJECT.md — android-player

## 這個專案是什麼

LL 宇宙的**手機控制中心 / 通用手機驗證儀器**——透過 scrcpy 把 Android 手機畫面投到桌面、用電腦操控手機，服務 LL 所有需要「在真手機跑一遍」的子產品。

### 為什麼必要

```
LL 對外品牌幾乎全部是 web 產品：
  RR  reinroom.leaflune.org      ← 手機 RWD 是核心體驗
  DD  datadojo.leaflune.org      ← 高中校園用、學生大多用手機
  LL  leaflune.org               ← 品牌入口、手機流量大宗
  SS  strategyspace.leaflune.org ← 對戰平台、手機端必須
  XX  xuanxuexi.leaflune.org     ← 兒童語言學習、手機 / 平板優先
  TT  tradetrail.leaflune.org    ← 即時金融資訊、手機常用
  II  id.leaflune.org            ← Widget 在手機 LINE 跑、必須驗證

→ 「在真手機跑」是 LL 所有對外產品的硬需求
→ F12 viewport 模擬不夠真實
→ android-player = LL 通用手機驗證儀器
```

地位等同：
- `image-studio` — 畫室（圖像生成）
- `video-factory` — 錄影棚（影片自動化）
- `agent-stream` — 直播間（直播 + VTuber）
- `android-player` — 手機操控房（本專案）

---

## LL 三軸定位

- **空間軸**：對內（生產基礎設施）
- **時間軸**：現在（建設中）
- **內容軸**：跨軸通用工具（不限學習/玩樂）

---

## 主要用途

### 1. 3 min vibe coding 系列拍攝

```
左視窗：Bolt.new / Windsurf / 編輯器
右視窗：scrcpy（真 Android 手機畫面）
OBS 抓全螢幕 → 觀眾看到「真實落地」
```

→ 取代過去用 F12 viewport 模擬手機的「假手機感」

### 2. LL 所有對外產品的手機端驗證（高頻使用）

**這是 android-player 的主要用途、不是次要用途**。LL 對外品牌幾乎全部 web、手機體驗是核心：

```
高優先（已上線、有真實用戶）：
  ✓ leaflune.org           品牌入口
  ✓ reinroom.leaflune.org  RR RWD（最近的工作重點）
  ✓ datadojo.leaflune.org  DD 校園端
  ✓ tradetrail.leaflune.org TT 金融端
  ✓ xuanxuexi.leaflune.org XX 語言學習

中優先（規劃中）：
  ✓ id.leaflune.org        II Widget 在手機 LINE 顯示
  ✓ strategyspace.leaflune.org SS 對戰平台
  ✓ XX 小春老師 卡牌 app

→ 不再「我覺得手機上應該長這樣」、是「我看到手機上長這樣」
→ 每次改動推上 CF Pages 後、開 android-player 看一眼 = 標準流程
```

### 3. 自動化拍攝（未來可能）

```
pywinauto 控制 scrcpy 視窗 + 模擬觸控
+ Claude 寫 prompt 觸發 demo
+ video-factory 接收輸出

→ 「無人值守錄手機畫面 demo 影片」可能性
```

---

## 工具棧

| 工具 | 用途 | 狀態 |
|------|------|------|
| **scrcpy** | Android 鏡像 + 控制（核心） | 待裝 |
| **ADB** | Android Debug Bridge（scrcpy 前置） | 待裝 |
| **OBS** | 錄影 / 串流 | 既有 |
| **pywinauto** | 視窗自動化（未來） | 規劃中 |
| **ffmpeg** | 後製（既有 video-factory pipeline） | 既有 |

---

## 架構概覽（v0.1，建設中）

```
android-player/
├── PROJECT.md          本檔
├── CLAUDE.md           AI 協作規範（引用 ~/.claude/CLAUDE.md）
├── README.md           專案介紹
├── TODO.md             待辦
├── docs/               硬約束（連線指令、設定文件）
├── notes/              軟敘述（操作 know-how、實驗紀錄）
├── scripts/            自動化腳本（pywinauto / 啟動 scrcpy）
└── recordings/         錄影暫存（.gitignore）
```

---

## 連線方式

### USB（穩定、適合初次測試）

```bash
# 手機開「開發者選項」→ USB 偵錯
# 接 USB 線
scrcpy
```

### WiFi ADB（拍片時推薦、無線）

```bash
# 第一次設定（手機接 USB）：
adb tcpip 5555

# 之後（同一 WiFi 下、拔線即可）：
adb connect <手機IP>:5555
scrcpy
```

---

## 已知考量 / 坑

- scrcpy 預設不錄音、要錄手機音用 `--audio-source=output`（需要 Android 11+）
- 螢幕鎖定時 scrcpy 仍能控、但畫面是鎖定狀態
- 同 WiFi 下、有些路由器隔離 client、無法 adb connect
- iPhone 不適用（要另用 QuickTime 鏡像）
- 手機電量會被 scrcpy 持續消耗、長時拍片建議接電

---

## 跟其他執行層的關係

```
content-engine（調度層）
       │
       ├── image-studio       靜態圖像
       ├── video-factory      影片後製
       ├── agent-stream       直播 / VTuber
       └── android-player     手機端 demo 與測試 ← 本專案
```

content-engine 排程拍片時、可以指定「這集需要 android-player」。

---

## 開發規範

- commit 訊息：繁體中文
- recordings/ 不進 git（在 .gitignore）
- 操作指令收進 docs/、實驗心得收進 notes/

---

## 相關資源

- scrcpy GitHub：https://github.com/Genymobile/scrcpy
- ADB 文件：https://developer.android.com/tools/adb
