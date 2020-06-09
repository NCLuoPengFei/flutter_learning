## Getting Started
1.Card组件就是自带圆角的容器，其elevation属性为阴影的大小

2.ListTile组件中，leading属性是左侧的容器（Widget）、title属性是主元素容器（Widget）、subtitle属性是副元素容器（Widget）、trailing属性是右侧的容器（Widget）、dense属性如果为true，则主元素容器变小、isThreeLine属性如果为true，则显示的是三行（默认是两行）

3.使用MaterialApp中的routes属性设置默认显示的页面，通过标签映射的方式（'/': (context) => FirstScreen()），然后使用initialRoute属性指定默认展示页面的标签（initialRoute: ‘/‘）

4.在MaterialApp中某个页面中要跳转页面可以使用（Navigator.pushNamed(context, '/second’);）来进行跳转

5.在MaterialApp中某个页面如果要返回到前面跳转的页面，可以使用（Navigator.pop(context);）来进行返回

6.状态类构造函数的格式样式是：TodosScreen({Key key, @required this.todos}) : super(key: key);

7.生成集合的方法：
class Todo {
  final String title;
  final String description;
  Todo(this.title, this.description);
}

下面这个生成的是：final List<Todo> todos;

List.generate(20,(i) => Todo(
    'Todo $i',
    'A description of what needs to be done for Todo $i',
  ),
)

8.生成列表的方法：
ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(todos[index].title),
      onTap: () {
        Navigator.push(//跳转到另一个页面并把数据传出去
          context,
          MaterialPageRoute(//可以选择安卓或者苹果方式跳转
            builder: (context) => DetailScreen(todo: todos[index]),
          ),
        );
      },
    );
  },
)

9.点击按钮跳转页面并获取返回的值的写法：
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SelectionScreen()),
);
跳转的页面中：
Navigator.pop(context, ‘我是返回的值！’);
所以：
result=‘我是返回的值！’

10.转场效果是这样实现的：
GestureDetector(
  child: Hero(//是通过Hero这个widget来实现
    tag: 'imageHero',
    child: Image.network(
      'https://picsum.photos/250?image=9',
    ),
  ),
  onTap: () {
    Navigator.push(context, MaterialPageRoute(builder: (_) {
      return DetailScreen();
    }));
  },
)
—————
（跳转的另一个页面也点击返回实现转场效果）
GestureDetector(
  child: Center(
    child: Hero(
      tag: 'imageHero',
      child: Image.network(
        'https://picsum.photos/250?image=9',
      ),
    ),
  ),
  onTap: () {
    Navigator.pop(context);
  },
)
