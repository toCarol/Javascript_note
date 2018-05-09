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
2. ECMAScript5 新增了Array.isArray()方法用来确定某个值到底是不是数组，而不需要管它是在哪个全局执行环境中创建的。

### 转换方法
1. 调用数组的toString()方法会返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串。
2. 调用valueOf()返回的还是数组。

    var colors = ["red", "blue", "green"];
    alert(colors.toString());
    alert(colors.valueOf());
    alert(colors);

在以上的实例中，alert()会得到与直接调用toString()方法相同的结果。因为alert()要接收字符串参数，它会在后台调用toString()方法。
3. 调用toLocaleString()方法经常会返回与toString()和valueOf()方法相同的值。

>数组继承的toLocaleString()、toString()和valueOf()方法，在默认情况下都会以逗号分隔的字符串形式返回数组。而如果使用join()方法，则可以使用不同的分隔符来构建这个字符串。

    var colors = ["red", "green", "blue"];
    alert(colors.join(","));              //red,green,blue
    alert(colors.join("||"));             //red||green||blue

如果不给join()方法传入任何值，或者给它传入undefined,则使用逗号作为分隔符。

### 栈方法
>栈是一种LIFO(Last-In-First-Out,后进先出)的数据结构，也就是最新添加的项最早被移除。而栈中的插入(叫做推入)和移除(叫弹出)，只发生在一个位置——栈的顶部。
ECMAScript为数组专门提供了push()和pop()方法，以便实现类似栈的行为。
1. push()方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。

    var colors = new Array();
    var count = colors.push("red", "green");       //推入两项 
    alert(count);                                  //2

2. pop()方法从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。

    //接上
    var item = colors.pop();         //取得最后一项
    alert(item);                     //"black"
    alert(colors.length);            //1

### 队列方法
>队列数据结构的访问规则是FIFO(First-In-First-Out,先进先出)。队列在列表的末端添加项，从列表的前端移除项。 
1. shift()能够移除数组中的第一个项并返回该项，同时将数组长度减1.
结合使用shift()和push()方法，可以像使用队列一样使用数组。

    var colors = new Array();                  
    var count = colors.push("red", "green");    //推入两项
    alert(count);                      //2
    var item = colors.shift();         //取得第一项
    alert(item);                       //"red"
    alert(colors.length);              //1  

2. unshift() 在数组前端添加任意个项并返回新数组的长度。
同时使用unshift()方法和pop()方法，可以从相反的方向来模拟队列，即在数组的前端添加项，从数组末端移除项。

    var colors = new Array();
    var count = colors.unshift("red", "green");      //推入两项
    alert(count);                        //2
    ver item = colors.pop();             //取得最后一项
    alert(item);                         //green
    alert(colors.length);                //1

### 重排序方法
数组中存在两个可以直接用来重排序的方法：reverse()和sort().
1. reverse()方法会反转数组项的顺序。

    var values = [1, 2, 3, 4, 5];
    values.reverse();
    alert(values);            //5,4,3,2,1

2. sort()方法，在默认情况下。sort()方法按升序排列数组项——即最小的值位于最前面，最大的值排在最后面。
为了实现排序，sort()方法会调用每个数组项的toString()转型方法，然后比较得到的字符串，以确定如何排序。

    var values = [0, 1, 5, 10, 15];
    values.sort();
    alert(values);                  //0,1,10,15,5

上例中，在进行字符串比较时，“10”位于“5”的前面。
因此sort()方法可以接收一个比较函数作为参数，以便我们制定哪个值位于哪个值的前面。
比较函数接收两个参数，如果第一个参数应该位于第二个之后则返回一个正数。

    function compare(value1, values2) {
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            0;
        }
    }

这个比较函数可以适用于大多数数据类型，只要将其作为参数传递给sort()方法。

    var values = [0, 1, 5, 10, 15];
    values.sort(compare);
    alert(values);               //0,1,5,10,15

> 对于数值类型或者其valueOf()方法会返回数值类型的对象类型，可以使用一个更简单的比较函数。

    function compare(value1, value2){
        return value2 - value1;
    }

### 操作数组
ECMAScript为操作已经包含在数组中的项提供了很多方法。
1. concat()方法可以基于当前数组中的所有项创建一个新数组。它会先创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。

    var colors = ["red", "green", "blue"];
    var colors2 = colors.concat("yellow", ["black", "brown"]);
    alert(colors);        //red,green,blue
    alert(colors2);       //red,green,blue,yellow,black,brown

2. slice(),它能够基于当前数组中的一或多个项创建一个新数组，（slice()方法不会影响原始数组）。
在只有一个参数的情况下，slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。
如果有两个参数，该方法返回起始和结束位置之间的项————但不包括结束位置的项。

    var colors = ["red", "green", "blue", "yellow", "purple"];
    var colors2 = colors.slice(1);
    var colors3 = colors.slice(1,4);
    alert(colors2);               //green,blue,yellow,purple
    alert(colors3);               //green,blue,yellow

3. splice(),主要用途是向数组的中部插入项。
- 删除：可以删除任意数量的项，指定两个参数：要删除的第一项的位置和要删除的项数。
- 插入：可以向指定位置插入任意数量的项，指定3个参数：起始位置、0和要插入的项。
- 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，指定3个参数：起始位置、要删除的项数和要插入的任意数量的项。
注意：splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）。

    var colors = ["red", "green", "blue"];
    var removed = colors.splice(0, 1);  //删除第一项
    alert(colors);                      //green,blue
    alert(removed);                     //返回的是一个空数组

### 位置方法
ECMAScript5为数组实例添加了两个位置方法：indexOf()和lastIndexOf()
- 这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。
- indexOf方法从数组的开头（位置0）开始向后查找
- lastIndexOf()方法从数组的末尾开始向前查找
- 这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回-1
- 在比较第一个参数与数组中的每一项时，会使用全等操作。也就是说，要求查找的项必须严格相等。

    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    alert(numbers.indexOf(4));                    //3
    alert(numbers.indexOf(4, 4));                 //5

    var person = {name: "Nicholas"};
    var people = [{name: "Nicholas"}];
    var morePeople = [person];
    alert{people.indexOf(person)};                //-1
    alert(morePeople.indexOf(person));           //0

### 迭代方法
ECMAScript5为数组定义了5个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选）运行该函数的作用域对象————影响this的值。
传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。
- every():对数组中的每一项运行给定函数，如果该函数对每一项都返回true,则返回true.
- filter():对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组.
- forEach():对数组中的每一项运行给定函数，没有返回值.
- map():对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组.
- some():对数组中的每一项运行给定函数，如果该函数对任一项返回true,则返回true.

    var numbers = [1,2,3,4,5,4,3,2,1];
    var everyResult = number.every(function(item, index, array){
        return (item > 2);
    });
    alert(everyResult);             //false
    var someResult = numbers.some(function(item, index, array){
        return (item > 2);
    });
    alert(someResult);              //true

    var filterResult = numbers.filter(function(item, index, array){
        return (item > 2);
    });
    alert(filterResult);            //[3,4,5,4,3]

    var mapResult = numbers.map(function(item, index, array){
        return item * 2;
    });
    alert(mapResult);               //[2,4,6,8,10,8,6,4,2]

    numbers.forEach(function(item, index, array){
        //执行某些操作
    });