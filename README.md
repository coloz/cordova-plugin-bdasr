### 前言
1. 这是一个百度语音识别的cordova插件。为什么使用百度语音识别，因为是免费的，识别的准确度也还挺不错的。
2. 这个插件只包含语音识别功能，不包含其他的比如唤醒、长语音功能。
3. 百度语音开发文档 http://ai.baidu.com/docs#/ASR-API/top

### 支持平台
1. Android
2. iOS

### 安装
1. 在线npm安装
 `cordova plugin add cordova-plugin-bdasr --variable APIKEY=[your apikey] --variable SECRETKEY=[your secretkey] --variable APPID=[your appid]`
2. 在线url安装
  `cordova plugin add https://github.com/hhjjj1010/cordova-plugin-bdasr.git --variable APIKEY=[your apikey] --variable SECRETKEY=[your secretkey] --variable APPID=[your appid]`

3. 本地安装
`cordova plugin add /your localpath --variable APIKEY=[your apikey] --variable SECRETKEY=[your secretkey] --variable APPID=[your appid]  `


### API使用

     // 开启语音识别
     cordova.plugins.bdasr.startSpeechRecognize();

    // 语音识别事件监听
     cordova.plugins.bdasr.addEventListener(function (res) {
        // res参数都带有一个type
        if (!res) {
          return;
        }

        switch (res.type) {
          case "asrReady": {
            // 识别工作开始，开始采集及处理数据
            $scope.$apply(function () {
              // TODO
            });
            break;
          }

          case "asrBegin": {
            // 检测到用户开始说话
            $scope.$apply(function () {
              // TODO
            });
            break;
          }

          case "asrEnd": {
            // 本地声音采集结束，等待识别结果返回并结束录音
            $scope.$apply(function () {
              // TODO
            });
            break;
          }

          case "asrText": {
            // 语音识别结果
            $scope.$apply(function () {
              var message = angular.fromJson(res.message);
              var results = message["results_recognition"];
            });
            break;
          }

          case "asrFinish": {
            // 语音识别功能完成
            $scope.$apply(function () {
              // TODO
            });
            break;
          }

          case "asrCancel": {
            // 语音识别取消
            $scope.$apply(function () {
              // TODO
            });
            break;
          }

          default:
            break;
        }

      }, function (err) {
         alert("语音识别错误");
      });

    // 主动结束语音识别
    cordova.plugins.bdasr.closeSpeechRecognize();

    // 主动取消语音识别
    cordova.plugins.bdasr.cancelSpeechRecognize();

#### 写在最后
因为对android开发并不是很熟悉，所以特此记录在开发插件的android端时遇到的一些问题
1. 加载so库，对应不同的平台，需要添加不同平台的.so文件

        <source-file src="src/android/libs/armeabi/libBaiduSpeechSDK.so" target-dir="libs/armeabi"/>
        <source-file src="src/android/libs/armeabi/libvad.dnn.so" target-dir="libs/armeabi"/>

        <source-file src="src/android/libs/x86_64/libBaiduSpeechSDK.so" target-dir="libs/x86_64"/>
        <source-file src="src/android/libs/x86_64/libvad.dnn.so" target-dir="libs/x86_64"/>

        <source-file src="src/android/libs/x86/libBaiduSpeechSDK.so" target-dir="libs/x86"/>
        <source-file src="src/android/libs/x86/libvad.dnn.so" target-dir="libs/x86"/>

        <source-file src="src/android/libs/arm64-v8a/libBaiduSpeechSDK.so" target-dir="libs/arm64-v8a"/>
        <source-file src="src/android/libs/arm64-v8a/libvad.dnn.so" target-dir="libs/arm64-v8a"/>

        <source-file src="src/android/libs/armeabi-v7a/libBaiduSpeechSDK.so" target-dir="libs/armeabi-v7a"/>
        <source-file src="src/android/libs/armeabi-v7a/libvad.dnn.so" target-dir="libs/armeabi-v7a"/>

2. PermissionHelper.requestPermission()方法封装了动态获取权限的代码
动态获取权限的回调方法：public void onRequestPermissionResult(int requestCode, String[] permissions, int[] grantResults) throws JSONException {}）



bash: rt: command not found

