# PROJECT.md — android-player

## 這個專案是什麼

LL 宇宙的**手機控制中心**——透過 scrcpy 把 Android 手機畫面投到桌面、用電腦操控手機，並把這個能力整合進 content-engine 的拍攝與測試流程。

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

### 2. LL 各產品手機端驗證

```
✓ leaflune.org 手機版視覺
✓ reinroom.leaflune.org RWD 體驗
✓ datadojo.leaflune.org 手機端
✓ tradetrail.leaflune.org 手機端
✓ II Widget（未來）在手機 LINE 內顯示效果
✓ XX 小春老師 卡牌 app 等手機產品
```

→ 不再「我覺得手機上應該長這樣」、是「我看到手機上長這樣」

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
