---
title: Apache Rewrite with Htaccess
tags: [伺服器]
layout: single
date: 2020-03-04
toc: true
toc_sticky: true
---

啟用Rewrite需設定Apache，當讀取改寫過的.htaccess時須重啟Apache，因此...(略)直接使用線上測試.htaccess即可。
- [Htaccess Tester](https://htaccess.madewithlove.be/)

## RewriteRule
`RewriteRule [match_uri] [rewrite_uri] [flags]`

- match_uri: 需改寫的uri。(使用正規式表達)
- rewrite_uri: 改寫後的uri。(使用正規式表達)
- flags: 設定Rule的行為。(可用逗號代表多個，中間不能有空格)

##### 常見flags
```
[L]：Last，成功執行這個 Rule 後就會停止，不繼續往下執行。
[NC]：Non Case-sensitive，代表 match_uri 不比對大小寫差異。
[QSA]：Query String Append，代表保留網址尾端帶的 GET 參數，沒使用 flag 的預設是會把參數去掉的。
[QSD]：Query String Discard，與 QSA 相反的作用，apache v2.4 才有。
[R]: Redirect，代表用轉址的方式轉到新的網址，預設是 302 Status Code，如：[R=301]，也可以回傳 400、200、404 等的 Status Code，通常會跟 [L] 一起代表結束，也是除錯常用的 Flag
[DPI]: 不要再接續的 Rule 中結尾中加上 PathInfo，會在「五、一些小特性」的段落說明。
[F]: Forbdien 就是不給看啦！
```
###### 參考資料: [Apache Rewrite with Htaccess 理解與技巧](https://medium.com/@awonwon/htaccess-with-rewrite-3dba066aff11)
##### Example
輸入網址：
https://www.youbike.com.tw:10035/APP2.HTML%0D%0AA18C847475320100007A0000000000

轉至後為:
https://www.youbike.com.tw:10035/app2.html

``` php
>> .htaccess

RewriteEngine on //開啟Rewrite功能

RewriteRule ^.*APP2\.HTML[\S\s]*$ /app2.html //改寫規則

```