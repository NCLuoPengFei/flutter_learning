## Getting Started
41.文字上的一些展示特效使用的是animated_text_kit插件

42.拍照&从相册选取单个照片等方式获取照片使用的是image_picker插件

43.从相册选取多张照片可以使用multi_image_picker插件

44.

45.从手机上选取音频、视频、图片以及任意格式的一个或多个使用的是file_picker插件

46.倒计时做某件事的写法是：
Future.delayed(Duration(seconds: 3)).then((value) {
  （要做的事情）
})

47.loading等待框在开发中的使用：
ProgressDialog pr;
build中。。
pr = new ProgressDialog(context, showLogs: true);
pr.style(message: 'Please wait...');
pr.show();//展示出来
pr.hide().whenComplete(() {//关闭掉且当完成了实现哪些内容
  Navigator.of(context).push(CupertinoPageRoute(
      builder: (BuildContext context) => SecondScreen()));
});

48.实现Android端透明有沉浸感的顶栏效果，可以在main方法中加入如下代码块：
if (Platform.isAndroid) {
  // 以下两行 设置android状态栏为透明的沉浸。写在组件渲染之后，是为了在渲染后进行set赋值，覆盖状态栏，
  // 写在渲染之前MaterialApp组件会覆盖掉这个值。
  SystemUiOverlayStyle systemUiOverlayStyle =
      SystemUiOverlayStyle(statusBarColor: Colors.transparent);
  SystemChrome.setSystemUIOverlayStyle(systemUiOverlayStyle);
}

49.实现IOS端顶部主题浅色或者深色主题的方法如一下代码块：
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //下面这段话的意思是使得状态栏的主题设为深色主题，即时间和信号等信息为黑色
    return AnnotatedRegion<SystemUiOverlayStyle>(
      value: SystemUiOverlayStyle.dark,//也可以设置成light
      child: MaterialApp(
        debugShowCheckedModeBanner: false,
        title: '腾讯体育',
        initialRoute: '/second',
        routes: {
          '/second': (context) => IndexPage(),
        },
      ),
    );
  }
}

50.flutter布局中增加间隔一般采用如下的代码进行设置：
SizedBox(
  height: 10.0,
)