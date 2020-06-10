## Getting Started
21.fluttertoast插件的使用：
Fluttertoast.showToast(
    msg: '水果是$_selectedFruit',
    toastLength: Toast.LENGTH_LONG,//toast
    gravity: ToastGravity.BOTTOM,//toast的位置
    backgroundColor: Colors.red,//toast的背景颜色
    textColor: Colors.white,//toast字的颜色
    timeInSecForIos: 1)

22.Scaffold中的drawer属性可以添加侧边栏，侧边栏控件生成的格式：
Drawer getNavDrawer(BuildContext context) {
  ListView listView = ListView(children: myNavChildren);
  return Drawer(
    child: listView,
  );
}

23.基本对话框的使用：
AlertDialog dialog = AlertDialog(
    content: Text(
  "Hello World!",
  style: TextStyle(fontSize: 30.0),
))
showDialog(context: context, builder: (BuildContext context) => dialog);

24.使用自定义字体：
首先在pubspec.yaml中添加：
fonts:
  - family: Pacifico
    fonts:
      - asset: data_repo/fonts/Pacifico-Regular.ttf
        weight: 400
然后在代码中Text的控件的style属性中这么写：
fontFamily: 'Pacifico’就可以了

25.如何设置主题色？
在MaterialApp中的theme参数设置为：
theme: ThemeData(
  primarySwatch: Colors.deepOrange,
  accentColor: Colors.lightGreenAccent,
  // Set background color
  backgroundColor: Colors.black12,
)
控件如何调用主题色呢？
color: Theme.of(context).accentColor

26.如何设置顶部状态栏的主题色？
如果没有手动设置过状态栏，则
Widget build(BuildContext context) {
  var body = getBody();
  ///如果手动设置过状态栏，就不可以用 AnnotatedRegion ，会影响
  if (customSystemUIOverlayStyle) {
    return body;
  }
  ///如果没有手动设置过状态栏，就可以用 AnnotatedRegion 直接嵌套显示
  return AnnotatedRegion<SystemUiOverlayStyle>(
    value: SystemUiOverlayStyle.dark,
    child: body,
  );
}
如果需要手动设置状态栏的颜色，则
onPressed: () {
  ///手动修改
  setState(() {
    customSystemUIOverlayStyle = true;
  });
  SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle.light);
}

27.Text中限制文字显示的行数可使用maxLines这个属性，如果显示不下后面添加点点点，可使用overflow: TextOverflow.ellipsis来表示；富文本可使用RichText来表示，其使用TextSpan来展示文字,例如：
RichText(//富文本
  text: TextSpan(
      text: 'luopengfei',
      style: TextStyle(
        color: Colors.deepPurple,
        fontSize: 20.0,
        fontWeight: FontWeight.bold,
      ),
      children: [
        TextSpan(
            text: ' is best',
            style: TextStyle(
              color: Colors.redAccent,
              fontSize: 40.0,
              fontWeight: FontWeight.bold,
            ))
      ]),
)

28.悬浮弹出菜单使用PopupMenuButton这个控件，可参考：
PopupMenuButton(
  onSelected: (value) {
    setState(() {
      _currentContent = value;
    });
    print('数值是：'+_currentContent);
  },
  itemBuilder: (BuildContext context) => [
    PopupMenuItem(
      child: Text('Home'),
      value: 'Home',
    ),
  ],
)

29.按比例显示的控件是AspectRatio，其中aspectRatio这个参数用于标记（16/9）

30.用于给控件边框加圆角的控件是ClipRRect，案例是：
ClipRRect(
  borderRadius: BorderRadius.only(
    topLeft: Radius.circular(4.0),//左上的弧度
    topRight: Radius.circular(4.0),//右上的弧度
    bottomLeft: Radius.circular(4.0),//左下的弧度
    bottomRight: Radius.circular(4.0)//右下的弧度
  ),
  child: Image.network(
    post.imageUrl,
    fit: BoxFit.cover,
  ),
)
