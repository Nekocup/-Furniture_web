# 家具網站 ( landing page )
參考 templatemonster 裡的模板練習網頁的切版，純手刻css，沒有使用css框架
## 使用的技術
* vue
* swiper
## 採雷 ...
* 在 Safari 裡面 overflow-x:hidden 無效
  * 需要搭配 `html, body { position:relative; }` 才行
* 部分瀏覽器不支援 DOM 的 scrollTop
需要使用
`      let scrollTop =
        document.documentElement.scrollTop ||
        window.pageYOffset ||
        document.body.scrollTop; `
