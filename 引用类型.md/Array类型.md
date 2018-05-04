## Array类型
ECMAScript数组与其他语言中的数组：
相同点：都是数据的有序列表。
不同点：①ECMAScript数组的每一项可以保存任何类型的数据 ②ECMAScript数组的大小是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。

创建数组的基本方式有两种：
1. 使用Array构造函数
如果预先知道数组要保存的项目数量，也可以给构造函数传递该数量

    var colors = new Array(20);

也可以向Array构造函数传递数组中应该包含的项。

    var colors = new Array("red", "blue", "green");

在使用Array构造函数时也可以省略new操作符。

    var colors = Array(3);

2. 使用数组字面量表示法
数组字面量由一对包含数组项的方括号表示，多个数组项之间以逗号隔开。

    var colors = ["blue", "red", "green"];   //创建一个包含3个字符串的数组
    var names = [];                          //创建一个空数组
    var options = [,,,,,];                   //不要这样做！创建一个包含5或6项的数组，IE与其他浏览器表现不一致，因此不建议使用

>像上面这种省略值的情况下，每一项都将获得undefined值。

读取和设置数组的值：
- 要使用方括号并提供相应值的基于0的数字索引，方括号中的索引表示要访问的值。
- 如果索引小于数组中的项数，则返回对应项的值。
- 设置数组的值也采用相同的语法，但会替换指定位置的值。
- 如果设置某个值的索引超过了数组现有项数，数组就会自动增加到该索引值加1的长度。
- 如果将其length属性设置为大于数组项数的值，则新增的每一项都会取得undefined值。

    var colors = ["red", "blue", "green"];
    colors.length = 4;                     
    alert(colors[3]);                      //undefined

>每当在数组末尾添加一项后，其length属性都会自动更新以反应这一变化。

    var colors = ["red", "blue", "green"];
    colors[99] = "black";                     
    alert(colors.length);                     //100

上例中，位置3到98实际上都是不存在的。

### 检测数组
确定某个对象是不是数组：
1. 对于一个网页，或者一个全局作用域而言，使用instanceof操作符就可以得到满意的结果：

    if (value instanceof Array){
        //对数组执行某些操作
    }

instanceof操作符存在的问题：它假定只有一个全局环境，当网页中包含多个全局执行环境时，会存在多个不同版本的Array构造函数。
2. ECMAScript 5新增了Array.isArray()方法用来确定某个值到底是不是数组，而不需要管它是在哪个全局执行环境中创建的。





