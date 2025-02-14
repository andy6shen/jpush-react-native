# JPush-React-Native

## 1. 安装

```
npm install jpush-react-native --save
```

* 注意：如果项目里没有jcore-react-native，需要安装

  ```
  npm install jcore-react-native --save
  ```

## 2. 配置

### 2.1 Android

* build.gradle

  ```
  android {
        defaultConfig {
            applicationId "yourApplicationId"           //在此替换你的应用包名
            ...
            manifestPlaceholders = [
                    JPUSH_APPKEY: "yourAppKey",         //在此替换你的APPKey
                    JPUSH_CHANNEL: "yourChannel"        //在此替换你的channel
            ]
        }
    }
  ```

  ```
  dependencies {
        ...
        implementation project(':jpush-react-native')  // 添加 jpush 依赖
        implementation project(':jcore-react-native')  // 添加 jcore 依赖
    }
  ```

* AndridManifest.xml

  ```
  <meta-data
  android:name="JPUSH_CHANNEL"
  android:value="${JPUSH_CHANNEL}" />
  <meta-data
  android:name="JPUSH_APPKEY"
  android:value="${JPUSH_APPKEY}" />
  ```

* setting.gradle

  ```
  include ':jpush-react-native'
  project(':jpush-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jpush-react-native/android')
  include ':jcore-react-native'
  project(':jcore-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jcore-react-native/android')
  ```

### 2.2 iOS

### 2.2.1 pod

```
pod install
```

* 注意：如果项目里使用pod安装过，请先执行命令

  ```
  pod deintegrate
  ```

### 2.2.2 手动方式

* Libraries

  ```
  Add Files to "your project name"
  node_modules/jcore-react-native/ios/RCTJCoreModule.xcodeproj
  node_modules/jpush-react-native/ios/RCTJPushModule.xcodeproj
  ```

* Capabilities

  ```
  Push Notification --- ON
  ```

* Build Settings

  ```
  All --- Search Paths --- Header Search Paths --- +
  $(SRCROOT)/../node_modules/jcore-react-native/ios/RCTJCoreModule/
  $(SRCROOT)/../node_modules/jpush-react-native/ios/RCTJPushModule/
  ```

* Build Phases

  ```
  libz.tbd
  libresolv.tbd
  UserNotifications.framework
  libRCTJCoreModule.a
  libRCTJPushModule.a
  ```

## 3. 引用

### 3.1 Android

参考：[MainApplication.java](https://github.com/jpush/jpush-react-native/tree/master/example/android/app/src/main/java/com/example/MainApplication.java)

### 3.2 iOS

参考：[AppDelegate.m](https://github.com/jpush/jpush-react-native/tree/master/example/ios/example/AppDelegate.m) 

## 4. API

详见：[index.js](https://github.com/jpush/jpush-react-native/blob/master/index.js)

## 5.  其他

* 集成前务必将example工程跑通
* JPush3.5.7&&JCore1.3.7属于重构版本，API主要缺少本地通知，如有紧急需求请前往[极光社区](https://community.jiguang.cn/c/question)
* 目前react-native link还不完善，待下个版本完成
* 上报问题还麻烦先调用JPush.setLoggerEnable({"debug": true}，拿到debug日志

 