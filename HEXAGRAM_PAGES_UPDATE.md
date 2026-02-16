# 卦象頁面更新說明

## 問題
Google Search Console 報告：「頁面會重新導向，導致你的網頁無法編入索引。」

原因：所有 36 個卦象頁面（11.html 到 66.html）都包含 JavaScript 重定向：
```javascript
window.location.replace('/index.html?y=0&w=0');
```

這導致：
- ❌ Google 爬蟲無法索引這些頁面
- ❌ 頁面內容無法被搜索引擎讀取
- ❌ 社交媒體分享時可能無法正確顯示

## 解決方案

使用新的 Python 腳本 `generate_static_hexagram_pages.py` 生成包含完整內容的靜態卦象頁面。

### 新頁面特點

✅ **完整的 SEO 優化**
- 包含完整的卦象內容
- 正確的 meta description
- 結構化數據（Schema.org）
- Canonical URL
- Open Graph 和 Twitter Card

✅ **用戶友好**
- 美觀的視覺設計（與主頁一致）
- 顯示卦象圖片
- 完整的卦辭、解讀和修持建議
- 返回首頁的按鈕

✅ **SEO 可索引**
- 無重定向
- 真實內容可被爬蟲讀取
- 每個頁面都是獨立的完整 HTML

## 使用方法

### 重新生成所有卦象頁面

```bash
cd manjushri-divination
python3 generate_static_hexagram_pages.py
```

輸出：
```
Found 36 hexagrams
✓ Generated 11.html: 無垢晴空 - 中平
✓ Generated 12.html: 璀璨杲日 - 中平
...
✓ Generated 66.html: 勝幢高懸 - 上上吉

✓ Successfully generated 36/36 static hexagram pages
```

## 部署後的步驟

1. **上傳更新的文件到伺服器**
   - 所有 11.html 到 66.html 文件
   - 確保 manjusigns/ 目錄下的圖片存在

2. **在 Google Search Console 中請求重新索引**
   - 前往 Google Search Console
   - 使用「網址檢查」工具
   - 輸入幾個卦象頁面 URL（例如：https://manjumo.com/11）
   - 點擊「要求建立索引」

3. **提交更新的 sitemap**
   ```
   https://manjumo.com/sitemap.xml
   ```

4. **驗證頁面可被索引**
   - 使用「檢視為 Google」功能
   - 確認沒有重定向錯誤
   - 確認可以看到完整內容

## 預期結果

- Google 可以成功索引所有 36 個卦象頁面
- 搜索結果中會顯示卦象的名稱和卦辭
- 用戶可以直接從搜索結果訪問特定卦象
- 社交媒體分享時會顯示正確的卦象圖片和描述

## 技術細節

### 頁面結構
- 響應式設計（移動設備友好）
- 與主頁一致的視覺風格
- 包含 Google Analytics
- 完整的無障礙支持

### SEO 優化
- 語義化 HTML
- 結構化數據標記
- 適當的標題層級
- 描述性的 alt 文字

---

**更新日期：** 2026-02-16
**腳本：** generate_static_hexagram_pages.py
**影響頁面：** 36 個卦象頁面（11.html - 66.html）
