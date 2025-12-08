# 2025 YYsuni Blog

> 最新引導說明：https://www.yysuni.com/blog/readme

該項目使用 Github App 管理項目內容，請保管好後續創建的 **Private key**，不要上傳到公開網上。

## 1. 安裝

使用該項目可以先不做本地開發，直接部署然後配置環境變量。具體變量名請看下列大寫變量

```ts
export const GITHUB_CONFIG = {
	OWNER: process.env.NEXT_PUBLIC_GITHUB_OWNER || 'yysuni',
	REPO: process.env.NEXT_PUBLIC_GITHUB_REPO || '2025-blog-public',
	BRANCH: process.env.NEXT_PUBLIC_GITHUB_BRANCH || 'main',
	APP_ID: process.env.NEXT_PUBLIC_GITHUB_APP_ID || '-'
} as const
```

也可以自己手動先調整安裝，可自行 `pnpm i`

## 2. 部署

我這里熟悉 Vercel 部署，就以 Vercel 部署為例子。創建 Project => Import 這個項目

![](https://www.yysuni.com/blogs/readme/730266f17fab9717.png)

無需配置，直接點部署

![](https://www.yysuni.com/blogs/readme/95dee9a69154d0d0.png)

大約 60 秒會部署完成，有一個直接 vercel 功能變數名稱，如：https://2025-blog-public.vercel.app/

到這里部署網站已經完成了，下一步創建 Github App

## 3. 創建 Github App 鏈接倉庫

在 github 個人設定裡面，找到最下麵的 Developer Settings ，點擊進入

![](https://www.yysuni.com/blogs/readme/0abb3b592cbedad6.png)

進入開發者頁面，點擊 **New Github App**

*GitHub App name* 和 *Homepage URL* , 輸入什麼都不影響。Webhook 也關閉，不需要。

![](https://www.yysuni.com/blogs/readme/71dcd9cf8ec967c0.png)

只需要注意設定一個倉庫 write 權限，其它不用。

![](https://www.yysuni.com/blogs/readme/2be290016e56cd34.png)

點擊創建，誰能安裝這個倉庫這個選擇無所謂。直接創建。

![](https://www.yysuni.com/blogs/readme/aa002e6805ab2d65.png)


### 創建密鑰

創建好 Github App 後會提示必須創建一個 **Private Key**，直接創建，會自動下載（不見了也不要緊，後面自己再創建再下載就行）。頁面上有個 **App ID** 需要復制一下

再切換到安裝頁面

![](https://www.yysuni.com/blogs/readme/c122b1585bb7a46a.png)

這里一定要只**授權當前項目**。

![](https://www.yysuni.com/blogs/readme/2cf1cee3b04326f1.png)

點擊安裝，就完成了 Github App 管理該倉庫的權限設定了。下一步就是讓前端知道推送那個項目，就是最開始提到的環境變量。（如果你不會設定環境變量，直接改倉庫文件 `src/consts.ts` 也行。因為是公開的，所以環境變量意義也不大）

直接輸入這幾個環境變量值就行，一般只用設定 OWNER 和 APP_ID。其它配置不用管，直接輸入創建就行。

![](https://www.yysuni.com/blogs/readme/c5a049d737848abf.png)

設定完成後，需要手動再部署一次，讓環境變量生效。
* 可以直接 push 一次倉庫代碼會觸發部署
* 也可以手動選擇創建一次部署
![](https://www.yysuni.com/blogs/readme/59a802ed8d1c3a13.png)

## 4. 完成

現在，部署的這個網站就可以開始使用前端改內容了。比如更改一個分享內容。

**提示**，網站前端頁面刪改完提示成功之後，你需要等待後台的部署完成，再刷新頁面才能完成服務器內容的更新哦。

## 5. 刪除

使用這個項目應該第一件事需要刪除我的 blog，單獨刪除，批量刪除已完成。

## 6. 配置

大部分頁面右上角都會有一個編輯按鈕，意味著你可以使用 **private key** 進行配置部署。

### 6.1 網站配置

首頁有一個不顯眼的配置按鈕，點擊就能看到現在可以配置的內容。

![](https://www.yysuni.com/blogs/readme/cddb4710e08a5069.png)

## 7. 寫 blog

寫 blog 的圖片管理，可能會有疑惑。圖片管理推薦邏輯是先點擊 **+ 號** 添加圖片，（推薦先壓縮好，尺寸推薦寬度不超過 1200）。然後將上傳好的圖片直接拖入文案編輯區，這就已經添加好了，點擊右上角預覽就可以看到效果。

## 8. 寫給非前端

非前端配置內容，還是需要一個文件指引。下麵寫一些更細致的代碼配置。

### 8.1 移除 Liquid Grass

進入 `src/layout/index.tsx` 文件，刪除兩行代碼，然後提交代碼到你的 github
```tsx
const LiquidGrass = dynamic(() => import('@/components/liquid-grass'), { ssr: false })
// 中間省略...
<LiquidGrass /> // 第 53 行
```

![](https://www.yysuni.com/blogs/readme/f70ff3fe3a77f193.png)

### 8.2 配置首頁內容

首頁的內容現在只能前端配置一部分，所以代碼更改在 `src/app/(home)` 目錄，這個目錄代表首頁所有文件。首頁的具體文件為  `src/app/(home)/page.tsx`

 ![](https://www.yysuni.com/blogs/readme/011679cd9bf73602.png)

這里可以看到有很多 `Card` 文件，需要改那個首頁 Card 內容就可以點入那個具體文件修改。

比如中間的內容，為 `HiCard`，點擊 `hi-card.tsx` 文件，即可更改其內容。

![](https://www.yysuni.com/blogs/readme/20b0791d012163ee.png)

## 9. 互助群

對於完全不是**程式員**的用戶，確實會對於更新代碼後，如何同步，如何**合並代碼**手足無措。我創建了一個 **QQ群**（加群會簡單點），或者 vx 群還是 tg 群會好一點可以 issue 裡面說下就行。

QQ 群：[https://qm.qq.com/q/spdpenr4k2](https://qm.qq.com/q/spdpenr4k2)
> 不好意思，之前的那個qq群ID（1021438316），不知道為啥搜不到😂

微信群：剛建好了一個微信群，沒有 qq 的可以用這個微信群
![](https://www.yysuni.com/blogs/readme/343f2c62035b8e23.webp)


應該主要是我自己親自幫助你們遇到問題怎麼辦。（後續看看有沒有好心人）

希望多多的非程式員加入 blogger 行列，web blog 還是很好玩的，屬於自己的 blog 世界。

游戲資產不一定屬於你的，你只有**使用權**，但這個 blog **網站、內容、倉庫一定是屬於你的**

#### 特殊的導航 Card

因為這個 Card 是全局都在的，所以放在了 `src/components` 目錄

![](https://www.yysuni.com/blogs/readme/9780c38f886322fd.png)

## Star History

<a href="https://www.star-history.com/#YYsuni/2025-blog-public&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=YYsuni/2025-blog-public&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=YYsuni/2025-blog-public&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=YYsuni/2025-blog-public&type=date&legend=top-left" />
 </picture>
</a>
