- 引用类型的值（对象）是引用类型的一个实例。
- 在ECMAScript中，引用类型是一种数据结构，用于将数据和功能组织在一起。
- 它也常被称为类，但这种称呼并不妥当。尽管ECMAScript从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。
- 引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

对象：
- 对象是某个特定引用类型的实例
- 新对象是使用new操作符后跟一个构造函数来创建的
- 构造函数本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的

## Object类型
目前为止，我们看到的大多数引用类型值都是Object类型的实例，Object对于在应用程序中存储和传输数据而言，是非常理想的选择。

创建Object的方式有两种：
1. 使用new操作符后跟Object构造函数

    ```javascript
    var person = new Object();
    person.name = "Nicholas";
    person.age = 29;
    ```

2. 使用对象字面量表示法(目的在于简化创建包含大量属性的对象的过程)

    ```javascript
    var person = {
        name: "Nicholas",
        age: 29
    };
    ```

在对象字面量中，使用逗号来分隔不同的属性。对象的最后一个属性后面不需要添加逗号。
>ECMAScript中的表达式上下文指的是能够返回一个值（表达式）。赋值操作符表示后面是一个值，所以左花括号在这里表示一个表达式的开始。同样的花括号如果在一个语句上下文中，例如跟在if语句后面，则表示一个语句块的开始。

使用对象字面量语法时，留空花括号，就可以定义只包含默认属性和方法的对象，如下所示：

    ```javascript
    var person = {};   //与new Object()相同
    person.name = "Nicholas";
    ```

开发人员更喜欢对象字面量语法，因为这种语法要求的代码量少，而且能够给人封装数据的感觉。实际上，对象字面量也是向函数传递大量可选参数的首选方式。

    ```javascript
    function displayInfo(args) {
        var output = "";
        if (typeof args.name == "string") {
            output += "Name: " + args.name + "\n"；
        }
        if (typeof args.age == "number") {
            output += "Age: " + args.age + "\n";
        }
        alert(output);
    }
    displayInfo({
        name: "Nicholas",
        age: 29
    });
    displayInfo({
        name: "Grey"
    });
    ```

访问对象属性的方法有两种：
1. 点表示法：通常，除非必须使用变量来访问属性，否则我们建议使用点表示法。
2. 方括号表示法：将要访问的属性以字符串的形式放在方括号内。
从功能上看，这两种方法没有任何区别，但方括号语法的主要优点是可以通过变量来访问属性。
>如果属性名中包含会导致语法错误的字符，或者属性名使用的是关键字或保留字，也可以使用方括号表示法。

    ```javascript
    person["first name"] = "Nicholas";
    ```



