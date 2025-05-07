---
title: React native 懸浮視窗
tags: [React Native]
layout: single
date: 2020-03-04
toc: true
toc_sticky: true

---

[Android Floating Widget Tutorial – Display Widget Over Apps](https://www.simplifiedcoding.net/android-floating-widget-tutorial/)

[Creating floating chat head like Messenger in Android!](https://thunderwiring.wordpress.com/2018/04/01/creating-floating-chat-head-like-messenger-in-android/)

[使用RN出現問題](https://stackoverflow.com/questions/52339231/floating-widget-in-react-native)

## Step1. 創建 React Native 專案
React Native 是一框架讓 JavaScript 也能輕鬆開發 Android 及 iOS App，其效能也較接近原生 Native App。
### 前置作業
安裝 Node.JS v4 以上版本(筆者安裝 v8 版本)，安裝教學請參考此文。
### 步驟摘要
1. 完成前置作業。
2. 使用 npm 安裝 create-react-native-app 套件於全域。
3. 於電腦與行動設備(手機或模擬器)上安裝 Expo(電腦及開發設備上都要)。
4. 使用 create-react-native-app 創建 App 專案。
5. 切換到專案目錄下使用 npm start 指令來直行專案，或者選擇使用 Expo 來啟動。
6. 依照指示將該專案值入行動設備(或模擬器)中。
7. 看到 App 畫面後，請搖晃手機至開發選單出現為止，接著選擇「Enable Hot Reloading」開始進行 App 開發。

### 詳細過程
#### 步驟 1
打開終端機(命令提示字元)，使用下列指令安裝 create-react-native-app 於全域環境。
```
npm install -g create-react-native-app
```
![](https://i.imgur.com/aqbPmv7.png)
若過程順利，將出現類似以下畫面。 
![](https://i.imgur.com/DFX4ACl.png)

#### 步驟 2
進入到 Expo 於您的電腦中下載安裝 Expo XDE，並於您的行動裝置中也安裝 Expo (Android 版、iOS 版)。
![](https://i.imgur.com/U0kVG3h.png)



#### 步驟 3
於終端機(命令提示字元)中，使用下列指令建立新專案(時間需要幾分鐘)：
```
create-react-native-app <專案名稱>  
```

#### 步驟 4
使用下列兩行指令，切換至目錄中，並啟動專案：
```
cd AwesomeProject  
npm start  
```

> 備註：除了 npm start 外，您也可以選擇使用 Expo 來啟動專案。

#### 步驟 5
啟動完成後，請將電腦與手機連接至同一網域(同一 WiFi)，並打開 Expo 掃描畫面中之 QR Code。
![](https://i.imgur.com/1kOurWu.png)
![](https://i.imgur.com/g95iHj7.png)



備註：植入方法不僅僅 QR Code 中一種，您可依照您的需求來選擇植入方式。

#### 步驟 6
若過程順利即可看到您的 App 畫面，並可依照指示搖晃手機，直到出現下方表單為止。選擇「Enable Hot Reloading」開始進行 App 開發。



### 開始開發
打開專案目錄，編輯 App.js 檔案。可先行改變 <Text> 標簽中的值，筆者程式修改如下：

``` javascript
import React from 'react';  
import { StyleSheet, Text, View } from 'react-native';

export default class App extends React.Component {  
  render() {
    return (
      <View style={styles.container}>
        <Text>Hello Makee.io!</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({  
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

若過程順利，手機則會自動更新如下方畫面：
![](https://i.imgur.com/gj94Wbw.png)

###### 資料來源：[[RN] React Native 起手教學](https://oranwind.org/react-native-started/)

## 打包
[expo](https://stackoverflow.com/questions/44301539/react-native-generate-apk-and-ipa-using-expo)

