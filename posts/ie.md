---
layout: post
title: IE対応
excerpt: 案件で背景画像を固定するデザインのコーディングをしていたのですが、ちょいハマったのでメモがてら。
tags: cd
---

見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し

-----

# 概要
- 皆んな大好きIEで起きるバグの対応についてまとめます。  

## IE
- 即ち
- ではなく、マイクロソフトが開発したWebブラウザです。
- バージョンによってはサポートが切れています。~~今後、全てのサポートが切れる事を切に祈っています。~~  
- 後継版としてEdgeがでましたが、ここではEdgeについては触れません。

## 対応  
過去に対応した内容を列挙しようと思います。
- positionやらbackground-attachmentやらにfixedを使用すると、スクロール時に背景画像がガタツク。下記jsで直ります。
```
<script>
 if(navigator.userAgent.match(/MSIE 10/i) || navigator.userAgent.match(/Trident\/7\./) || navigator.userAgent.match(/Edge\/12\./)) {
 $('body').on("mousewheel", function () {
 event.preventDefault();
 var wd = event.wheelDelta;
 var csp = window.pageYOffset;
 window.scrollTo(0, csp - wd);
 });
 }
</script>
```

思い出したら追記していきます。