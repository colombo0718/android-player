# TODO.md — android-player

---

## ⬡ MM 同步

| title | status | importance | energy | effort | due | next_action | tags |
|-------|--------|------------|--------|--------|-----|-------------|------|
| 裝 scrcpy + ADB 環境 | active | 1 | l | 30 | | scoop install scrcpy 或 GitHub release | android-player,setup |
| USB 連線測試 | active | 1 | l | 15 | | 手機開發者模式 + USB 偵錯 | android-player,setup |
| WiFi ADB 設定 | queued | 1 | l | 15 | | adb tcpip + adb connect | android-player,setup |
| OBS 抓 scrcpy 視窗測試 | queued | 1 | l | 20 | | 確認錄出畫面 OK | android-player,obs |
| 3 min vibe coding 首支腳本 | queued | 2 | m | 60 | | Bolt.new 寫 app + scrcpy demo | vibe-coding |
| 首支試拍 | idea | 2 | m | 90 | | 跑通整套流程 | vibe-coding |
| pywinauto 自動化 | idea | 3 | h | 240 | | 等試拍幾次手動有經驗再做 | automation |

---

## 環境準備（必做）

- [ ] 裝 scrcpy
  > Windows：`scoop install scrcpy` 或 [GitHub release](https://github.com/Genymobile/scrcpy/releases)
- [ ] 手機開「開發者選項」→ USB 偵錯
- [ ] USB 線連線 + 跑 `scrcpy` 看畫面
- [ ] WiFi ADB 設定（之後拍片用、不被線擋畫面）
- [ ] OBS 抓 scrcpy 視窗測試

---

## 第一輪驗證

- [ ] scrcpy 抓 leaflune.org 看視覺
- [ ] scrcpy 抓 reinroom.leaflune.org（RR-RWD 驗證）
- [ ] scrcpy 抓 datadojo.leaflune.org（手機端 RWD）

---

## 3 min vibe coding 系列整合

- [ ] 第一支影片腳本設計
  > 主題建議：「Bolt.new 3 分鐘寫個手機端工具 + 立刻在手機跑」
  > 視覺：左 Bolt.new、右 scrcpy 真手機
- [ ] 首支試拍 + 後製
- [ ] 整合進 video-factory pipeline

---

## 自動化（未來）

- [ ] pywinauto 控制 scrcpy 視窗 + 模擬觸控
- [ ] 「無人值守錄 demo」實驗
- [ ] 跟 video-factory pipeline 對接

---

## 擱置

- iPhone 鏡像（要用 QuickTime、跟本 repo 範圍不同）— 擱置原因：需求未到、不擴張範圍

---

## 已完成

- [x] 專案建立（PROJECT / CLAUDE / README / TODO）
