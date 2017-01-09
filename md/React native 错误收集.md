# React native 错误收集

## 打包js

    react-native bundle --entry-file index.android.js --bundle-output ./app/src/main/assets/index.android.bundle --platform android --assets-dest ./app/src/main/res/ --dev false




#### 1.java.lang.IllegalAccessError: Method 'void android.support.v4.net.ConnectivityManagerCompat.()' is inaccessible to class 'com.facebook.react.modules.netinfo.NetInfoModule' (declaration of 'com.facebook.react.modules.netinfo.NetInfoModule' appears in /data/app/package.name-2/base.apk)

注意：小坑一个，如果遇到。请按第6项修改，并且要保证 react-native 版本是0.21.0以上
修改如下文件

.gitignore（在该文件里添加排除项，node_modules/ 和 npm-debug.log）

app/build.gradle (将 'com.android.support:appcompat-v7:23.2.1' 改为 'com.android.support:appcompat-v7:23.0.1')

gradle.properties (在文件末尾添加，android.useDeprecatedNdk=true)


#### 2.Warning:Conflict with dependency 'com.google.code.findbugs:jsr305'. Resolved versions for app (3.0.0) and test app (2.0.1) differ. See http://g.co/androidstudio/app-test-app-conflict for details.

在 build.gradle 里加入

    configurations.all {
        resolutionStrategy.force 'com.google.code.findbugs:jsr305:1.3.9'
    }


#### 3. com.facebook.react.bridge.JSExecutionException: ReferenceError: Can't find variable: __fbBatchedBridge
