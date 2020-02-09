# -javaScript
快速学习javascript看这个就够了
#  第1章	在HTML中使用Javascript

## 1.1  script元素

在使用<script>元素嵌入JavaScript代码时，只须像下面这样把代码直接放在元素内部即可：

```  javascript
<script>
	function sayHi() {
    	alert("Hi!")
	}    
</script>
```

如果通过<script>元素来包含外部JavaScript文件，那么src属性就是必须的。这个属性的值是一个指向外部JavaScript文件的连接，例如：

``` javascript
<script src="example.js"></script>
```

注意：引入外部文件.js扩展名不是必须的，因为浏览器不会检查JavaScript文件的扩展名。但是服务器通常还需要看扩展名来决定响应哪种MIME类型。如果不适应 .js扩展名，请确保服务器能返回正确的MIME类型。

另外，通过<script>元素的src属性还可以包含来自外部域的JavaScript文件。

 ### 1.1.1  标签位置

按照传统做法，放在html文件的<head>元素中，例如：

``` javascript
<!DOCTYPE html>
<html>
	<head>
    	<script src="example.js"></script>
    </head>
	<body>
        <!-- 这里放内容 -->
    </body>
</html>
```

在<head>元素种引入js文件，会导致页面呈现延迟展示一片空白。为了避免这个问题，现代Web应用程序一般把全部JavaScript引用放在 <body>元素种页面内容的后面，例如：

``` javascript
<!DOCTYPE html>
<html>
	<head>    	
    </head>
	<body>
        <!-- 这里放内容 -->
    	<script src="example.js"></script>
    </body>
</html>
```

这样在解析JavaScript之前，页面内容将完全呈现在浏览器种。

### 1.1.2  延迟脚本

HTML4.0.1为<script>标签定义了defer属性。表明脚本执行时不会影响页面构造。相当于告诉浏览器立即下载，但延迟执行。

```javascript
<!DOCTYPE html>
<html>
	<head>
    	<script src="example.js" defer="defer"></script>
    </head>
	<body>
        <!-- 这里放内容 -->
    </body>
</html>
```

但是延迟脚本不会按一定顺序执行，因此最好只包含一个延迟脚本。

在HTML5规范种，脚本要按照出现的先后顺序执行，因此会忽略defer这一属性。

### 1.1.3  异步脚本

HTML5为<script>元素定义了 async 属性。这个属性告诉浏览器立即下载，但不保证执行先后顺序，所以在使用此属性时要确保不同的脚本之间没有相互依赖。

## 1.2  嵌入代码与外部文件

在HTML中嵌入JavaScript代码虽然没有问题，但是尽可能引入外部文件。有点如下：

- 可维护性：
  - 把所以的JavaScript文件都放在一个文件夹中，维护起来轻松，而且开发人员可在不触及HTML的情况下，集中经理编辑JavaScript代码。
- 可缓存：
  - 浏览器能够根据具体的设置缓存所有外部JavaScript文件。

## 1.3  noscript元素

早期浏览器有的不支持JavaScript，为了平稳退化创造了<noscript>元素，在<noscript>元素中的内容只有在下列情况下才会显示出来：

- 浏览器不支持脚本；
- 浏览器支持脚本，但脚本被禁用；

``` javascript
<html>
    <head>
    </head>
	<body>
    	<noscript>
    		<p>本页面需要浏览器支持（启用）JavaScript。</p>
    	</noscript>
    </body>
</html>
```



#  第2章	基本概念

## 2.1  语法

### 2.1.1  区分大小写

在JavaScript中的一切变量、函数名和操作符都区分大小写。变量名test和Test表示两个不同的变量，函数名不能使用typeof，因为它是一个关键字，但typeOf是一个有效的函数名。

### 2.1.2  标识符

所谓的标识符，就是指变量、函数、属性的名字，或者函数的参数。可按下列规则组合

- 第一个字符必须是一个字母、下划线（_）、或者一个美元符号（$）;
- 其他字符可以是字母、下划线、美元符号或数字。

按照惯例，JavaScript标识符采用驼峰大小写格式，也就是第一个字母小写，剩下的每个单子的首字母大写。

例如：myCar

### 2.1.3  注释

注释包括单行注释和多行注释。单行注释以两个斜杠开头、块级注释以一个斜杠和一个星号开头（/*），以一个星号和一个斜杠（*/）结尾

```javascript
// 单行注释
/*
*多行注释
*
*/
```

### 2.1.4  严格模式

在严格模式下一些不确定行为将得到处理，而且对某些不安全的操作会抛出错误。要在整个脚本中启用严格模式，可在顶部添加如下代码：

``` javascript
"use strict";
```

也可以指定函数在严格模式下执行：

``` javascript
function doSomething() {
    "use strict";
    // 函数体
}
```

### 2.1.5  语句

Javascript语句以分号结尾；如果省略分号，则由解析器确定语句的结尾。

```javascript
var sum = a + b 	//有效不推荐
var diff = a - b;    //有效推荐
```

加上分号也会在某些情况下增进代码的性能，因为这样解析器就不必在花时间推测应该在哪里插入分号了。

可以把多条语句放到一个组合代码块中，即在{}中

```javascript
if (test) {
    test = false;
    alert(test);
}
```



## 2.2  关键字和保留字

JavaScript描述了一组特定用途的关键字，和保留字。这些字不能用做变量或者函数名。

## 2.3  变量 

JavaScript的变量是松散类型的，所谓的松散类型就是可以用来保存任何类型的数据。换句话说就是每个变量仅仅是一个用于保存值的占位符而已。

```javascript
var message;
```

这行代码定义了一个名为message的变量，该变量可以保存任何值，为经过初始化的会保存一个特殊的值undefined。

```javascript
var message = "hi";
message = 100; //有效 不推荐
```

上面的代码提现了一个变量可以保存为不同的数据类型，但是不推荐。

用var操作符定义的变量会成为定义该变量的作用域中的局部变量。也就是说，如果在函数中使用var定义一个变量，那么这个变量在函数退出后就会被销毁，例如：

```javascript
function test() {
    var message = "hi"; // 局部变量
}

test();
alert(message); // 错误!
```

如果不用var定义变量，将会被保存为全局变量，例如：

```javascript
function test() {
    message = "hi";  // 全局变量  不推荐
}
test();
alert(message);  // "hi"
```

可以用一条语句定义多个变量，用逗号分隔

```javascript
var message = 'hi',
    found = false,
    age =  =29;
```



## 2.4  数据类型

JavaScript有5中简单数据类型，也称基本数据类型：

- Undefined
- Null
- Boolean
- Number
- String

还有一种复杂数据类型：

- Object

### 2.4.1  typeof 操作符

typeof 是用来检测变量的数据类型，可能返回下列某个字符串：

- undefined——如果这个值未定义；
- boolean——如果这个值是布尔值；
- string——如果这个值是字符串；
- number——如果这个值是数值；
- object——如果中国值是对象或者null；
- function——如果中国值是函数；

例如：

```javascript
var message = "some string";
alert(typeof message); // 'string'
```

### 2.4.2  undefined类型

```javascript
var message;
alert(message == undefined); // true;
```

```javascript
var message = undefined;
alert(message == undefined); //true;
alert(typeof message); // undefined;
```

### 2.4.3  null类型

null值表示一个空对象指针

```javascript
var car = null;
alert(typeof car); // "object"
```

注意null和undefined用（==）操作符比较会返回true

```javascript
alert(null == undefined); // true
```

### 2.4.4  boolean类型

| 数据类型  | 转换为true的值 | 转换为false的值 |
| --------- | -------------- | --------------- |
| Boolean   | true           | false           |
| String    | 任何非空字符串 | “"(空字符串)    |
| Number    | 任何非0数字值  | 0和NaN          |
| Object    | 任何对象       | null            |
| Undefined |                | undefined       |

### 2.4.5  Number类型

 ```javascript
var intNum = 55;  // 10进制整数
var num1 = 070;   // 8进制的56
var num2 = 079;   // 无效的8进制——解析为79
var num3 = 08;    // 无效的8进制——解析为8

var num4 = 0xA;   // 16进制的10
var num5 = 0x1f;  // 16进制的31
 ```

 #### 1.浮点数值

所谓的浮点数值，就是该数值中包含一个小数点，并且小数点后面必须至少有一位数字，小数点前可以没有数值，但是不推荐。

```javascript
var floatNum1 = 1.1;
var floatNum2 = 0.1;
var floatNum3 = .1;  // 有效但不推荐
```

``` javascript
var floatNum1 = 1.;		  // 小数点后没有数字——解析为1
var floatNum2 = 10.0;	  // 整数——解析为10
var floatNum = 3.125e7;   // 等于31250000
```

浮点数的最高精度是17位小数，但在进行算数计算时其精确度远远不如整数。例如，0.1加0.2的结果不是0.3，而是0.30000000000000004。

````javascript
if(a + b == 0.3){	// 不要这样做 
    alert("You got 0.3")
}
````

#### 2.数值范围

JavaScript最小的数值保存在Number.MIN_VALUE中，这个值时5e-324.最大值保存在Number.MAX_VALUE中。如果计算结果超过数值范围，那么这个值将自动转换位Infinity值。如果时负的将转换位-Infinity。

判断是不是在数值范围内可用isFinite();

```javascript
var result = Number.MAX_VALUE + Number.MAX_VALUE;
alert(isFinite(result)); // false;
```

#### 3.NaN

NaN,即非数值，用于表示一个本来要返回数值的操作数未返回数值的情况。

NaN有两个特点

- 任何涉及NaN的操作都会返回NaN
- NaN与任何值都不相等，包括NaN本身。

``` javascript
alert(NaN == NaN);  // false;
```

#### 4.数值转换

有3个函数可以把非数值转换位数值：Number(),parseInt(),parseFloat().

Number()转换规则

- 如果时Boolean，true和false分别转换为1和0；
- 如果时数字，只是简单第传入和返回
- 如果是null，返回0；
- 如果是undefined，返回NaN
- 如果时字符串遵循下列规则：
  - 如果字符串中只包含数字，则将其转换为十进制数值。
  - 如果字符串中包含有效的浮点格式，则转换为浮点数值
  - 如果字符串中包含有效的十六进制格式，则将其转换为相同大小的十进制整数值
  - 如果字符串是空的，则将其转换为0；
  - 如果字符串中包含除上述格式之外的字符，则将其转换为NaN
- 如果是对象，则调用对象的valueOf（）方法，然后依照前面的规则转换返回值，如果转换的结果是NaN，则调用对象的toString（）方法，然后在按照规则进行转换。

parseInt()

- 他会忽略字符串前的空格，直至找到第一个非空格字符。
- 如果第一个字符不是数字字符或者负号，返回NaN
- 空字符串返回NaN
- 如果第一个字符是数字，会解析到第一个不是数字的字符位置，小数点不是有效数字字符

```javascript
var num1 = parseInt("1234blue");  // 1234
var num2 = parseInt("");          // NaN
var num3 = parseInt("0xA");       // 10(十六进制)
var num4 = parseInt(22.5)         // 22
var num5 = parseInt("070");       // 56(八进制)
var num6 = parseInt("70");        // 70(十进制)
var num7 = parseInt("0xf");       // 15(十六进制)
```

注意：在es6中parseInt不具备解析八进制的能力

```javascript
var num = parseInt("070")
alert(num)   // 70  在es6中
```

为消除上述问题parseInt接受第二个参数

```javascript
var num1 = parseInt("AF",16);   // 175
var num2 = parseInt("10",2);    // 2
var num3 = parseInt('10',8);    // 8
var num4 = parseInt('10',16);   // 16
```

parseFloat()

- 从第一个字符开始直到遇到无效的字符为止。
- 第一个小数点有效，第二个无效。
- 只解析十进制，所以没有第二个参数。

### 2.4.6  String类型

字符串可以由单引号或双引号表示

#### 字符字面量

| 字面量 | 含义                              |
| ------ | --------------------------------- |
| \n     | 换行                              |
| \t     | 制表                              |
| \b     | 退格                              |
| \r     | 回车                              |
| \f     | 进纸                              |
| \\  \  | 斜杠                              |
| \ '    | 单引号                            |
| \ "    | 双引号                            |
| \xnn   | 以十六进制nn表示一个字符          |
| \unnnn | 以十六进制nnnn表示一个Unicode字符 |

#### 字符串特点

字符串一旦创建，他的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后在用另一个包含新值的字符串填充该变量。

```javascript
var lang = "Java";
lang = lang + "Script";
```

#### 转换为字符串

```javascript
var age = 11;
var ageAsString = age.toString();   // "11"
var found = true;
var foundAsString = found.toString(); // "true"
```

数值、布尔值、对象和字符串都有toString()方法，但null和undefined没有这个方法。数值调用该方法时可以传一个参数输出数值的基数。

```javascript
var num = 10;
alert(num.toString());   // "10"
alert(num.toString(2));  // "1010"
alert(num.toString(8));  // "12"
alert(num.toString(10)); // "10"
alert(num.toString(16)); // "16"
```

在不知道转换的值是不是null和undefined的情况下，可以用String（）,这个函数可以将审核类型转换为字符串。

- 如果值由toString()方法，则调用该方法并返回值
- 如果时null，返回"null"
- 如果时undefined，返回"undefined"

### 2.4.7  Object 类型

```javascript
var o = new Object();   // 创建新对象
var o1 = new Object;    // 有效不推荐
```

Object的每个实例都具有下列属性和方法

- constructor:保存着用于创建当前对象的函数，即构造函数
- hasOwnProperty(propertyName)：用于检查给定的属性在当前的实例中是否存在，其中参数必须以字符串的形式指定。
- isPrototypeOf(object):用于检查传入的对象是否是当前对象的原型
- propertyIsEnumerable(propertyName):用于检测给定的属性是否可以枚举。
- toLocalString():返回对象的字符串表示
- toString():返回对象的字符串表示
- valueOf():返回对象的字符串，通常与toString()方法返回的值相同

## 2.5  操作符

### 2.5.1  一元操作符

只能操作一个值的操作符叫一元操作符

#### 递增和递减操作符

```javascript
var age = 29;
alert(++age);   // 30
alert(age++);   // 30
alert(age);     // 31
```

```javascript
var age = 29;
alert(--age);  // 28
alert(age--);  // 28
alert(age):    // 27
```

#### 一元加和减操作符

```javascript
var num = 25;
num = +num    // 25
num = -num    // -25
```

### 2.5.2  位操作符

JavaScript中所以数值都以64位存储，但位操作符不直接操作64位的值，而是先把64位转换位32位的整数，然后执行操作，由于64位的存储格式时透明的，因此整个过程就像只存在于32位整数一样。

32位中，前31位表示值。第32位表示数值的符号：0表示正式，1表示负数。整个表示符号的位叫符号位。

注意：NaN和Infinity进行位操作时，都被当成0来处理

#### 按位非

按位非操作用波浪线（~）表示

```javascript
var num1 = 25;
var num2 = ~num1;
alert(num2);      // -26
```

相当于

```javascript
var num1 = 25;
var num2 = -num1 - 1;
alert(num2);     // 26
```

#### 按位与

按位与的操作符用和字符（&）表示

| 第一个数值的位 | 第二个数值的位 | 结果 |
| -------------- | -------------- | ---- |
| 1              | 1              | 1    |
| 1              | 0              | 0    |
| 0              | 1              | 0    |
| 0              | 0              | 0    |

#### 按位或

按位或操作符用一个竖线符号（|）表示

| 第一个数值的位 | 第二个数值的位 | 结果 |
| -------------- | -------------- | ---- |
| 1              | 1              | 1    |
| 1              | 0              | 1    |
| 0              | 1              | 1    |
| 0              | 0              | 0    |

#### 按位异或

按位异或由一个插入符号（^）表示

| 第一个数值的位 | 第二个数值的位 | 结果 |
| -------------- | -------------- | ---- |
| 1              | 1              | 0    |
| 1              | 0              | 1    |
| 0              | 1              | 1    |
| 0              | 0              | 0    |

#### 左移

左移操作符由两个小于号（<<）表示

```javascript
var oldValue = 2;
var newValue = oldValue<<5;    //2乘以2的5次方
```

### 2.5.3  布尔操作符

#### 逻辑非   

逻辑非操作由一个叹号（!）表示

```javascript
alert(!false);   // true
```

#### 逻辑与

逻辑与由两个和号（&&）表示

| 第一个操作 | 第二个操作 | 结果  |
| ---------- | ---------- | ----- |
| true       | true       | true  |
| true       | false      | false |
| false      | true       | false |
| false      | false      | false |

```javascript
var a = true && 1;
alert(a);    // 1;
```

```javascript
var a = false && 1;
alert(a);    // false
```

#### 逻辑或

逻辑或操作符由两个竖线（||）表示

| 第一个操作 | 第二个操作 | 结果  |
| ---------- | ---------- | ----- |
| true       | true       | true  |
| true       | false      | true  |
| false      | true       | true  |
| false      | false      | false |

```javascript
var found = true;
var result = found || someUndefinedVariable;   // 不会发生错误
alert(result);  //  会执行true
```

```javascript
var found = false;
var result = found || someUndefinedVariable;   // 会发生错误
alert(result);  //  不会执行
```

### 2.5.4  乘性操作符

乘性操作符：乘法、除法和求模

#### 乘法

```javascript
var result = 34*56
```

#### 除法

``` javascript
var result = 66/11
```

#### 求模

```javascript
var result = 26%5
```

- 操作数如果有NaN，则返回NaN
- 如果操作数不是数值，则调用Number（）进行转换

### 2.5.5  加性操作符

加性操作符：加法、减法

#### 加法

```javascript
var result = 1+2
```

- 如果有一个操作数是NaN，结果是NaN
- 如果两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来
- 如果只有一个操作数是字符串，则将另一个操作数转换为字符串，然后在将两个字符串拼接起来。

#### 减法

```javascript
var result = 2-1
```

- 如果有一个操作数是NaN，则返回NaN

### 2.5.6  关系操作符

关系操作符包括小于（<）,大于（>）, 小于等于（<=），大于等于（>=）

```javascript
var result1 = 5 > 3;     // true
var result2 = 5< 3;      // false
```

- 如果两个操作数都是数值，则执行数值比较。
- 如果两个操作数都是字符串，则比较两个字符串对应的字符编码值。
- 如果一个是数值，则将另一个操作数转换为一个数值，然后进行数值比较。
- 如果一个操作数是对象，则调用这个对象的valueOf（）方法，用得到的结果按照前面的规则执行比较。如果对象没有valueOf（），则调用toString()方法，并用得到的结果按照前面的规则进行比较。
- 如果操作数是布尔值，则先将其转换为数值，然后在执行比较。

### 2.5.7  相等操作符

#### 相等和不等

相等操作符由（==）表示，不等操作符由（!=）表示

在转换不同的数据类型时，相等和不等遵循下列基本规则：

- 如果有一个操作数时布尔值，则在比较相等性之前先将其转换为 数值——false转换为0，而true转换为1；
- 如果第一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值。
- 如果第一个操作数是对象，另一个不是，则调用对象的valueOf()方法，用得到的基本类型进行比较。
- null和undefined是相等的。
- 要比较相等性之前，不能将null和undefined转换成其他任何值。
- 如果有一个操作数是NaN，则相等操作符返回false，而不等操作符返回true。如果两个都是NaN，则返回false
- 如果两个操作数都是对象，则比较他们是不是同一个对象。如果两个操作数都指向同一个对象，则相等操作符返回true，否则返回false

#### 全等和不全等

全等由（===）表示，不全等由（!==）表示

```javascript
var result1 = ("55" == 55);    // true
var result2 = ("55" === 55);   // false

var result3 = ("55" != 55);    // false
var result4 = ("55" !== 55);   // true

var result5 = (null === undefined)   // false
```

### 2.5.8  条件操作符

```javascript
var num1 = 2;
var num2 = 3;
var max = (num2>num1)?num2:num1;    // 3
```

### 2.5.9  复制操作符

赋值操作符如下所示：

- 乘/赋值(*=)
- 除/赋值(/=)
- 模/赋值(%=)
- 加/赋值(+=)
- 减/赋值(-=)
- 左移/赋值(<<=)
- 有符号右移/赋值(>>=)

### 2.5.10  逗号操作符

```javascript
var num1 = 1, num2 = 2,num3 = 3;

var num = (5,3,2,6);   // 6
```

逗号操作符可以用于赋值，再用于赋值时逗号操作符总会返回表达式中最后一项。

## 2.6  语句

### 2.6.1  if语句

```javascript
if (i>25) {
    alert("Greater than 25.")
}else if (i<0){
    alert("Less than 0")
}else {
    alert("Between 0 and 25,inclusive")
}
```

### 2.6.2  do-while语句

```javascript
do {
    statement
} while (expression)
```

### 2.6.3  while语句

```javascript
while (expression) {
    statement
}
```

### 2.6.4  for语句

```javascript
for (initialization;expression;post-loop-expression) {
    statement;
}
```

### 2.6.5  for-in语句

```javascript
for(property in expression) {
    statement;
}
```

### 2.6.6  label语句

label：statement

```javascript
start:for (var i=0; i < count;i++) {
    alert(i);
}
```

start标签将来由break或continue语句引用。加标签的语句一般都要与for语句等循环语句配合使用。

### 2.6.7  break和continue语句

break语句立即退出循环，强制执行循环后面的语句。而continue语句虽然也是立即退出循环，但会退出循环后会从循环的顶部继续执行。

```javascript
var num = 0;
for(var i=1;i<10;i++) {
    if(i%5) {
        break;
    }
    num ++;
}
alert(num);    // 4
```

```javascript
var num = 0;
for (var i = 1;i<10;i++) {
    if(i%5 == 0){
        continue;
    }
}
alert(num)  //  8
```

```javascript
var num = 0;
outermost:for(var i=0;i<10;i++){
    for(var j=0;j<10;j++){
        if(i==5 && j == 5) {
            break outermost;
        }
        num ++;
    }
}

alert(num);   // 55
```

```javascript
var num = 0;
outermost:for(var i=0;i<10;i++){
    for(var j=0;j<10;j++){
        if(i==5 && j == 5) {
            continue outermost;
        }
        num ++;
    }
}

alert(num);   // 55
```

### 2.6.8  with语句

with语句的作用时将代码的作用域设置到一个特定对象中。

```javascript
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;
```

上面几行代码都包含location对象，如果使用width语句，可以把上面的代码改成如下所示：

```javascript
with(location) {
    var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
}
```

```j
注意：由于大量使用with语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用with语句
```

### 2.6.9  switch语句

```javascript
switch(expression) {
    case value:statement
    break;
    case value:statement
    break;
    default:statement
}
```

```j
注意:switch语句在比较值时使用的时全等操作符，因此不会发生类型转换
```

## 2.7  函数

在javaScript中函数使用function关键字来声明，后跟一组参数及函数体

```javascript
function functionName(arg0,arg1,...,argN) {
    statements
}
```

```javascript
function sayHi(name,message) {
    alert("Hello " + name + "," + message)
}

sayHi("XiaoMing","how are you");    // Hello xiaoMing,how are you
```

函数体中有return语句，遇到return后停止并立即退出，因此位于return后的代码永远都不会执行。

### 2.7.1理解参数

javaScript中不介意来多少个参数，也不在乎时什么类型，原因时参数在内部使用一个数组来表示的。在函数体内可以用arguments对象来范围这个参数数组，从而获取传递给函数的每一个函数。

arguments对象只是与数组类似并不是Array的实例，因此可以用方括号访问它的每一个元素，用length属性表示传递进来的个数

```javascript
function functionName(){
    alert("Hello " + arguments[0] + "," + arguments[1]);
}

functionName("XiaoMing","how are you");   // Hello XiaoMing,how are you
```

#  第3章	变量、作用域、内存问题

## 3.1  基本类型和引用类型的值

## 3.2  执行环境及作用域

## 3.3  垃圾收集 

#  第4章	引用类型

## 4.1  Object类型

## 4.2  Array类型

## 4.3  Date类型

## 4.4  RegExp类型

## 4.5  Function类型

## 4.6  基本包装类型

## 4.7  单体内置对象



#  第5章	面向对象的程序设计

## 5.1  理解对象

## 5.2  创建对象

## 5.3  继承



#  第6章	函数表达式

## 6.1  递归

##  6.2  闭包

##  6.3  模仿块级作用域

## 6.4  私有变量



# 第7章	BOM

## 7.1  window对象

## 7.2  location对象

## 7.3  navigator对象

## 7.4  screen对象

## 7.5 history对象



#  第8章	客户端检测

## 8.1  能力检测

## 8.2  怪癖检测

## 8.3  用户代理检测



#  第9章	DOM

## 9.1  节点层次

## 9.2  DOM操作技术



#  第10章	DOM扩展

## 10.1  选择符API

## 10.2  元素遍历

## 10.3  HTML5

## 10.4  专有扩展



# 第11章	DOM2和DOM3

## 11.1  DOM变化

## 11.2  样式

## 11.3  遍历

## 11.4  范围



#  第12章	事件

## 12.1  事件流

## 12.2  事件处理程序

## 12.3  事件对象

## 12.4  事件类型

## 12.5  内存和性能

## 12.6  模拟事件



# 第13章	表单脚本

##  13.1  表单的基础知识

## 13.2  文本框脚本

## 13.3  选择框脚本

## 13.4  表单序列化

## 13.5  富文本编辑



# 第14章	使用Canvas绘图

## 14.1  基本用法

## 14.2  2D上下文

## 14.3  WebGL



# 第15章	HTML5脚本编程

## 15.1  跨文档消息传递

## 15.2  原生拖放

## 15.3  媒体元素

## 15.4  历史状态管理



# 第16章	错误处理与调试

## 16.1 浏览器报告的错误

## 16.2  错误处理

## 16.3  调试技术

## 16.4  常见的IE错误



# 第17章	Javascript与XML

## 17.1  浏览器对XML和DOM的支持

## 17.2  浏览器对XPath的支持

## 17.3  浏览器对XSLT的支持



# 第18章	E4X

## 18.1  E4X的类型

## 18.2  一般用法

## 18.3  其他变化



# 第19章	JSON

## 19.1  语法

## 19.2  解析与序列化



# 第20章	Ajax 与 Comet

## 20.1  XMLHttpRequest对象

## 20.2  XMLHttpRepuest 2 级

## 20.3 进度事件

## 20.4  跨域资源共享

## 20.5  其他跨域技术

## 20.6  安全



# 第21章	高级技巧

## 20.1  高级函数

## 20.2  防篡改对象

## 20.3  高级定时器

## 20.4  自定义事件

## 20.5  拖放



# 第22章	离线应用与客户端存储

## 22.1  离线检测

## 22.2  应用缓存

## 22.3  数据存储

 

# 第23章	最佳实践

## 23.1  可维护性

## 23.2  性能

## 23.3  部署



# 第24章	新兴API

## 24.1 request Animation Frame（）

## 24.2  Page Visibility API

## 24.3  Geolocation API

## 24.4  File API

## 24.5 Web计时

## 24.6 Web Workers





