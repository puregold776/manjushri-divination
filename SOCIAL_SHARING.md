# 社交媒体分享功能说明

## 功能概述

当用户分享文殊占卜的卦象链接到 Facebook、Line 或其他社交媒体时，会自动显示该卦的卦象图片和相关信息。

## 工作原理

### 1. URL 格式

支持两种 URL 格式：

**路径格式**（推荐）：
- `https://yourdomain.com/11` （第1卦：佛父ཨ，佛母ཨ）
- `https://yourdomain.com/45` （第24卦：佛父ཙ，佛母ན）

**查询参数格式**（向后兼容）：
- `https://yourdomain.com/?y=0&w=0` （y=佛父索引0-5，w=佛母索引0-5）

### 2. 动态 Meta 标签更新

系统会在以下两个时机更新 Open Graph 标签：

#### 页面加载时（head 中的 script）
- 解析 URL 参数
- 如果有有效的卦象参数，立即更新 meta 标签
- 确保社交媒体爬虫能抓取到正确的图片

#### 显示卦象结果时（updateMetaTags 函数）
- 更新页面标题：`{卦象名} - {运势} | 文殊占卜`
- 更新 og:title、og:description、og:image
- 更新 twitter:title、twitter:description、twitter:image
- 使用绝对 URL 路径确保兼容性

### 3. 更新的 Meta 标签

- `og:title` - 卦象名称和运势
- `og:description` - 卦象偈语
- `og:image` - 对应的卦象图片（800x800 JPG）
- `og:url` - 当前页面 URL
- `twitter:title` - 同 og:title
- `twitter:description` - 同 og:description
- `twitter:image` - 同 og:image

## 测试方法

### 1. 本地测试
访问以下 URL 并查看页面源代码中的 meta 标签：
- http://localhost:8000/index.html?y=0&w=0
- http://localhost:8000/11

### 2. Facebook 分享调试
部署后使用 Facebook 分享调试工具：
https://developers.facebook.com/tools/debug/

输入卦象页面 URL，查看抓取的图片和信息。

### 3. Line 分享测试
直接在 Line 中分享链接，查看预览效果。

## 图片要求

- **格式**：JPG
- **尺寸**：800x800 像素
- **路径**：`manjusigns/sign{佛父}{佛母}.jpg`
- **示例**：`manjusigns/sign11.jpg`（第1卦）

## 注意事项

1. **绝对 URL**：图片使用绝对 URL 路径，确保社交媒体爬虫能正确访问
2. **缓存问题**：Facebook 等平台会缓存分享内容，更新后需要使用调试工具刷新
3. **HTTPS**：生产环境建议使用 HTTPS，确保图片能在所有平台正常显示
4. **文件大小**：JPG 压缩质量 80%，单个文件约 76KB-204KB

## 相关代码位置

- **Head 中的动态更新**：第 29-80 行
- **updateMetaTags 函数**：第 2186-2237 行
- **调用位置**：第 2307 行（loadFromURL 函数中）

