---
title: 使用 Sequelize 建立資料庫
tags: [後端]
layout: single
date: 2020-03-04

---

# 使用 Sequelize 建立資料庫
###### tags: `後端`
## 建立 ER Model
ER Model (Entity–relationship model)是設計資料庫的重要方法，簡單來說可使用 ER Model 設計資料的骨架。

**以 MP Park 專案為例(簡易表示DB存放骨架)：**

![](https://i.imgur.com/zVAJvZ0.png)


**下圖為各資料存放細項**：

![](https://i.imgur.com/bupSfUN.png)

## 建立資料庫指令
**以 MP Park 專案為例建立 store 資料：**
```
yarn sequelize model:create --name store --underscored --attribute 'name:string,business_name:string,business_id:integer,conact:string,address:text'
```
