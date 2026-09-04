# MindAR 真實 AR 頁面 — 使用說明

## 文件清單

```
MindAR_真實版/
├── index.html       # AR 主頁面
├── ar-content.png   # AR 內容圖片（麝香貓）
└── targets.mind     # ⚠️ 圖像追蹤目標文件（MindAR 編譯器下載的預設文件名）
```

## 第一步：生成 targets.mind 目標文件

MindAR 需要一個編譯後的目標文件才能識別圖像。請按以下步驟生成：

1. **準備識別圖**：使用你的 Timor Leste Kopi Luwak 咖啡包裝圖（建議尺寸 800×800 以上，JPG/PNG 格式）

2. **打開 MindAR 線上編譯器**：
   ```
   https://hiukim.github.io/mind-ar-js-doc/tools/compile/
   ```

3. **上傳識別圖**：點擊「Upload」選擇你的咖啡包裝圖

4. **下載目標文件**：編譯完成後點擊「Download」，會得到一個 `.mind` 文件

5. **放入資料夾**：MindAR 編譯器下載的文件預設名為 `targets.mind`，直接放入 `MindAR_真實版/` 資料夾中，與 `index.html` 同級即可（不需要重命名）

## 第二步：運行 AR 頁面

### 方式一：本地伺服器（推薦）

AR 功能需要訪問相機，瀏覽器只允許在 **HTTPS** 或 **localhost** 環境下訪問相機。直接用 `file://` 打開可能無法使用相機。

**使用 Python 啟動本地伺服器：**
```bash
cd MindAR_真實版
python3 -m http.server 8080
```

然後在瀏覽器打開：
```
http://localhost:8080
```

**使用 Node.js 啟動：**
```bash
npx serve MindAR_真實版 -p 8080
```

### 方式二：部署到 HTTPS 伺服器

將整個資料夾上傳到任何支援 HTTPS 的靜態網站託管服務：
- GitHub Pages
- Netlify
- Vercel
- Cloudflare Pages

然後用手機瀏覽器打開網址，允許相機權限即可。

## 座標參數說明

頁面中已應用從 Kivicube 轉換後的座標：

| 對象 | Position | Scale | 說明 |
|---|---|---|---|
| 對象1 | `-0.297 0.5 0.649` | `0.5 0.5 0.5` | Kivicube 真實座標 |
| 對象2 | `0.3 0.35 -0.2` | `0.6 0.6 0.6` | 第二個位置 |

**Rotation 說明**：Kivicube 中對象1的 rotation.x=-90° 是將圖片從平放轉為垂直。MindAR 的 `<a-image>` 預設即為垂直面向觀察者，故不需再設置 rotation。

## 常見問題

**Q: 頁面打開後顯示「需要相機權限」？**
A: 請確保在 localhost 或 HTTPS 環境下打開，並在瀏覽器提示中允許相機訪問。

**Q: 相機畫面出現了但識別不到圖？**
A: 請確認 `targets.mind` 文件已正確放入資料夾，且識別圖與生成 targets.mind 時使用的圖片一致。

**Q: 圖片顯示為白色方塊？**
A: 請確認 `ar-content.png` 已放入資料夾，且文件名大小寫正確。

**Q: 可以在手機上使用嗎？**
A: 可以，推薦使用手機版 Chrome 或 Safari，透過 HTTPS 鏈接訪問。

## 技術資訊

- MindAR 版本：1.2.5
- A-Frame 版本：1.4.1
- 圖像追蹤：自然特徵追蹤（Natural Feature Tracking）
- 支援平台：桌面 Chrome/Safari、手機 Chrome/Safari
