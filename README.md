# android-player

LL 宇宙的**手機控制中心**。透過 scrcpy 把 Android 手機畫面投到桌面、用電腦操控手機。

## 用途

- **3 min vibe coding 系列拍攝**：左 code 視窗、右真手機畫面
- **LL 各產品手機端驗證**：leaflune / reinroom / datadojo / tradetrail / II Widget …
- **未來自動化**：pywinauto 控制 scrcpy + 自動 demo 影片

## 工具棧

scrcpy（核心）+ ADB + OBS + pywinauto（規劃中）

## 快速啟動（USB）

```bash
# 1. 手機開啟「開發者選項」→ USB 偵錯
# 2. 接 USB 線
# 3. 啟動
scrcpy
```

## WiFi ADB（無線拍片）

```bash
adb tcpip 5555
adb connect <手機IP>:5555
scrcpy
```

## 在 LL 宇宙的位置

```
content-engine（調度層）
       │
       ├── image-studio    畫室
       ├── video-factory   錄影棚
       ├── agent-stream    直播間
       └── android-player  手機操控房  ← 本專案
```

詳細定位見 [PROJECT.md](PROJECT.md)。
