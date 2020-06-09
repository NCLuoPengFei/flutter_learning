## Getting Started
11.Json直接转为数据集合的方式：
List lists = [];///默认是为空的
loadData() async {
  String dataURL = "https://jsonplaceholder.typicode.com/posts";
  http.Response response = await http.get(dataURL);
  setState(() {
    lists = json.decode(response.body);
  });
}
var title=lists[0][‘title’]就可以获得数据了

12.如何在全屏生成一个进度圈圈：
getBody() {
  if (ifListNull()) {///假如数据为空
    return Center(child: CircularProgressIndicator());///显示进度条
  } else {
    return getListView();///如果有数据，则展示数据
  }
}

13.Container中背景装饰的使用，制作渐变色的背景和设置边框：
decoration: BoxDecoration(
    gradient: LinearGradient(
        colors: [Colors.red, Colors.blue, Colors.amberAccent]),//红色蓝色黄色的渐变
    border: Border.all(width: 5.0, color: Colors.greenAccent))//宽度是5的绿色边框

14.生成一个GridView的方式1：
GridView(
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 3,//分几列
    mainAxisSpacing: 3.0,//上下之间的边距
    crossAxisSpacing: 3.0,//左右之间的边距
    childAspectRatio: 0.7,//横向距离除以纵向距离
  ),
  children: <Widget>[
    。。。
  ],
)
生成GridView的方式2:
GridView.count(
  primary: true,
  padding: const EdgeInsets.all(1.0),
  crossAxisCount: 2,
  childAspectRatio: 0.85,
  mainAxisSpacing: 1.0,
  crossAxisSpacing: 1.0,
  children: <Widget>[
    。。。
  ],
)

15.Stack层叠布局中的alignment属性设置为const FractionalOffset(0.5,0.5)指的是其中的内容居中摆放，其中第一个数字范围是【0，1】是X轴方向的，第二个数字范围也是【0，1】是Y轴方向的，eg.如果是const FractionalOffset(0.0,0.0)的位置是左上角，其他位置可推理。

16.制作圆形头像的方法：
CircleAvatar(
  backgroundImage: NetworkImage(
      ‘Url…’),
  radius: 100.0,
)

17.绝对布局的使用：
使用Positioned这个Widget，举个例子：
new Positioned(
  child: new Text(
    'hello',
    style: TextStyle(
      fontSize: 30.0,
    ),
  ),
  top: 10.0,//距离顶部10个单位的像素
  left: 20.0,//距离左边20个单位的像素
)

18.Container中padding属性的用法（与margin（外边距）同理）：
EdgeInsets.all(20.0)指的是上下左右都设置内边距20个单位的像素,等同于padding: EdgeInsets.fromLTRB(20.0, 20.0, 20.0, 20.0)，括号中分别表示LTRB（左上右下）

19.Row中mainAxisAlignment属性的用法：
mainAxisAlignment: MainAxisAlignment.spaceBetween指的是Row中的元素分左右靠边对齐，mainAxisAlignment: MainAxisAlignment.spaceAround指的是Row中的元素分别靠边距离等于元素之间距离的两倍，mainAxisAlignment: MainAxisAlignment.spaceEvenly指的是Row中的元素分别靠边距离等于元素之间的距离;还有start指的是Row中元素都靠左边，end指的是Row中元素都靠右边，center指的是Row中元素靠中间

20.MaterialApp中如果设置debugShowCheckedModeBanner为false时，则右上角的debug图标就会消失，默认时true
