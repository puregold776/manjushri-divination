# Google 搜尋優化設定指南

## 步驟 1: 提交網站到 Google Search Console

1. 前往 [Google Search Console](https://search.google.com/search-console/)
2. 登入您的 Google 帳號
3. 點擊「新增資源」
4. 選擇「網域」或「網址前置字元」
   - 網域：輸入 `manjumo.com`（需要 DNS 驗證）
   - 網址前置字元：輸入 `https://manjumo.com`（較簡單）
5. 驗證網站擁有權（會提供 HTML 檔案或 meta 標籤）
6. 驗證成功後，提交 Sitemap：`https://manjumo.com/sitemap.xml`

## 步驟 2: 建立 robots.txt 和 sitemap.xml

這些檔案已經在專案中建立，會自動部署。

## 步驟 3: 等待 Google 索引

- 通常需要 1-4 週
- 可在 Search Console 中查看索引狀態
- 可使用「要求建立索引」功能加速

## 步驟 4: 優化 SEO

網站已包含：
- ✅ 適當的 meta 標籤（title, description）
- ✅ Open Graph 標籤（社群媒體分享）
- ✅ 響應式設計（手機友善）
- ✅ 清晰的 URL 結構（/11, /12 等）
- ✅ 語意化的 HTML 結構

## 驗證方式選擇建議

最簡單的驗證方式是「HTML 標記」：
1. Google 會給您一個 meta 標籤
2. 將標籤加入 index.html 的 <head> 中
3. 部署後點擊驗證

## 檢查索引狀態

在 Google 搜尋列輸入：
```
site:manjumo.com
```

如果出現結果，表示已被索引。
