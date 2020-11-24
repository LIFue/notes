# JavaScript学习笔记

## 第一章

### 1. 原始值和对象

- 原始值：包括布尔值、数字、字符串、null和undefined。
- 对象：其他的值都是对象。

原始值与对象之间的差别在于他们的比较方式;每个对象都有唯一的标识且只能等于自己。原始值只要编码值相同，就被认为相等。JavaScript中等于号为`===`，赋值号为`=`。

1. 原始值

    原始值也能有属性，如字符串的length属性，但是原始值的属性不能被改变，且不能添加新属性。

2. 对象

    - 简单对象：可以通过对象字面量来创建。即给对象的属性赋值，也可以创建一个空对象，可以将创建的对象赋值给一个变量。

        ```javascript
        {
            firstName:"Jane",
            lastName:"Doe"
        }
        ```

    - 数组：可以通过数组字面量来创建

        ```javascript
        ['apple', 'banana', 'cherry']
        ```

    - 正则表达式

        ```javascript
        /^a+b+$/
        ```

3. undefined 和 null

- undefined:意为“没有值”。

  - 未被初始化的变量为undefined。

  - 丢失的参数也会是undefined：

    ```javascript
    > function f(x){return x}
    > f()
    undefined
    ```
  
  - 访问不存在的属性，也会得到undefined。

- null的意思是“没有对象”。在用到对象的时候它表示空值。

undefined和null没有任何属性。

### 2. 使用typeof和instanceof对值分类

typeof主要用于原始值，instanceof主要用于对象。

```javascript
typeof value
```

返回值为一个表示这个值“类型”的字符串。

typeof会得到的所有结果：

|操作数|结果|
|:----|----|
|undefined|'undefined'|
|null|object|
|布尔值|boolean|
|数字|number|
|字符串|string|
|函数|function|
|所有其他的常规值|object|
|引擎创建的值|JavaScript引擎可以被允许去创建一些值，且typeof的结果可以返回任意字符串（可以与表中列出的结果都不一样）|

```javascript
value instanceof Constr
```

如果value是一个通过Constr构造器创建的对象，则返回true，否则返回false。

### 3. 布尔值

在JavaScript中可以使用任意值来表示布尔值。他们都会被解释成true或false。

以下值会被解释成false：

- undefined、null。
- 布尔值：false。
- 数字：-0、NaN。
- 字符串：''。

其他所有的值都会被当成true。

二元逻辑运算符是短路的。（&&, ||）.

#### 等式运算符

- 常规的，或“宽松的”相等： == 和 ！=。
- 严格的相等： === 和 ！==。

### 4. 数字

JavaScript中所有的数字都是浮点数。

```javascript
> 1 === 1.0
true
```

`Infinity`比任何一个数都要大。（NaN除外）

`-Infinity`比任何一个数都要大。

Infinity多数情况也是一个错误的值：

```javascript
> 3 / 0
Infinity
```

也可以使用Infinity作为默认值。

### 5. 字符串

字符串字面量限定在单引号或双引号之内。反斜杠（\）用于转义字符及产生一些控制字符。

可以通过方括号加索引的方式访问字符串中的单个字符：

```javascrpt
> var str = 'abc';
> str[1]
b
```

#### 5.1 字符串运算符

可以通过加号`+`来拼接两个字符串，如果一个是字符串，另一个也将转换为字符串。

#### 5.2 字符串方法

slice（begin）

slice（begin， end）

产生一个substring。

### 6. 语句

#### 6.1 条件语句

```javascript
if(/*condition*/){
    //then
}

if(/*condition*/){
    //then
}else{
    //then
}

if(/*condition*/){
    //then
}else if(/*condition*/){
    //then
}else if(/*condition*/){
    //then
}else{
    //then
}
```

switch语句支持字符串。

#### 6.2 循环语句

```javascript
for([<<init>>]; [<<condition>>];[<<post_iteration>>]){
    <<statement>>
}

while(/*condition*/){
    /*
        statement
    */
}

do{
    //statement
}while(/*condition*/);
```

break 和 continue

### 7. 函数

- 函数声明

    ```javascript
    function add(param1, param2){
        return param1 + param2;
    }
    ```

- 给变量赋值为函数表达式的方式

    ```javascript
    var add = function (param1, param2){
        return param1 + param2;
    }
    ```

因为函数会返回一个值，所以可以将函数作为参数直接传递给另外的函数。

通过函数声明创建的函数，它们的实体会被移动到所在作用域的开始处。

```javascript
function foo(){
    bar();  //ok

    function bar(){
        //....
    }
}
```

但是变量赋值方式不行。

#### 7.1. 特殊的变量--arguments

在JavaScript中，函数的所有参数都可以被自由调用，他会通过arguments变量来使所有参数可用。（就是传入的函数多余声明函数时定义的行参，我们也可以通过arguments来获取到多余的实参）arguments看起来像个数组，但却不具备数组的方法：

```javascript
> function(){return arguments}
> var args = f('a', 'b', 'c', 'd');
> args.length
3
> args[0]
'a'
```

#### 7.2. 参数太多或太少

多余的参数会被忽略（arguments可以获取到所有的参数），丢失的参数会得到undefined这个值。

#### 7.3. 可选参数

给参数赋上默认值的通用模式：

```javascript
function pair(x, y){
    x = x || 0;
    y = y || 0;
    return [x, y];
}
```

`||`运算符会在x为真值时返回x。

#### 7.4. 强制参数长度

可以通过arguments.length来检查参数长度。

```javascript
function pair(x, y){
    if(arguments.length !== 2){
        throw new Error('Need exactly 2 arguments');
    }
}
```

将arguments转换为数组的方法：

```javascript
function toArray(arrayLikeObject){
    return Array.prototype.slice.call(arrayLikeObject);
}
```

#### 7.5. 异常捕获

JavaScript可以通过`throw new Error(str);`的方式抛出一个异常;

捕获异常使用try-catch语句

```javascript
try{
    //code
}catch(exception){
    console.log(exception);
}
```

### 8. 变量作用域和闭包

#### 8.1. 变量是函数作用域的

一个变量的作用域总是完整的函数。例如：

```javascript
function foo(){
    var x = -512;
    if(x < 0){
        var temp = -x;
        ...
    }
    console.log(temp);
}
```

在if内定义的变量即使出了if作用域，只要还是在函数内就都还可以使用。

#### 8.2. 变量的提升特性

所有变量声明都会被提升：声明会被移动到函数的开始处，而赋值则仍然会在原来的位置进行。

```javascript
function foo(){
    console.log(tmp);  //undefined
    if(false){
        var tmp = 3;
    }
}

//相当于

function foo(){
    var tmp;
    console.log(tmp);
    if(false){
        tmp = 3;
    }
}
```

在函数中定义的变量，其声明在函数开始处，但没赋值。

#### 8.3. 闭包

每个函数都和它周围的变量保持着连接，哪怕他离开被创建时的作用域也是如此。
例如：

```javascript
function createIncrementor(start){
    return function(){
        start ++;
        return start;
    }
}
```

内部匿名函数在创建结束后即离开它的上下文环境，但它仍然保持着和start的连接。

就是说，在函数内部可以使用外部作用域定义的变量。

闭包：函数以及它所连接的周围作用域中的变量即为闭包。

#### 8.4. IIFF模式：引入一个新的作用域

在JavaScript中，想要防止一个变量变成全局变量。不能通过块来做，必须使用函数。**IIFF模式**可以将函数当做类似块的方式来使用。

```javascript
(function(){   //open IIFF
    var tmp = ...;   //not a global variable
}());     //close IIFF
```

IIFF用例：闭包造成的无意共享

闭包会持续地保持与外部变量的连接，而这有时候并不是你想要的：

```javascript
var result = [];
for(var i = 0; i < 5; i++){
    result.push(function(){return i});
}
console.log(result[1]());
console.log(result[3]());
```

数组result在push时，是在数组中放入了一个函数，所以result[1]处取出的是一个函数，所以需要加上括号执行这个函数。

因为function中的i是for作用域中的。所以在console打印方法返回值时都是5,因为return i;中的i连接的是for中的i，而跳出循环后，i的值就是5了。

要防止这种情形出现，那么就需要使用**IIFF模式**创建一个局部变量，用来保存运行期间i值的一个快照。

```javascript
for(var i = 0; i < 5; i++){
    (funtion(){
        var i2 = i;
        result.push(function(){return i2});
    }());
}
```

### 9 对象和构造函数

#### 9.1 单一对象

对象的每个属性都是一个（键，值）对。键名都是字符串，值可以是JavaScript的任意值。

```javascript
var jane = {
    name: 'jane',
    describe: function(){
        return 'Person named' + this.name;
    }
};

//get
> jane.name
'Jane'

//set
> jane.name = 'John';
> jane.myProperty = 'abc'; //property created automatically
```

函数作为值的属性被称为方法，如describe。

使用`in`运算符检查属性是否存在：

```javascript
> 'myProperty' in jane
true
> 'foo' in jane
false
```

如果读取一个不存在的属性，会得到undefined。

使用delete运算符移除属性

```javascript
> delete jane.myProperty
true
> 'myProperty' in jane
false
```

#### 9.2 任意属性名

如果想用其他字符串（不满足javascript对标识符的定义）作为属性名，需使用引号引起来，再通过对象字面量和方括号来获取或设置这个属性。

```javascript
> var obj = {'not an identifier': 123};
> obj['not an identifier']
123
> obj['not an identifier']=456 //赋值
```

方括号可以用来动态计算属性键名：

```javascript
> var obj = {hello: 'world'};
> var x = 'hello';

> obj[x]
'hello'
> obj['hel' + 'lo']
'world'
```

#### 9.3 提取方法

将对象的方法保存到一个变量中，对于原函数而言，它不再是一个方法，this的值也会是undefined（在严格模式下，严格模式就是在函数起始出加上`'use strict';`字符串）

```javascript
'use strict';
var jane = {
    name: 'Jane',

    describe: function(){
        return 'Person named ' + this.name;
    }
};

//错误
var func2 = jane.describe;
func2()
TypeError: Cannot read property 'name' of undefined
```

使用`bind()`方法，它会创建一个this总是指向给定值的新函数：

```javascript
> var func2 = jane.describe.bind(jane);
> func2()
'Person named Jane'
```

所有函数都有其特殊的this变量。如果在方法中有嵌套函数，在嵌套函数中不能访问方法中的this变量。
例如：

```javascript
var jane = {
    name: 'Jane',
    friends: ['Tarzan', 'Cheeta'],
    logHiToFriends: function(){
        'use strict';
        this.friends.forEach(function(friend){
            console.log(this.nanme + ' says hi to ' + friend);
        });
    }
}

> jane.logHiToFriends()
TypeError: Cannot read property 'name' of undefined
```

解决方法：

1. 将this保存到不同变量中

    ```javascript
    logHiToFriends: function(){
        'use strict';
        var that = this;
        this.friends.forEach(function(friend){
            console.log(that.nanme + ' says hi to ' + friend);
        });
    }
    ```

    由此可知：内部函数之所以不能使用外部方法的this对象，是因为内部函数的this对象覆盖了外部方法的this对象。

2. 利用forEach的第二个参数，他可以给this指定一个值

    ```javascript
    logHiToFriends: function(){
        'use strict';
        this.friends.forEach(function(friend){
            console.log(that.nanme + ' says hi to ' + friend);
        }， this);
    }
    ```

    使用外部方法的this对象，而不是嵌套函数的this对象。
