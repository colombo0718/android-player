# CLAUDE.md — android-player

> 通用 LL 員工手冊（未來會 公告欄化到 `~/.claude/CLAUDE.md`）。
> 專案定位、用途、架構、坑見 `PROJECT.md`。

@PROJECT.md

---

## 開場 SOP（進來時讀什麼）

1. `PROJECT.md` — 本專案定位與工具棧
2. `TODO.md` — 當前待辦
3. `matrix-manager/UNIVERSE.md`（如可讀）— LL 宇宙當前狀態
4. `matrix-manager/meetings/` 最近 3 篇含 android-player 的會議紀錄

---

## 工作邊界

```
✓ 允許：
  - 寫 scrcpy / ADB 啟動腳本
  - 設計拍攝流程（跟 video-factory / content-engine 銜接）
  - 寫操作 know-how 進 notes/
  - 規劃 pywinauto 自動化（未來）

✗ 不要：
  - 把錄影檔 commit 進 git（用 .gitignore 擋）
  - 在本 repo 處理 CWSoft 工作（那是 cwsoft-project-tracker）
  - 主動 root 手機 / 安裝奇怪的 APK
```

---

## 與其他 LL 系統的協作

- **content-engine**：調度時可指定本專案
- **video-factory**：scrcpy 錄出來的影片進 video-factory 後製
- **image-studio**：手機畫面截圖可作為 image-studio 來源
- **agent-stream**：直播時若要展示手機畫面、用 scrcpy 加 OBS source

---

## 安全規範

- ADB 啟用後手機暴露在 LAN 上、拍片完關掉 `adb tcpip` 或拔網
- 不要把手機真實 IP 寫進 git
- recordings/ 內容可能含個人資訊、發布前審核
