---
title: Android APP 打包 for Window
tags: [React Native]

---

# Android APP 打包 for Window
###### tags: `React Native`
## Step1.使用Keytool產生一把Key

進入資料夾 cd C:\Program Files\Java\jre1.8.0_191\bin
```
keytool -genkey -v -keystore ${名稱}.keystore -alias ${別名} -keyalg RSA -keysize 2048 -validity 10000
```
Example：
```
keytool -genkey -v -keystore HelloRN.keystore -alias HelloRN -keyalg RSA -keysize 2048 -validity 10000
```
:::info
React Native 的 .gitignore 預設有 *.keystore
請勿移除，會有資安問題
:::
## Step2. 移動新產生的 Keystore
C:\Program Files\Java\jre1.8.0_191\bin目錄下的 ==${名稱}.keystore== 
移至專案中/adnroid/app目錄下

## Step3.設定 gradle 的全域變數(給 App 簽名)
編輯 ~/.gradle/gradle.properties
(如果沒有這個檔案自己新增一個，然後新增下列文字)
``` javascript=
${APPNAME}_STORE_FILE=${名稱}.keystore
${APPNAME}_KEY_ALIAS=${別名}
${APPNAME}_STORE_PASSWORD=這裡輸入儲存庫密碼
${APPNAME}_KEY_PASSWORD=這裡輸入金鑰密碼
```

## Step4.設定專案中的 gradle
開啟專案當中的 android/app/build.gradle，新增下列的配置
``` javascript=
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(${APPNAME}_RELEASE_STORE_FILE)
            storePassword ${APPNAME}_RELEASE_STORE_PASSWORD
            keyAlias ${APPNAME}_RELEASE_KEY_ALIAS
            keyPassword ${APPNAME}_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```
## Step5.建立離線Bundle檔-Build Bundle
:::info
專案中已建立可跳過此步驟
:::
建立assets資料夾(存儲打包的JavaScript的文件)。
```
mkdir -p android/app/src/main/assets
```
通過curl從ReactNative包管理器中獲取的JavaScript文件。
```
"http://localhost:8081/index.android.bundle" >android/app/src/main/assets/index.android.bundle
```
開始建立
```
react-native bundle --entry-file index.js --bundle-output ./android/app/src/main/assets/index.android.jsbundle --platform android --assets-dest ./android/app/src/main/res/ --dev false
```

## Step6. 打包成APK
進入android目錄下，使用gradlew來構建發布版本的APK
```
cd android && gradlew assembleRelease
```
```
cd android && ./gradlew assembleRelease
```

## Step7. 成功取得APK檔
APK檔案路徑
```
android/app/build/outputs/apk/release/
```

## FAILURE
### FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processReleaseResources'.
> Failed to process resources, see aapt output above for details.

==Add following code into currentBundleTask's creation block (after doFirst block)==
```
doLast {
    def moveFunc = { resSuffix ->
        File originalDir = file("${resourcesDir}/drawable-${resSuffix}")
        if (originalDir.exists()) {
            File destDir = file("${resourcesDir}/drawable-${resSuffix}-v4")
            ant.move(file: originalDir, tofile: destDir)
        }
    }
    moveFunc.curry("ldpi").call()
    moveFunc.curry("mdpi").call()
    moveFunc.curry("hdpi").call()
    moveFunc.curry("xhdpi").call()
    moveFunc.curry("xxhdpi").call()
    moveFunc.curry("xxxhdpi").call()
}
```

### FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:validateSigningRelease'.
> Keystore file 'E:\Yoke\YokeProductionLine\android\app\Yoke.keystore' not found for signing config 'release'.

==參考Step2==

## 相關問題
### 重複文件錯誤
自定義node_modules / react-native / react.gradle來解決重複文件錯誤

==Add following code into currentBundleTask's creation block (after doFirst block)==
```
doLast {
    def moveFunc = { resSuffix ->
        File originalDir = file("${resourcesDir}/drawable-${resSuffix}")
        if (originalDir.exists()) {
            File destDir = file("${resourcesDir}/drawable-${resSuffix}-v4")
            ant.move(file: originalDir, tofile: destDir)
        }
    }
    moveFunc.curry("ldpi").call()
    moveFunc.curry("mdpi").call()
    moveFunc.curry("hdpi").call()
    moveFunc.curry("xhdpi").call()
    moveFunc.curry("xxhdpi").call()
    moveFunc.curry("xxxhdpi").call()
}
```

### error: uncompiled PNG file passed as argument. Must be compiled first into .flat file..

```
//In gradle.properties
android.enableAapt2=false
```