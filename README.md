# 香港天氣資訊 (Hong Kong Weather Information)

一個展示香港天文台實時天氣數據的前端應用程式，使用 Cloudflare Workers 部署。

## 功能特色

- 🌤️ **當前天氣概況** - 顯示天氣狀況、濕度等基本信息
- 🌡️ **各區氣溫** - 展示香港各區的實時氣溫數據
- 🌧️ **各區雨量** - 顯示過去一小時各區的降雨量
- ⚠️ **警告信息** - 實時顯示天氣警告
- 🌀 **熱帶氣旋資訊** - 熱帶氣旋相關信息
- 🔄 **自動更新** - 每 10 分鐘自動刷新數據
- 📱 **響應式設計** - 適配桌面和移動設備

## 技術棧

- **前端**: HTML5, JavaScript (Vanilla)
- **樣式**: Tailwind CSS (CDN)
- **部署**: Cloudflare Workers
- **後端 API**: `https://hkweather-backend.yung0000.workers.dev/weather`

## 項目結構

```
weather-frontend/
├── index.html          # 主頁面文件
├── wrangler.toml       # Cloudflare Workers 配置文件
├── workers-site/
│   └── index.js        # Workers 處理腳本
└── README.md           # 項目說明文檔
```

## 本地開發

### 前置要求

- Node.js
- Wrangler CLI (Cloudflare Workers 命令行工具)

### 安裝 Wrangler

```bash
npm install -g wrangler
```

### 登錄 Cloudflare

```bash
wrangler login
```

### 本地運行

```bash
wrangler dev
```

應用將在本地運行，通常為 `http://localhost:8787`

## 部署

### 部署到 Cloudflare Workers

```bash
wrangler deploy
```

部署完成後，你的應用將可以在 Cloudflare Workers 提供的 URL 上訪問。

## 配置說明

### wrangler.toml

```toml
name = "hkweather-frontend"
compatibility_date = "2025-10-05"

[assets]
bucket = "./"
document = "index.html"
```

- `name`: Workers 項目名稱
- `compatibility_date`: Cloudflare Workers 兼容性日期
- `assets.bucket`: 靜態資源目錄
- `assets.document`: 主文檔文件

## API 說明

應用從以下後端 API 獲取天氣數據：

```
GET https://hkweather-backend.yung0000.workers.dev/weather
```

### 響應數據格式

```json
{
  "icon": "天氣狀況描述",
  "humidity": [
    {
      "value": 75,
      "unit": "%"
    }
  ],
  "updateTime": "2025-01-01T12:00:00Z",
  "warningMessage": ["警告信息1", "警告信息2"],
  "tcMessage": ["熱帶氣旋信息"],
  "temperature": [
    {
      "place": "地區名稱",
      "value": 25,
      "unit": "°C"
    }
  ],
  "rainfall": [
    {
      "place": "地區名稱",
      "max": 5,
      "unit": "mm"
    }
  ],
  "rainfallTime": {
    "startTime": "2025-01-01T11:00:00Z",
    "endTime": "2025-01-01T12:00:00Z"
  }
}
```

## 功能說明

### 自動刷新

應用會自動每 10 分鐘（600,000 毫秒）刷新一次天氣數據。

### 手動刷新

點擊頁面底部的「🔄 重新載入」按鈕可手動刷新數據。

### 溫度顏色編碼

- 🔴 紅色: ≥ 30°C
- 🟠 橙色: 25-29°C
- 🟡 黃色: 20-24°C
- 🟢 綠色: 15-19°C
- 🔵 藍色: < 15°C

### 雨量顏色編碼

- 🔵 深藍: ≥ 10mm
- 🔵 中藍: 5-9mm
- 🔵 淺藍: 1-4mm
- ⚪ 灰色: < 1mm

## 瀏覽器支持

- Chrome (最新版本)
- Firefox (最新版本)
- Safari (最新版本)
- Edge (最新版本)

## 許可證

此項目僅供學習和個人使用。

## 相關鏈接

- [香港天文台](https://www.hko.gov.hk/)
- [Cloudflare Workers 文檔](https://developers.cloudflare.com/workers/)
- [Tailwind CSS 文檔](https://tailwindcss.com/docs)

## 更新日誌

### 當前版本

- 實時天氣數據顯示
- 各區氣溫和雨量展示
- 警告和熱帶氣旋信息
- 響應式設計
- 自動刷新功能

