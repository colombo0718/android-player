# TODO.md — android-player

---

## ⬡ MM 同步

| title | status | importance | energy | effort | due | next_action | tags |
|-------|--------|------------|--------|--------|-----|-------------|------|
| WiFi ADB 設定（vivo V40 Lite）| active | 1 | l | 30 | | 等有 WiFi 環境後執行 | android-player,setup,wifi |
| OBS 抓 scrcpy 視窗測試 | queued | 1 | l | 20 | | 等 WiFi ADB 通了之後 | android-player,obs |
| 3 min vibe coding 首支腳本 | queued | 2 | m | 60 | | Bolt.new 寫 app + scrcpy demo | vibe-coding |
| 首支試拍 | idea | 2 | m | 90 | | 跑通整套流程 | vibe-coding |
| pywinauto 自動化 | idea | 3 | h | 240 | | 等試拍幾次手動有經驗再做 | automation |

---

## 環境準備

### ✅ 已完成
- [x] 裝 scrcpy 3.3.4 + adb 1.0.41（C:\Users\USER\android-player\bin\scrcpy）
- [x] 裝 Google USB Driver（C:\Users\USER\android-player\bin\google-usb-driver）
- [x] 手機開「開發者選項」+「USB 偵錯」

### 🔴 卡住：USB ADB 在 vivo V40 Lite 上不通

**問題診斷（2026-05-12 排查）**：
- Windows 端認到「ADB Interface OK」、但 adb daemon 看不到設備
- Manufacturer 是「WinUsb Device」、不是「Google, Inc.」
- 根因：vivo VID_2D95 不在 Google USB Driver 的 android_winusb.inf 內
- Google driver 只 hardcode 了 VID_18D1（Google 自家設備）

**為什麼擱置這條路**：
- 修法 1：改 INF 加 vivo VID → 破壞數位簽章、要關閉 Windows driver 簽章驗證、要重啟 + 桌面會有「測試模式」水印、工程量太大
- 修法 2：找 vivo 官方 USB Driver → vivo 台灣官網沒提供 PC Suite
- 修法 3：Universal ADB Driver（ClockworkMod）→ **2026-05-12 驗證：項目失維護、下載連結 404 死了**
- 修法 4：UniversalAdbDriver（koushik dutta GitHub）→ 也是 2019 年後沒更新、不確定含 VID_2D95

→ 沒有現成且維護中的 driver 包含 vivo VID
→ 唯一剩下選項都需要重啟 Windows + 工程量大
→ ROI 太低、放棄

**為什麼可以擱置**：
- WiFi ADB 完全繞過 USB driver 問題
- 拍 3 min vibe coding 時、WiFi ADB 反而更好（沒線擋畫面）
- 短期內優先走 WiFi 這條

### 🟡 主推：WiFi ADB（等有 WiFi 環境）

```
手機端：
  1. 開發者選項 → 開啟「無線偵錯」
  2. 點「無線偵錯」進入設定頁
  3. 點「使用配對碼配對裝置」→ 跳出彈窗
  4. 把彈窗的「配對碼」+「IP:port」告訴 AI
  5. 不要關掉彈窗、保持顯示

電腦端：
  adb pair <IP>:<port>      # 輸入配對碼
  adb connect <IP>:<port>    # 注意：connect 用的 port 跟 pair 不同
  adb devices                # 應該看到設備
  scrcpy                     # 啟動鏡像

前提：手機跟電腦必須同一個 WiFi（不是手機分享熱點給電腦那種）
```

---

## 第一輪驗證（WiFi ADB 通了之後）

- [ ] scrcpy 抓 leaflune.org 看視覺
- [ ] scrcpy 抓 reinroom.leaflune.org（RR-RWD 驗證）
- [ ] scrcpy 抓 datadojo.leaflune.org（手機端 RWD）
- [ ] scrcpy 抓 tradetrail.leaflune.org（手機端）
- [ ] scrcpy 抓 xuanxuexi.leaflune.org（XX 手機體驗）

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

- **USB ADB 路徑（vivo V40 Lite）**
  > 擱置原因：vivo VID_2D95 不在 Google USB Driver 支援範圍
  > 解套要動 INF + 關閉簽章驗證、工程量大、ROI 低
  > WiFi ADB 已可解決 + 拍片場景更適合
  > 若未來換非 vivo 手機、USB 應該直接 work

- **iPhone 鏡像**
  > 擱置原因：要用 QuickTime、跟本 repo 範圍不同、需求未到

---

## 已完成

- [x] 專案建立（PROJECT / CLAUDE / README / TODO + .gitignore）
- [x] PROJECT.md 強化戰略定位（LL 通用手機驗證儀器）
- [x] CLAUDE.md 從 matrix-manager 複製
- [x] android-player repo push 上 GitHub
- [x] 裝 scrcpy 3.3.4（含 adb 1.0.41）
- [x] 裝 Google USB Driver（雖然對 vivo 沒效果、但裝在 store 不影響）
- [x] 手機端 USB 偵錯 + USB 模式設為「檔案傳輸」
- [x] 診斷 vivo USB ADB 問題（VID 不相容、放棄走 WiFi）
