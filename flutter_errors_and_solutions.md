1、新建flutter项目，在模拟器上运行报错如下：**Could not initialize class org.codehaus.groovy.reflection.ReflectionCache**，解决方法：打开Android文件夹，打开gradle文件，wrapper文件夹在的gradle-wrapper文件，更改distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.2-all.zip中gradle版本为最新版本

2、StatefulWidget组件需要在布局中抽出，以防止build重绘时绘制全部组件

3、常见的性能瓶颈：Skia函数调用中的saveLayer和clipPath。几乎出现在所有的Material组件：card/chip/button

4、multi_image_picker使用时出现Before Android 4.1, method android.graphics.PorterDuffColorFilter androidx.vectordrawable.graphics.drawable.VectorDrawableCompat.updateTintFilter(android.graphics.PorterDuffColorFilter, android.content.res.ColorStateList, android.graphics.PorterDuff$Mode) would have incorrectly overridden the package-private method in android.graphics.drawable.Drawable。需要将targetSDK修改为23一下，因为是Android6以下权限问题。

5、gradle-properties修改

```
android.useAndroidX=true
android.enableJetifier=true
```

6、修改MinSdk导致错，需要将MinSDK修改为新建项目的MinSDK版本

7、Flutter处理网络返回JSON数据，使用json_serializable。在终端使用命令如下：flutter packages pub run build_runner build

8、Tips: flutter结合后端进行开发时，需要将后端数据与前端Model、Provider数据字段名称一致。否则不能将数据进行绑定。数据将会获得空值。

9、flutter开发过程中新增插件时插件gradle依赖版本低于应用程序所需gradle版本导致重新编译报错。解决：找到插件位置External Libraries --> Flutter Plugins -->.....，修改build.gradle内的版本为应用程序的gradle版本。![image-20201217230400988](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201217230400988.png)

10、audioplayer插件编译报错：sdk.dir找不到，需要在插件编译目录下面新增一个local.properties文件，将项目下面的local.properties文件内容复制到新增文件下面即可。
![image-20201220210450759](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201220210450759.png)

11、file_picker插件编译报错：![image-20201220210422909](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201220210422909.png)![image-20201221130252252](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201221130252252.png)
解决网址：https://stackoverflow.com/questions/64932702/flutter-failure-build-failed-with-an-exception
![image-20201221130342958](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201221130342958.png)

12、项目插件SharedPreference报错：[ERROR:flutter/lib/ui/ui_dart_state.cc(177)] Unhandled Exception: MissingPluginException(No implementation found for method getAll on channel plugins.flutter.io/shared_preferences)
解决：![image-20201222154838802](C:\Users\ViaX\AppData\Roaming\Typora\typora-user-images\image-20201222154838802.png)

13、对于一个新建的空列表，没有初始化赋值的列表。不应该讲一个可能为空的操作数据赋值给这个列表，如果这个操作返回的数据为空，那么列表也为空，所以列表的函数isNotEmpty或者isEmpty不能使用，需要先判断操作数据返回值是否为空。

