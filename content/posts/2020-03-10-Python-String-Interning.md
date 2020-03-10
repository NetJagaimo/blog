---
title: "Python String Interning機制"
date: 2020-03-10T10:51:05+08:00
draft: false
categories: ["python"]
tags: ["python"]
toc: true
---

某天在玩弄python的時候(迷:住手!放開那個python!!)發現了一個有趣的現象:  
```python
>>> a = "helloworld"
>>> b = "helloworld"
>>> id(a)
2917193150576
>>> id(b)
2917193150576

>>> a = "hello world"
>>> b = "hello world"
>>> id(a)
2917193150576
>>> id(b)
2917193150640
```
第一個例子，兩個變數指向同一個字串，然後記憶體位置一樣。  
但是，當我們加入了空格，兩個變數都指向"hello world"時，記憶體位置卻不一樣了。  
咦?? 為什麼會這樣? 
<!--more-->  

## Python字串駐留說明
這是因為python的string interning(字串駐留)機制運作方式的關係。所謂的string interning就是當一個string被命名為某個變數時，python會決定要不要使用之前用過的string，以節省記憶體空間，最佳化程式的運行。

決定的規則如下:
* 所有長度為0或是1的string都會被interned(駐留)
* string interning只會發生在compile time的時候。`"wtf"`會被保留，但是`"".join(["w", "t", "f"])`不會，因為join()是發生在run time時。
* string由ASCII字母、數字、底線以外的東西組成的不會被interned，所以`"hello world"`才沒有被interned，因為裡面含有空格

但是再看一個例子:
```python
>>> a, b = "hello world", "hello world"
>>> id(a)
2917193150576
>>> id(b)
2917193150576
```
恩，沒錯，它們又一樣了...
這是因為它們在同一時間進行編譯，所以python會認得這裡有出現過一樣的物件，而讓兩個變數指向同一物件。

所以說，以上情況只會發生在使用互動式模式寫python的時候，如果是用`.py`檔案進行編譯就不會有這個現象，因為互動式模式每一行都會從新編譯一次，而`.py`檔案會全部進行編譯之後再運行，設計上會記得之前出現過的字串，進而優化儲存空間的使用。

看到這可能會產生個疑問，python不是直譯式語言嗎?怎麼扯到編譯去了?如果想了解更多，可以看這篇[Python編譯與直譯探討](https://netjagaimo.github.io/2020-03-10-python-interpreter-vs-compile/)

## 手動將字串駐留起來
使用sys模組裡面的intern()方法可以手動將字串駐留起來
```python
>>> import sys
>>> a = sys.intern("hello world")
>>> b = sys.intern("hello world")
>>> id(a)
2699044712176
>>> id(b)
2699044712176
```
記憶體位置一樣了，世界和平了(X

## 整數駐留
其實整數也會駐留，駐留的範圍是-5~256
```python
>>> a = 256
>>> b = 256
>>> id(a)
1423430688
>>> id(b)
1423430688
```
但是使用257時就會不同了
```python
>>> a = 257
>>> b = 257
>>> id(a)
2699041996592
>>> id(b)
2699043325584
```
這是因為python認為-5~256屬於常用數字，所以將他的記憶體空間固定起來，要用時指向同一個就行，就不需要再重複開啟記憶體空間>指派>刪除空間的動作，節省時間

{{% notice note %}}
參考資料:  
[Do you really think you know strings in Python?](https://www.codementor.io/satwikkansal/do-you-really-think-you-know-strings-in-python-fnxh8mtha)  
[python中的字符串intern机制](http://ohmycat.me/python/2015/03/03/python-string-intern.html)  
[Python中的字符串驻留](https://blog.51cto.com/cnn237111/1615356)  
{{% /notice %}}