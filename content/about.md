---
title: "關於我"
date: 2020-03-06T00:24:09+08:00
draft: false
---

目前就讀於師大圖資所的一枚研究生，綽號土豆，NetJagaimo的Jagaimo是日文的馬鈴薯

最喜歡的一句話，出自於Zen of Python:
> Now is better than never.
>
> Although never is often better than *right* now.

## 技能

#### 網頁設計
* HTML、CSS: 理解基本語法，能夠看著資料或是範例改出自己的東西，了解RWD與HTML5一些與之前不同的標籤
    > freeCodeCamp Responsive Web Design Certification (300 hours) 完課認證: https://www.freecodecamp.org/certification/samyang/responsive-web-design

* jQuery: 能夠手刻出一個模擬Terminal的動畫
    > 可參考("我們學什麼"區塊): https://sirla-fjulis.github.io/

* Bootstrap: 理解Bootstrap的基本用法

#### 程式設計
* Python: 使用PyGame寫出一個拳擊遊戲、自動玩Chrome小恐龍遊戲的Game bot，還有自動篩選Email的小腳本。目前正在學習Flask。
    > PyBoxing: https://github.com/Bluebell3310/PyBoxing
    > Chrome Dinosaur Game Bot: https://github.com/Bluebell3310/Chrome-Dinosaur-Game-Bot
    > Email篩選腳本: https://github.com/Bluebell3310/Python-Scripts/blob/master/catchEmail.py
    > Flask實作練習: https://github.com/Bluebell3310/Flask-learning-practice
    > 與同學一同撰寫的Flask學習筆記: https://hackmd.io/c/SyR6D_sDV/%2Fs%2FSJi6nIfBV

* Git: 了解基本用法，能用Github與他人協作，可以參考這份筆記
    > https://hackmd.io/EKfZJbc4SUmCHkT0LEm85Q

* JavaScript: 了解基礎語法

* C++、Java: Basic

#### 繪圖軟體
* Inkscape、Illustrator、Photoshop: 能畫一些簡單的向量圖與效果

* 幫SIRLA讀書會設計的LOGO
![](https://i.imgur.com/alIpYBU.png =200x)

* 萬聖節版本
![](https://i.imgur.com/N1TlFPA.png =200x)

### Linux
安裝、基本操作沒問題，之前在碩睿資訊實習時用過Linux來架設KOHA(一套Open Source的Web-based圖書館管理系統)
    
#### 資料結構&演算法
具備基礎知識，可以參考這個Repository，裡面是我在看Problem Solving with Algorithms and Data Structures using Python這本書時做的練習。
> Repository: https://github.com/Bluebell3310/Algorithm-and-Data-Structure-With-Python 

## 作品
### SIRLA官方網站
:::info
Github Repository: https://github.com/SIRLA-FJULIS/sirla-fjulis.github.io
網站連結: https://sirla-fjulis.github.io/
使用工具: HTML, CSS, Bootstrap, jQuery
:::
![](https://i.imgur.com/2FXU2ZP.png)
這是我幫我們的讀書會設計並製作的官方網站，第一次製作網頁，做的過程中學習到很多，例如怎麼用JQuery手刻動畫、怎麼做出背景固定效果、怎麼樣在社群軟體中分享連結時會出現簡介與縮圖，還有怎麼解決有些瀏覽器上會出現的bug。

印象最深刻的是一個奇怪的小錯誤，一開始在製作的時候我使用background-color: rgb(r, g, b, a); 的方式讓背景變透明。這個方式在我的電腦上看是正常的，在很多人的電腦上看也是正常的。但是當同學拿起他的舊手機進行測試時卻發現沒有正常的出現透明色。經過很多嘗試後才發現原來要使用rgba()。這問題感覺上很小(或很蠢XD)，但卻讓我了解到前端需要考慮到不同裝置的使用情況，並且讓使用讓每個裝置都能獲得最佳體驗的解法。

### 桃李滿天下
:::info
使用工具: Unity, Illustrator
遊玩影片: https://drive.google.com/open?id=1RMrCDY486zW6T54mHwBnnjlw-fLvjoYz
:::
![](https://i.imgur.com/9V5RAcE.png)
參加中央創遊第四屆Game Jam時與隊友一同製作的遊戲。我擔任企劃、美術的角色，遊戲的主要架構是由我想出來的，而大部分美術圖也是我畫出來的。另外我還兼任了一部份程式設計的角色。場景中有兩種樹，桃樹及李樹，分別會掉出小桃子怪物跟小李子怪物，牠們會砍掉對方的樹。玩家的任務是透過水槍(澆水，讓樹長更快)以及酒瓶(砸死小怪物)維持生態平衡，並將樹種植到一定的數量以上即可獲勝。

### 音波戰機
:::info
Github Repository: https://github.com/Bluebell3310/Sound-Wave-Fighter
使用工具: Processing, Arduino, PureData, LoopMidi
遊玩影片: https://drive.google.com/open?id=1JcvoxcxiJ7lt773Np72NGcFIcgIMjJ9f
:::
![](https://i.imgur.com/tqDGVSw.jpg)
這是一個戰機射擊遊戲，特色在於玩家要透過發出聲音來進行發射子彈，隨著不同的聲音頻率會射出三種子彈，分別可消滅對應的三種敵人，而大吼一聲讓音量超過閾值則可觸發全螢幕消除的大招。

音波戰機是選修互動媒體概論時的期末專案，當初設計專案時腦袋只有一個構想，想要結合聲音以及遊戲，但是老師上課其實沒有教過怎麼實現聲控功能，因此我研究了很多種方式，最後使用了PureData以及LoopMidi作為解決方案。

做這個遊戲的過程讓我了解到，實現腦中的想法並不容易，但只要努力研究，還是有辦法讓想像成真。

### PyBoxing
:::info
Github Repository: https://github.com/Bluebell3310/PyBoxing
使用工具 Tools: Python, Pygame
遊玩影片: https://drive.google.com/open?id=1tJT2BhqGmxeN3ZWrxMZ0hl2iYQdkEXUC
:::
![](https://i.imgur.com/T8Fe8xo.png)
這是一個雙人的拳擊對戰遊戲，玩家可以使用三種攻擊方式直拳、上鉤拳以及衝刺攻擊，每種攻擊的特性如下:
* 直拳: 一般攻擊，造成中等傷害
* 上鉤拳: 造成少量傷害，但擊中對手可累積暈眩值，累積到50%對手會進入緩速狀態，到達100%則進入不可動作的暈眩狀態。
* 衝刺攻擊: 按住按鍵集氣，氣滿自動向前衝鋒，對路徑上的對手造成大量傷害

可以透過這幾種攻擊的組合進行比較有策略性的格鬥。
