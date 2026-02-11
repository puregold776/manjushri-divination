# Google Analytics 事件追蹤指南

## 已設定的追蹤事件

網站現在會追蹤以下使用者互動：

### 1. 擲骰占卜 (dice_roll)
- **觸發時機**：使用者點擊「🎲 擲骰占卜」按鈕
- **事件名稱**：`dice_roll`
- **參數**：
  - `event_category`: "divination"
  - `event_label`: "Roll Dice Button"

### 2. 手動設定卦象 (manual_selection)
- **觸發時機**：使用者選擇音節後點擊「確認卦象」
- **事件名稱**：`manual_selection`
- **參數**：
  - `event_category`: "divination"
  - `event_label`: "Manual Hexagram Selection"
  - `hexagram_name`: 卦象名稱（例如：「金色蓮花」）

### 3. 分享功能 (share)
- **觸發時機**：使用者點擊任何分享按鈕
- **事件名稱**：`share`
- **參數**：
  - `method`: 分享方式
    - "Copy Link" - 複製分享連結
    - "Facebook" - 分享到 Facebook
    - "LINE" - 分享到 LINE
    - "Threads" - 分享到 Threads
    - "Twitter" - 分享到 Twitter/X
    - "WeChat" - 分享到微信
    - "Web Share API" - 使用系統分享功能
  - `content_type`: "hexagram"
  - `item_id`: 卦象名稱

---

## 如何在 Google Analytics 中查看事件數據

### 方法 1: 即時報表（立即可用）

1. 登入 Google Analytics：https://analytics.google.com/
2. 選擇「manjumo.com」資源
3. 點擊左側「報表」→「即時」
4. 在「依事件名稱」區段可以看到：
   - 目前正在發生的事件
   - 每個事件的即時數量

**測試建議**：
- 自己訪問網站並點擊不同按鈕
- 在即時報表中應該會立即看到事件出現

### 方法 2: 事件報表（24小時後數據較完整）

1. 點擊左側「報表」→「參與」→「事件」
2. 會看到所有事件的列表：
   - `dice_roll` - 擲骰占卜次數
   - `manual_selection` - 手動設定次數
   - `share` - 分享總次數
   - `page_view` - 頁面瀏覽（自動追蹤）

3. 點擊任何事件名稱可以看到詳細資訊

### 方法 3: 探索（自訂分析）

1. 點擊左側「探索」
2. 建立「自由格式」探索
3. 可以自訂分析，例如：

**範例 1：查看最受歡迎的分享方式**
- 維度：`Event name` = "share"
- 次要維度：`method`（自訂維度）
- 指標：`Event count`

結果會顯示：
```
Facebook: 150次
LINE: 320次
Copy Link: 89次
Twitter: 45次
...
```

**範例 2：查看最多人手動選擇的卦象**
- 維度：`Event name` = "manual_selection"
- 次要維度：`hexagram_name`
- 指標：`Event count`

結果會顯示哪個卦象最多人主動查詢。

**範例 3：擲骰 vs 手動選擇比例**
- 維度：`Event name`
- 篩選器：`dice_roll` 或 `manual_selection`
- 指標：`Event count`

可以了解使用者更喜歡用哪種方式占卜。

---

## 實用分析問題

安裝事件追蹤後，您可以回答這些問題：

### 使用者行為
- ❓ 有多少人使用「擲骰占卜」？
- ❓ 有多少人使用「手動設定卦象」？
- ❓ 擲骰和手動選擇的比例是？
- ❓ 使用者更傾向用哪種方式？

### 分享行為
- ❓ 最受歡迎的分享方式是什麼？（LINE、Facebook、Twitter？）
- ❓ 有多少人願意分享他們的卦象？
- ❓ 哪個卦象最常被分享？

### 卦象熱度
- ❓ 哪個卦象最多人手動查詢？
- ❓ 哪個卦象的頁面瀏覽量最高？
- ❓ 吉卦和凶卦的查看比例？

### 轉換率
- ❓ 多少訪客實際使用了占卜功能？
- ❓ 占卜後有多少人分享結果？
- ❓ 平均每個使用者占卜幾次？

---

## 建立自訂報表範例

### 報表 1：分享管道效能

**目的**：了解哪個分享按鈕最有效

1. 探索 → 自由格式
2. 維度：
   - `Event name` = "share"
   - `method`（拖到列）
3. 指標：
   - `Event count`（拖到值）
4. 加入圖表：橫條圖

### 報表 2：占卜方式偏好

**目的**：使用者更喜歡擲骰還是手動選擇

1. 探索 → 自由格式
2. 維度：
   - `Event name`
   - 篩選：只顯示 `dice_roll` 和 `manual_selection`
3. 指標：
   - `Event count`
   - `Users`（多少不同的使用者）
4. 加入圖表：圓餅圖

### 報表 3：熱門卦象排行

**目的**：找出最受歡迎的卦象

1. 探索 → 自由格式
2. 維度：
   - `Page path`（頁面路徑）
   - 篩選：只顯示 `/11` 到 `/66` 的路徑
3. 指標：
   - `Views`（瀏覽量）
   - `Users`（使用者數）
4. 排序：依 Views 降序
5. 限制：顯示前 10 名

---

## 資料隱私說明

追蹤的資料都是**匿名的使用行為**，不包含個人身份資訊：
- ✅ 追蹤：按鈕點擊、頁面瀏覽、分享行為
- ❌ 不追蹤：個人資料、IP 位址、姓名、Email

所有數據用於改善網站體驗，了解使用者需求。

---

## 進階功能（可選）

### 設定轉換目標

如果想追蹤「有多少訪客實際完成占卜」：

1. GA4 → 管理 → 事件
2. 建立新事件（基於現有事件）
3. 設定條件：`event_name` = `dice_roll` 或 `manual_selection`
4. 標記為轉換

### 設定客群（Audience）

建立特定使用者群組：
- 「活躍占卜者」：完成 3 次以上占卜
- 「分享者」：點擊過分享按鈕
- 「手動選擇愛好者」：只用手動方式

### 串連 Search Console

在 GA4 中串連 Google Search Console，可以看到：
- 哪些搜尋關鍵字帶來流量
- 搜尋來的訪客是否使用占卜功能
- SEO 表現與使用者行為的關聯

---

## 疑難排解

### 問題 1：看不到事件數據
- **可能原因**：需要等待幾小時
- **解決方式**：先查看「即時報表」測試

### 問題 2：事件數量異常低
- **可能原因**：追蹤代碼尚未生效
- **解決方式**：檢查網頁原始碼是否包含 `G-XNT97Q1GGJ`

### 問題 3：某些事件沒有出現
- **可能原因**：使用者沒有觸發該動作
- **解決方式**：自己測試點擊所有按鈕

---

## 資源連結

- **Google Analytics 4 文件**：https://support.google.com/analytics/
- **事件追蹤最佳實踐**：https://developers.google.com/analytics/devguides/collection/ga4/events
- **GA4 YouTube 教學**：搜尋「Google Analytics 4 教學」

祝您能從數據中獲得有價值的洞察！📊
