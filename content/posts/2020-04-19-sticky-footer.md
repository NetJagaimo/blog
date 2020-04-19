---
title: "CSS固定頁尾 - 使用flexbox的解法"
date: 2020-04-19T16:31:54+08:00
categories: ["css"]
tags: ["css", "sticky-footer"]
toc: true
---

在寫網頁的時後有一個常常會碰到的問題，那就是當網頁內容少於網瀏覽器高度的時候，footer就不會固定在下方，而是隨著內容一起浮上來，像這張圖一樣
![](/images/2020-04-19-sticky-footer/footer-bug-demo.PNG)
解決的方法有很多種，但大多都有些複雜，而這篇文章分享的是一個利用flexbox的解法，很單純且彈性很高，一起看下去吧!

<!--more-->

## HTML
以下範例以這個HTML為例
```html
<header>
  <h1>我是標題</h1>
</header>
<main>
  <p>...這裡放文字...</p>
</main>
<footer>
  <p>我是footer</p>
</footer>
```

## 了解問題
先來了解一下造成這個bug的問題，我們看這張圖，這是內容很多的情況，footer的位置很正常
![](/images/2020-04-19-sticky-footer/footer-demo.PNG)
然而導致footer跟著內容浮上去的問題就是，內容不夠多，沒辦法把footer擠到最下面。  
因此我們的解決方法就是要讓footer上方的元素設定一個最小高度，而這個高度要剛剛好可以讓footer擠到他該去的位置

## 利用calc的解法
最直觀的解法就是將header以及main用一個wrapper包起來，然後計算好footer高度之後，利用calc將wrapper的高度設為100vh - footer高度，像這樣子
```html
<div id="wrapper">
    <header>
        <h1>我是標題</h1>
    </header>
    <main>
        <p>...這裡放文字...</p>
    </main>
</div>
<footer>
  <p>我是footer</p>
</footer>
```
```css
/* 重點範圍，其他省略 */
#wrapper {
    height: calc(100vh - 50px);
}

footer {
    height: 50px;
}
```
十分直觀的想法，但是這樣有個問題，如果你footer內的文字換行了，或是想要在footer內新增些東西而導致footer高度改變，那就要重新計算一次高度，然後改程式碼，挺麻煩的。

## 利用flexbox的解法
這邊分享的解法，可以解決上面的難題，既不需要做計算，而且還會自己調整，十分有彈性，先看看demo吧!
{{< codepen id="WNQxgeR" >}}  

這時候可以先把wrapper拿掉了，我們用不到它  
接著加入下面這段css就可以了! 不管footer高度怎麼變化，都一樣會乖乖地固定在下方不會亂跑。  
```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex-grow: 1;
}
```

### 原理
首先看看body的部分，`flex-direction: column`將預設的row排列變為column，否則裡面的元素都會變成橫向排列。接著`min-height`將body的高度稱開到瀏覽器的窗口大小。  
然後看main，這邊的`flex-grow: 1`利用了flex的特性，flex-grow在計算時，會先扣掉具有固定高度的元素，接著再將剩餘元素依照grow給定的比例分配。  
因此我們可以利用這個特性，將main的高度分配為扣掉header以及footer高度後的全部(這邊設定1, 2, 3...皆可，大於零就好)，這樣就可以完成我們要的效果了!

## 參考
{{% notice note %}}
參考資料:  
Lea Verou(2016)。*CSS Secrets中文版：解決網頁設計問題的有效秘訣*。臺北市：碁峰資訊。 
{{% /notice %}}
