# What is This Project?

This project demonstrates that `expo-image-picker` crashes when `ImagePicker.launchCameraAsync` is used on an Android device due to a stack trace like the following:
```
E/AndroidRuntime: FATAL EXCEPTION: main
    Process: com.expoimagepickercameracrash, PID: 12002
    java.lang.RuntimeException: Unable to resume activity {com.expoimagepickercameracrash/com.expoimagepickercameracrash.MainActivity}: android.os.FileUriExposedException: file:///data/user/0/com.expoimagepickercameracrash/cache/ImagePicker/2af0fb89-c249-42f5-895a-8f8f47b50b3c.jpg exposed beyond app through ClipData.Item.getUri()
        at android.app.ActivityThread.performResumeActivity(ActivityThread.java:3645)
        at android.app.ActivityThread.handleResumeActivity(ActivityThread.java:3685)
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1643)
        at android.os.Handler.dispatchMessage(Handler.java:105)
        at android.os.Looper.loop(Looper.java:164)
        at android.app.ActivityThread.main(ActivityThread.java:6541)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.Zygote$MethodAndArgsCaller.run(Zygote.java:240)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:767)
     Caused by: android.os.FileUriExposedException: file:///data/user/0/com.expoimagepickercameracrash/cache/ImagePicker/2af0fb89-c249-42f5-895a-8f8f47b50b3c.jpg exposed beyond app through ClipData.Item.getUri()
        at android.os.StrictMode.onFileUriExposed(StrictMode.java:1958)
        at android.net.Uri.checkFileUriExposed(Uri.java:2348)
        at android.content.ClipData.prepareToLeaveProcess(ClipData.java:941)
        at android.content.Intent.prepareToLeaveProcess(Intent.java:9735)
        at android.content.Intent.prepareToLeaveProcess(Intent.java:9720)
        at android.app.Instrumentation.execStartActivity(Instrumentation.java:1609)
        at android.app.Activity.startActivityForResult(Activity.java:4472)
        at android.app.Activity.startActivityForResult(Activity.java:4430)
        at expo.modules.imagepicker.ImagePickerModule.startActivityOnResult(ImagePickerModule.java:754)
        at expo.modules.imagepicker.ImagePickerModule.launchCameraWithPermissionsGranted(ImagePickerModule.java:201)
        at expo.modules.imagepicker.ImagePickerModule.access$000(ImagePickerModule.java:60)
        at expo.modules.imagepicker.ImagePickerModule$1.onPermissionsResult(ImagePickerModule.java:156)
        at expo.modules.permissions.PermissionsService$1.onPermissionResult(PermissionsService.java:56)
        at expo.adapters.react.services.UIManagerModuleWrapper$5.onRequestPermissionsResult(UIManagerModuleWrapper.java:217)
        at com.facebook.react.ReactActivityDelegate$1.invoke(ReactActivityDelegate.java:201)
        at com.facebook.react.ReactActivityDelegate.onResume(ReactActivityDelegate.java:111)
        at com.facebook.react.ReactActivity.onResume(ReactActivity.java:64)
        at android.app.Instrumentation.callActivityOnResume(Instrumentation.java:1354)
        at android.app.Activity.performResume(Activity.java:7079)
        at android.app.ActivityThread.performResumeActivity(ActivityThread.java:3620)
        at android.app.ActivityThread.handleResumeActivity(ActivityThread.java:3685) 
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1643) 
        at android.os.Handler.dispatchMessage(Handler.java:105) 
        at android.os.Looper.loop(Looper.java:164) 
        at android.app.ActivityThread.main(ActivityThread.java:6541) 
        at java.lang.reflect.Method.invoke(Native Method) 
        at com.android.internal.os.Zygote$MethodAndArgsCaller.run(Zygote.java:240) 
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:767) 
E/unknown:ReconnectingWebSocket: Error occurred, shutting down websocket connection: Websocket exception
    java.io.EOFException
        at okio.RealBufferedSource.require(RealBufferedSource.java:61)
        at okio.RealBufferedSource.readByte(RealBufferedSource.java:74)
        at okhttp3.internal.ws.WebSocketReader.readHeader(WebSocketReader.java:117)
        at okhttp3.internal.ws.WebSocketReader.processNextFrame(WebSocketReader.java:101)
        at okhttp3.internal.ws.RealWebSocket.loopReader(RealWebSocket.java:274)
        at okhttp3.internal.ws.RealWebSocket$2.onResponse(RealWebSocket.java:214)
        at okhttp3.RealCall$AsyncCall.execute(RealCall.java:206)
        at okhttp3.internal.NamedRunnable.run(NamedRunnable.java:32)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1162)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:636)
        at java.lang.Thread.run(Thread.java:764)
```

# How Can I Reproduce This Crash?

You do NOT need an actual Android device to repro this crash.  Just run this project on an Android simulator (e.g. Nexus 5 API 26 (Android 8.0.0, API 26)).  It will crash every time in the emulator.