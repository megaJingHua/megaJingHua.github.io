---
title: 'React Native: Android環境設定 on Windows For 實體手機_mega版'
tags: [React Native]

---

# React Native: Android環境設定 on Windows For 實體手機_mega版
###### tags: `React Native`
##### RN遊戲引擎
https://www.npmjs.com/package/react-native-game-engine
## Step1.安裝
#### 1. [node.js](https://nodejs.org/en/)
#### 2. [Java SE Development Kit(JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
#### 3. [Android Studio](https://developer.android.com/studio/index.html)

## Step2.確認node.js是否安裝
安裝node時會自動配置好環境變數，主要查看node是否安裝
```
node -v
```
![](https://i.imgur.com/PtrUflj.png)

## Step3.設定JDK環境變數
#### 1. 進入  控制台\系統及安全性\系統進階系統設定->環境變數
![](https://i.imgur.com/GTlmna1.png)
#### 2. 設定使用者變數：JAVA_HOME環境變數
:::info
變數：JAVA_HOME 值：…\Java\jdk…
:::
>自行找尋路徑>Java\jdk...

![](https://i.imgur.com/TJBoL5Q.jpg)
#### 3. 測試JDK是否安装到環境變數中
```
java -version
```
![](https://i.imgur.com/2sySJsB.png)


## Step4.設定Android Studio環境變數並載SDK
#### 1. 進入  控制台\系統及安全性\系統進階系統設定->環境變數
![](https://i.imgur.com/GTlmna1.png)
#### 2. 設定使用者變數：ANDROID_HOME環境變數(變數：ANDROID_HOME 值：…\AppData\Local\Android\Sdk)
:::info
自行找尋路徑>AppData\Local\Android\Sdk
AppData的資料夾會隱藏需開啟
![](https://i.imgur.com/BHF6kWc.png)
:::

![](https://i.imgur.com/aphtXmF.png)

#### 3. 設定系統變數：PATH環境變數
:::info
變數：PATH 值：…\AppData\Local\Android\Sdk\tools
變數：PATH 值：…\AppData\Local\Android\Sdk\platform-tools
:::

![](https://i.imgur.com/3WpDJhm.jpg)

#### 4. 進入Android Studio開啟configure>SDK Manager>Tools下載
![](https://i.imgur.com/36mEgkJ.png)

**必需載下方SDK**
:::info
* Android SDK Tools
* Android SDK Platform-Tools
* Android SDK Bulid-Tools
* Google USB Drive
* Android 8.0 (android版本自行選用)
* Android Support Repostiory
:::

## Step.5 安裝 react native
```
npm install -g react-native-cli
```
## Step.6 開發
[使用手機開發](#使用手機開發)
[使用手機開發](#使用模擬器開發)

# 使用手機開發
## Step.6建立APP專案 & Run android app
#### 1. 建立資料夾YourProject>進入YourProject資料夾後建立專案
```
react-native init YourProject
cd YourProject
```
#### 2. 手機開啟開發模式>進入開發人員選項開啟USB偵錯
![](https://i.imgur.com/FzQXbfQ.png)

#### 3. Run android app
```
react-native run-android
```
連接成功畫面(node.js視窗可關閉)
![](https://i.imgur.com/cAoQOMU.jpg)

#### 4. 手機開發
:::info
首次連接成功時，手機會出現下面error
:::
![](https://i.imgur.com/c2mcRXx.png)
:::info
搖晃手機出現選單
:::
![](https://i.imgur.com/UyiiFjl.png)

# 使用模擬器開發
## Step.6建立APP專案 & Run android app
#### 1. 建立資料夾YourProject>進入YourProject資料夾後建立專案
```
react-native init YourProject
cd YourProject
```
#### 2.開啟Android Studio新建專案


ctrl + m
http://localhost:8081/debugger-ui/








