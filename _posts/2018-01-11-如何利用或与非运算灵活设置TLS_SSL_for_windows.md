---
layout:     post
title:      如何利用或与非运算灵活设置TLS/SSL-for windows
subtitle:   TLS/SSL
date:       2018-01-11
author:     kun
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - C++
    - Windows
---


## 1
***
在Windows平台下做安全辅助工具时经常会对IE高级选项中的TLS/SSL进行设置，在银行各种安全软件开发中尤为常见。

> _[TLS/SSL 传输层安全性协议 维基百科](https://zh.wikipedia.org/wiki/%E5%82%B3%E8%BC%B8%E5%B1%A4%E5%AE%89%E5%85%A8%E6%80%A7%E5%8D%94%E5%AE%9A)_

## 2
***
此项设置共包含
`TLS 1.0``TLS 1.1``TLS 1.2`
`SSL 2.0``SSL 3.0`

微软将这五项设置全部融合在windows注册表中`HKEY_CURRENT_USER`，`Software\Microsoft\Windows\CurrentVersion\Internet Settings`，`SecureProtocols`项里。
> _[官方参考文档](https://support.microsoft.com/en-us/help/3140245/update-to-enable-tls-1-1-and-tls-1-2-as-a-default-secure-protocols-in)_

例如，假设勾选TLS 1.0，TLS 1.1，TLS 1.2，附图表说明：

|  Item   | Hex | Dec | Oct |     Bin      |
|:-------:|----:|----:|----:|-------------:|
|× SSL 2.0|    8|    8|   10|          1000|
|× SSL 3.0|   20|   32|   40|     0010 0000|
|√ TLS 1.0|   80|  128|  200|     1000 0000|
|√ TLS 1.1|  200|  512| 1000|0010 0000 0000|
|√ TLS 1.2|  800| 2048| 4000|1000 0000 0000|

最后结果为：
* Hex: *0x80 + 0x200 + 0x800 = 0xa80(16)*
* Dec: *128 + 521 + 2048 = 2688(10)*
* Oct: *200 + 1000 + 4000 = 8200(8)*
* Bin: *1000 0000 0000 + 0010 0000 0000 + 1000 0000 = 1010 1000 0000*

## 3
***
(continue...)