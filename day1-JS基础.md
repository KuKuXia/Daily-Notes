day1 - JavaScript基础教程

[本书开源网址](https://wangdoc.com/javascript/)

[TOC]


# 入门



## JS是什么

轻量级的脚本语言。

本身不提供任何与输入输出相关的API。

**嵌入式**语言，宿主环境有浏览器和服务器等，也就是Node项目。

本身核心语法只能做简单数学和逻辑运算。包括两部分内容：**基本的语法构造和标准库**。除此之外，各种宿主环境提供额外的 API（即只能在该环境使用的接口），以便 JavaScript 调用。以浏览器为例，它提供的额外 API 可以分成三大类。
- **浏览器控制类**：操作浏览器
- **DOM 类**：操作网页的各种元素
- **Web 类**：实现互联网的各种功能



## 实验环境

工具：**Chrome浏览器**，Developer Tools里面的console，是运行Js的理想环境

使用：进入控制台以后，在提示符后输入代码，按`Enter`，执行代码，`Shift+Enter`



## 基本语法

注意：JavaScript 语言的标识符对大小写敏感。



#### 1. 语句

:pen:[语句](http://www.runoob.com/js/js-statements.html)是给浏览器发出的指令。

JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。
比如下面就是一行赋值语句。

```js
var a = 1 + 3；
```
这条语句先用`var`命令，声明了变量`a`，然后将`1 + 3`的运算结果赋值给变量`a`。`1 + 3`叫做表达式  （expression）。

语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内。

:pen:**[正则表达式](http://www.runoob.com/js/js-regexp.html)**

正则表达式（Regular Expression，简写regex、regexp或RE）。举例：正则表达式用于`search()`：
```
var str = "Visit Runoob!"; 
var n = str.search(/Runoob/i);
```
检索到与正则表达式种`Runoob`相匹配的子字符串，并返回子串的起始位置。`i`是一种修饰符，表示不区分大小写。正则表达式的语法结构就是`/正则表达式主体/修饰符(可选)`


#### 2. 变量

对变量二次赋值会覆盖掉之前的值。

先使用变量，后声明变量原则上是没有问题的。因为JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。



#### 3. 标识符

标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名。JavaScript 语言的标识符对大小写敏感，所以`a`和`A`是两个不同的标识符。

标识符命名规则如下：
- 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（`$`）和下划线（`_`）。
- 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字`0-9`。
- 保留字不能用作标识符，比如catch、if、enum等。
- 中文也可以做标识符。



#### 4. 注释

单行注释，用`//`起头；多行注释，放在`/*`和`*/`之间。

`<!--`和`-->`也被视为合法的单行注释。需要注意的是，-->只有在行首，才会被当成单行注释，否则会当作正常的运算。下面代码只有`x=1`被执行。

```javascript
x = 1; <!-- x = 2;
--> x = 3;
```



#### 5. 区块

```javascript
{
  var a = 1;
}
a 
```
JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

JavaScript 的区块不构成单独的作用域（scope）。



#### 6. 条件语句

**if语句**

```js
if (m === 3) {
  m += 1;
}
```
可以不用{}，但建议使用。

建议使用严格相等运算符符`===`，而不是相等运算符`==`。

```js
if (m !== 1) {
  if (n === 2) {
    console.log('hello');	
  }
} else {
  console.log('world');
}
```

**switch语句**

```js
switch (x) {
  case 1:
    console.log('x 等于1');
    break;
  case 2:
    console.log('x 等于2');
    break;
  default:
    console.log('x 等于其他值');
}
```
`break`必须有。

**三元运算符？：**

```js
var msg = '数字' + n + '是' + (n % 2 === 0 ? '偶数' : '奇数');
```



#### 7. 循环语句

**while循环**

```
var i = 0;

while (i < 100) {
  console.log('i 当前为：' + i);
  i = i + 1;
}
```
`while(true){}`无限循环

**for循环**

```
var x = 3;
for (var i = 0; i < x; i++) {
  console.log(i);
}
```
`for`语句的三个部分（initialize、test、increment），可以省略任何一个，也可以全部省略。

**do...while循环**

```js
var x = 3;
var i = 0;

do {
  console.log(i);
  i++;
} while(i < x);
```
不管条件是否为真，do...while循环至少运行一次，这是这种结构最大的特点。

**break语句和continue语句**

break`语句用于跳出代码块或循环。`continue`语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。

**标签**

标签相当于定位符，用于跳转到程序的任意位置。格式是`lable:语句`。

通常于`break`和`continue`	配合使用

```js
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
```
上面代码为一个双重循环区块，break命令后面加上了top标签（注意，top不用加引号），满足条件时，直接跳出双层循环。如果break语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。



# 数据类型


## 简介

#### JavaScript 语言有六种数据类型。

- 数值（number）：整数和小数（比如`1`和`3.14`）
- 字符串（string）：文本（比如`Hello World`）。
- 布尔值（boolean）：表示真伪的两个特殊值，即`true`（真）和`false`（假）
- `undefined`：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
- `null`：表示空值，即此处的值为空。
- 对象（object）：各种值组成的集合。

通常，数值、字符串、布尔值这三种类型，合称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于`undefined`和`null`，一般将它们看成两个特殊值。

对象是最复杂的数据类型，又可以分成三个子类型。
- 狭义的对象（object）
- 数组（array）
- 函数（function）

#### 判断某个数据是什么类型

Javascript有三种方法来判断数据的类型

- `typeof`运算符。`typeof 123`即返回`number`类型。注意，`typeof null`返回`object`类型。
- `instanceof`运算符
- `Object.prototype.toString`方法

## 布尔值

  `undefined` `null` `false` `0` `NaN` `""`或`''`（空字符串）会被转换为`false`，其他值都是`true`。

## 数值

`NaN`是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

`Infinity`表示“无穷”，用来表示两种场景。一种是一个正的数值太大，或一个负的数值太小，无法表示；另一种是非0数值除以0，得到`Infinity`。

几个全局方法：
1. `parseInt()`方法用于将字符串转为整数。
如果参数不是字符串，自动转换成字符串。结果只返回字符串头部可以转为数字的部分。
如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回NaN。
`parseInt`还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。默认情况下，parseInt的第二个参数为10，即默认是十进制转十进制。
2. `parseFloat()`方法用于将一个字符串转为浮点数。
3. `isNaN()`方法可以用来判断一个值是否为NaN。
4. `isFinite()`方法返回一个布尔值，表示某个值是否为正常的数值。  除了`Infinity`、`-Infinity`、`NaN`和`undefined`这几个值会返回`false`，`isFinite`对于其他的数值都会返回`true`。
5. 



# 控制台与console对象



## console对象

#### 静态方法

:one:**console.log()、console.info()、console.debug()、console.warn()、console.error()**

```js
console.log(' %s + %s = %s', 1, 1, 2)
```
上面代码中，`console.log`方法的第一个参数有三个占位符（`%s`），第二、三、四个参数会在显示时，依次替换掉这个三个占位符。

`console.log`方法支持以下占位符，不同类型的数据必须使用对应的占位符。

- `%s` 字符串
- `%d` 整数
- `%i` 整数
- `%f` 浮点数
- `%o` 对象的链接
- `%c` CSS 格式字符串

`console.info`是`console.log`方法的别名，用法完全一样。只不过`console.info`方法会在输出信息的前面，加上一个蓝色图标。

`console.debug`方法与`console.log`方法类似，会在控制台输出调试信息。但是，默认情况下，`console.debug`输出的信息不会显示，只有在打开显示级别在`verbose`的情况下，才会显示。

`warn`方法和`error`方法也是在控制台输出信息，它们与`log`方法的不同之处在于，`warn`方法输出信息时，在最前面加一个黄色三角，表示警告；`error`方法输出信息时，在最前面加一个红色的叉，表示出错。同时，还会高亮显示输出文字和错误发生的堆栈。其他方面都一样。

`console`对象的所有方法，都可以被覆盖。因此，可以按照自己的需要，定义`console.log`方法。

```javascript
['log', 'info', 'warn', 'error'].forEach(function(method) {
  console[method] = console[method].bind(
    console,
    new Date().toISOString()
  );
});

console.log("出错了！");
// 2014-05-18T09:00.000Z 出错了！
```

上面代码表示，使用自定义的`console.log`方法，可以在显示结果添加当前时间。

:two:**console.table()**

```
var languages = {
  csharp: { name: "C#", paradigm: "object-oriented" },
  fsharp: { name: "F#", paradigm: "functional" }
};

console.table(languages);
```

上面代码的`language`，转为表格显示如下。

| (index) | name | paradigm          |
| ------- | ---- | ----------------- |
| csharp  | "C#" | "object-oriented" |
| fsharp  | "F#" | "functional"      |

:three:**console.count()** 

`count`方法用于计数，输出它被调用了多少次。

** console.dir()，console.dirxml**

`dir`方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。
`dirxml`方法主要用于以目录树的形式，显示 DOM 节点。
如果参数不是 DOM 节点，而是普通的 JavaScript 对象，`console.dirxml`等同于`console.dir`。

:four:** console.assert()**

`console.assert`方法主要用于程序运行过程中，进行条件判断，如果不满足条件，就显示一个错误，但不会中断程序执行。这样就相当于提示用户，内部状态不正确。
第一个参数是表达式，表达式为`false`，才会提示第二个参数的错误信息。

```js
sole.assert(list.childNodes.length < 500, '节点个数大于等于500')
```

:five:**console.time(),console.timeEnd()**
`time`方法表示计时开始，`timeEnd`方法表示计时结束。它们的参数是计时器的名称。调用`timeEnd`方法之后，控制台会显示“计时器名称: 所耗费的时间”。

:six:**console.group()，console.groupEnd()，console.groupCollapsed()**

`console.group`和`console.groupEnd`这两个方法用于将显示的信息分组。它只在输出大量信息时有用，分在一组的信息，可以用鼠标折叠/展开。

```js
console.group('一级分组');
console.log('一级分组的内容');

console.group('二级分组');
console.log('二级分组的内容');

console.groupEnd(); // 二级分组结束
console.groupEnd(); // 一级分组结束
```

上面代码会将“二级分组”显示在“一级分组”内部，并且“一级分组”和“二级分组”前面都有一个折叠符号，可以用来折叠本级的内容。

`console.groupCollapsed`方法与`console.group`方法很类似，唯一的区别是该组的内容，在第一次显示时是收起的（collapsed），而不是展开的。

:seven:**console.trace()，console.clear()**

`console.trace`方法显示当前执行的代码在堆栈中的调用路径。

```
console.trace()
// console.trace()
//   (anonymous function)
//   InjectedScript._evaluateOn
//   InjectedScript._evaluateAndWrap
//   InjectedScript.evaluate
```

`console.clear`方法用于清除当前控制台的所有输出，将光标回置到第一行。如果用户选中了控制台的“Preserve log”选项，`console.clear`方法将不起作用。



## 控制台命令行 API

浏览器控制台中，除了使用`console`对象，还可以使用一些控制台自带的命令行方法。

:one:`$_`

`$_`属性返回上一个表达式的值。

```js
2 + 2
// 4
$_
// 4
```

:two:`$0` - `$4`

控制台保存了最近5个在 Elements 面板选中的 DOM 元素，`$0`代表倒数第一个（最近一个），`$1`代表倒数第二个，以此类推直到`$4`。

:three:`$(selector)`

`$(selector)`返回第一个匹配的元素，等同于`document.querySelector()`。注意，如果页面脚本对`$`有定义，则会覆盖原始的定义。比如，页面里面有 jQuery，控制台执行`$(selector)`就会采用 jQuery 的实现，返回一个数组。

:four:`$$(selector)`

`$$(selector)`返回选中的 DOM 对象，等同于`document.querySelectorAll`。

:five:`$x(path)`

`$x(path)`方法返回一个数组，包含匹配特定 XPath 表达式的所有 DOM 元素。

```js
$x("//p[a]")
```

上面代码返回所有包含`a`元素的`p`元素。

:six:`inspect(object)`

`inspect(object)`方法打开相关面板，并选中相应的元素，显示它的细节。DOM 元素在`Elements`面板中显示，比如`inspect(document)`会在 Elements 面板显示`document`元素。JavaScript 对象在控制台面板`Profiles`面板中显示，比如`inspect(window)`。

:seven:`getEventListeners(object)`

`getEventListeners(object)`方法返回一个对象，该对象的成员为`object`登记了回调函数的各种事件（比如`click`或`keydown`），每个事件对应一个数组，数组的成员为该事件的回调函数。

:eight:`keys(object)`，`values(object)`

`keys(object)`方法返回一个数组，包含`object`的所有键名。

`values(object)`方法返回一个数组，包含`object`的所有键值。

```js
var o = {'p1': 'a', 'p2': 'b'};

keys(o)
// ["p1", "p2"]
values(o)
// ["a", "b"]
```

:nine:`monitorEvents(object[, events]) ，unmonitorEvents(object[, events])`

`monitorEvents(object[, events])`方法监听特定对象上发生的特定事件。事件发生时，会返回一个`Event`对象，包含该事件的相关信息。`unmonitorEvents`方法用于停止监听。

```js
monitorEvents(window, "resize");
monitorEvents(window, ["resize", "scroll"])
```

上面代码分别表示单个事件和多个事件的监听方法。

```js
monitorEvents($0, 'mouse');
unmonitorEvents($0, 'mousemove');
```

上面代码表示如何停止监听。

`monitorEvents`允许监听同一大类的事件。所有事件可以分成四个大类。

- mouse："mousedown", "mouseup", "click", "dblclick", "mousemove", "mouseover", "mouseout", "mousewheel"
- key："keydown", "keyup", "keypress", "textInput"
- touch："touchstart", "touchmove", "touchend", "touchcancel"
- control："resize", "scroll", "zoom", "focus", "blur", "select", "change", "submit", "reset"

```js
monitorEvents($("#msg"), "key");
```

上面代码表示监听所有`key`大类的事件。

（10）其他方法

命令行 API 还提供以下方法。

- `clear()`：清除控制台的历史。
- `copy(object)`：复制特定 DOM 元素到剪贴板。
- `dir(object)`：显示特定对象的所有属性，是`console.dir`方法的别名。
- `dirxml(object)`：显示特定对象的 XML 形式，是`console.dirxml`方法的别名。



## debugger 语句

`debugger`语句主要用于除错，作用是设置断点。如果有正在运行的除错工具，程序运行到`debugger`语句时会自动停下。如果没有除错工具，`debugger`语句不会产生任何结果，JavaScript 引擎自动跳过这一句。

Chrome 浏览器中，当代码运行到`debugger`语句时，就会暂停运行，自动打开脚本源码界面。

```js
for(var i = 0; i < 5; i++){
  console.log(i);
  if (i === 2) debugger;
}
```

上面代码打印出0，1，2以后，就会暂停，自动打开源码界面，等待进一步处理。