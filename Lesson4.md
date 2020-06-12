## Getting Started
31.图片缓存框架flutter_cache_manager的用法：
CachedNetworkImage(
  imageUrl: 'http://via.placeholder.com/350x200',//加载的url
  placeholder: (context, url) => CircularProgressIndicator(),//等待的时候的进度条
  errorWidget: (context, url, error) => const Icon(Icons.error),//错误时显示的控件
  fadeOutDuration: const Duration(seconds: 1),//出来的动画效果
  fadeInDuration: const Duration(seconds: 3),//进去的动画效果
)

32.provide的用法：
首先生成一个业务类counter.dart:
class Counter with ChangeNotifier {
  int value = 0;
  add() {
    value++;
    notifyListeners();
  }
  subtract() {
    value--;
    notifyListeners();
  }
}
然后在pubspec.yaml中添加provide: ^1.0.2，其次在主页中main（）中声明初始化：
void main() {
//main函数里面引用provide
  var counter = Counter();
  var providers = Providers();
  providers..provide(Provider<Counter>.value(counter));
  runApp(ProviderNode(
    child: MyApp(),
    providers: providers,
  ));
}
如果要引用provider中的数据，则：
Provide<Counter>(
  //在其他页面也是用同样的方法可以引用到provide里面的参数
  builder: (context, child, counter) {
    return Text("${counter.value}");
  },
)
如果要实现provider的业务逻辑，则：
RaisedButton(
  onPressed: () {
    Provide.value<Counter>(context).add();
  },
  child: Text("增加"),
)

33.shared_preferences插件的使用：
首先在pubspec中添加依赖shared_preferences: ^0.5.6，存储值的写法是：
_setData() async {
  //2、存储的方法
  SharedPreferences prefs = await SharedPreferences.getInstance();
  prefs.setInt("save_test", 10);
}
获取值的写法是：
_getData() async {
  //3、取出的方法
  SharedPreferences prefs = await SharedPreferences.getInstance();
  setState(() {
    _aaa = prefs.getInt("save_test");
  });
}
清楚值的写法是：
_removeData() async {
  //4、销毁的方法
  SharedPreferences prefs = await SharedPreferences.getInstance();
  setState(() {
    prefs.remove("save_test");
  });
}

34.url_launcher这个插件可以允许手机拨打电话、发短信、发邮件、跳转浏览器、打开系统应用和指定第三方app

35.本地存储如何实现？
写入的方法是：
Future<String> writeToLocal(String data) async {
  String tempDir = (await getTemporaryDirectory()).path;
  File file = await File("$tempDir/test.txt");
  File result = await file.writeAsString(data);
  print(result.path);
  if (result.existsSync()) {
    return "保存成功，数据为：$data ,  存储路径为$result";
  } else {
    return "保存失败";
  }
}
读取的方法是：
Future<String> readFromLocal() async {
  String tempDir = (await getTemporaryDirectory()).path;
  File file = await File("$tempDir/test.txt");
  String result = await file.readAsString();
  if (result != null) {
    return "读取成功，读取结果为：$result";
  } else {
    return "读取失败";
  }
}
如何引用？
MyRowText("存储到本地", () async {
  String str = await writeToLocal("罗鹏飞") as String;
  setState(() {
    resultbody = str;
  });
})
MyRowText("从本地读取", () async {
  String str = await readFromLocal() as String;
  setState(() {
    resultbody = str;
  });
})

36.拖动列表中的子项进行排序利用ReorderableListView这个控件可以实现：
ReorderableListView(
  header: AppBar(title: Text('ReorderableListViewDemo')),
  children: names.map(_buildCard).toList(),//其中names是一组String数据的集合
  onReorder: _onReorder,
)
_onReorder(int oldIndex, int newIndex) {
  if (oldIndex < newIndex) newIndex = newIndex - 1;
  var name = names.removeAt(oldIndex);
  names.insert(newIndex, name);
  setState(() {
    debugPrint(names.toString());//每一次排序均会输出排序后的列表数据
  });
}

37.

38.

39.对于IOS系统来说，添加权限的地方在ios/Runner/info.plist这个文件中，例如：
<key>NSCameraUsageDescription</key>
<string>请允许APP访问您的相机</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>请允许APP保存图片到相册</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>请允许APP访问您的相册</string>

40.从网络上保存图片到本地使用的是image_gallery_saver插件
