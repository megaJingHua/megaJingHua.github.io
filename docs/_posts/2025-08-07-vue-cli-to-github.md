---
title: Vue Cli 自動部署至 GitHub
date: 2025-05-07
categories: [Vue, 技術筆記]
---

# Vue Cli 自動部署至 GitHub
###### tags: `Vue` `GitHub`
參考資料:[Vue Cli 部署](https://cli.vuejs.org/zh/guide/deployment.html#%E6%B7%B7%E5%90%88%E9%83%A8%E7%BD%B2)
## 在專案底下新增deploy.sh檔案
``` 
#!/usr/bin/env sh

# 發生錯誤時執行終止指令
set -e

# 打包編譯
npm run build

# 移動到打包資料夾下，若你有調整的話打包後的資料夾請務必調整
cd dist

# 部署到自定義網域
# echo 'www.example.com' > CNAME

git init
git add -A
git commit -m 'deploy'

# 部署到 https://<USERNAME>.github.io
# git push -f git@github.com:<USERNAME>/<USERNAME>.github.io.git master

# 部署到 https://<USERNAME>.github.io/<REPO>
# git push -f git@github.com:<USERNAME>/<REPO>.git master:gh-pages

# ssh 模式
git push -f git@github.com:hsiangfeng/HexfootMusic.git master:gh-pages

# HTTPS 模式
# git push -f https://github.com/hsiangfeng/HexfootMusic.git master:gh-pages

cd -
```
<Window 用戶必須使用 git bash 意指 Git 提供的工具來執行指令。>
```
sh deploy.sh
```
此時就有新分支gh-page
於setting設定顯示分支即可
![](https://i.imgur.com/5eOm9aM.png)
## 修改config檔案
![](https://i.imgur.com/sU79LUq.png)
