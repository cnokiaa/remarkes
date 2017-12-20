# react-native
  `npm update -g`   cmd下升级npm

[环境安装地址](http://reactnative.cn/docs/0.37/getting-started.html#content)

### 安装python2

    npm config set registry https://registry.npm.taobao.org --global
    npm config set disturl https://npm.taobao.org/dist --global

### 安装atom + Nuclide

    git clone https://github.com/facebook/nuclide
    cd nuclide
    npm install

### 创建启动项目

`react-native init projectName`	创建项目init

`react-native run-android`	到项目文件夹下启动项目

* run-android 出现download gradle ，下载gradle对应版本放到
  C:\Users\liu\.gradle\wrapper\dists\gradle-2.14.1-all\8bnwg5hd3w55iofp58khbp6yv  下

### 手机联调

唤起手机dev setting设置界面(需先在应用程序设置-权限管理中-开启 悬浮窗)

`adb shell input keyevent 82` live reload

其他指令

`adb devices`

`adb reverse tcp:8081 tcp:8081`

`react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/`

`react-native bundle --entry-file index.ios.js --bundle-output ./ios/bundle/index.ios.jsbundle --platform ios --assets-dest ./ios/bundle --dev false`

http://192.168.19.130:8081/index.android.bundle

http://localhost:8081/debugger-ui

* 注意:外面要套一层view 不然报错

### 打包安卓apk
1. 生成签名（android/app）

`keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000`

2. android/gradle.properties增加以下内容


    MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
    MYAPP_RELEASE_KEY_ALIAS=my-key-alias
    MYAPP_RELEASE_STORE_PASSWORD=xx
    MYAPP_RELEASE_KEY_PASSWORD=xx

3、android/app/build.gradle增加以下内容


    ...
    android {
      ...
      defaultConfig {
        ...
      }
      signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
      }
      buildTypes {
        release {
          ...
          signingConfig signingConfigs.release
        }
      }
    }

4、android目录下执行
`gradlew assembleRelease`

### 设置启动图片

[android 设置启动图片参考链接](http://www.myronliu.com/2016/07/22/react-native/react-native_launch/)

`android/app/src/main/res/drawable-hdpi`
里加上一个图片作为程序启动图 (名称随意，例如：splash.png)


android/app/src/main/res/values/styles.xml 里加上

`<item name="android:windowBackground">@drawable/splash</item>`
