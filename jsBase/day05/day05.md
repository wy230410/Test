## 1 arguments的使用
#### Target
1. 能够说出冒泡排序的实现思路
2. 能够封装一个函数, 返回两个数的最大值
3. 能够说出全局作用域和局部作用域区别
4. 能够书写定义函数的两种不同方式
5. 能够说出预解析的过程
6. 能够自定义创建对象
7. 能够使用对象的属性和方法
8. 能够for..in遍历对象的所有属性
9. 能够说出new关键字的执行过程
10. 能够说出构造函数和对象的区别

### 1.1 arguments

当不确定有多少个参数传递的时候，可以用 <span style="color:red;">arguments </span>来获取。在 JavaScript 中，arguments实际上它是当前函数的一个<span style="color:red;">内置对象</span>。所有函数都内置了一个 arguments 对象，arguments 对象中存储了<span style="color:red;">传递的所有实参</span>。

<span style="color:red;">**arguments展示形式是一个伪数组**</span>，因此可以进行遍历。

**伪数组**具有以下特点：

- 具有 length 属性

- 按索引方式储存数据 

- 不具有数组的 push , pop 等方法

  注意：<span style="color:red;">**在函数内部使用该对象**</span>，用此对象获取函数调用时传的实参。

### 1.2 案列 求函数的最大值

```javascript
// 求函数的最大值
function getMax() { // arguments = [1,2,3]
    var max = arguments[0];
    for (var i = 1; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
}
console.log(getMax(1, 2, 3));
console.log(getMax(1, 2, 3, 4, 5));
console.log(getMax(11, 2, 34, 444, 5, 100));
```

### 1.3 案例 函数翻转

```javascript
// 利用函数翻转任意数组 reverse 翻转
function reverse(arr) {
    var newArr = [];
    for (var i = arr.length - 1; i >= 0; i--) {
        newArr[newArr.length] = arr[i];
    }
    return newArr;
}
var arr1 = reverse([1, 3, 4, 6, 9]);
console.log(arr1);
var arr2 = reverse(['red', 'pink', 'blue']);
console.log(arr2);
```

### 1.4 案例 利用函数冒泡排序

```javascript
// 利用函数冒泡排序 sort 排序
function sort(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
var arr1 = sort([1, 4, 2, 9]);
console.log(arr1);
var arr2 = sort([11, 7, 22, 999]);
console.log(arr2);
```

### 1.5 案列 利用函数判断闰年

```js
// 利用函数判断闰年
function isRunYear(year) {
    // 如果是闰年我们返回 true  否则 返回 false 
    var flag = false;
    if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
        flag = true;
    }
    return flag;
}
console.log(isRunYear(2000));
console.log(isRunYear(1999));
```



### 1.6 函数案例

#### 1.6.1 **函数可以调用另外一个函数**

因为每个函数都是独立的代码块，用于完成特殊任务，因此经常会用到函数相互调用的情况。

#### 1.6.2 案例练习

```javascript
// 用户输入年份，输出当前年份2月份的天数
function backDay() {
    var year = prompt('请您输入年份:');
    if (isRunYear(year)) { // 调用函数需要加小括号
        alert('当前年份是闰年2月份有29天');
    } else {
        alert('当前年份是平年2月份有28天');
    }
}
backDay();


// 判断是否为闰年的函数
function isRunYear(year) {
    // 如果是闰年我们返回 true  否则 返回 false 
    var flag = false;
    if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
        flag = true;
    }
    return flag;
}
```



### 1.7 定义函数的两种方式🔥🔥🔥

#### 1.7.1 声明式(命名函数)

利用函数关键字 function 自定义函数方式

```js
// 声明定义方式
function fn() {...}
// 调用  
fn();  
```

- 因为有名字，所以也被称为命名函数
- 调用函数的代码既可以放到声明函数的前面，也可以放在声明函数的后面

#### 1.7.2 表达式(匿名函数）

利用函数表达式方式的写法如下： 

```js
// 这是函数表达式写法，匿名函数后面跟分号结束
var fn = function(){...}；
// 调用的方式，函数调用必须写到函数体下面
fn();
```

- 因为函数没有名字，所以也被称为匿名函数
- 这个fn 里面存储的是一个函数  
- 函数表达式方式原理跟声明变量方式是一致的
- 函数调用的代码必须写到函数体后面



## 2 - 作用域

**目标**

1. **<font color='red'>JS的两种作用域</font>**
2. **<font color='red'>全局变量和局部变量</font>**
3. **<font color='red'>在作用域链中查找变量的值</font>**

### 2.1 概述

> 作用域:  **就是变量与函数的可访问范围，即作用域控制着变量和函数的可见性和生命周期。**



**特点：**

1. 增强了程序的可靠性
2. **减少了名字冲突**

**作用域分类：**

ES6之前，ES作用域只有：

 - **全局作用域** (Global Scope): 中的对象在代码中的任何地方都能访问，其生命周期伴随着页面的生命周期。
 - **函数作用域** (Local Scope) :  JS的作用域是通过函数来定义的,  在一个函数中定义的变量只对这个函数内部可见, 称为函数(局部)作用域

ES6新增

 - **块级作用域：块级作用域内声明的变量不影响外面的变量**



### 2.2 全局作用域

作用于所有代码执行的环境（整个 script 标签内部）或者一个独立的 js 文件。

### 2.3 局部作用域

作用于函数内的代码环境，就是**局部作用域**。 因为跟函数有关系，所以也称为**函数作用域**。

**CODE01**

```js
//全局作用域： 整个script标签 或者是一个单独的js文件
var num = 10;
var num = 30;
console.log(num);

//局部作用域（函数作用域） 在函数内部就是局部作用域 这个代码的名字只在函数内部起效果和作用
function fn() {
    // 局部作用域
    var num = 20;
    console.log(num);
}
fn();
```

### 2.4 **块级作用域（扩展）**

块作用域由 { } 包括。如`if / if else / switch`

当使用`let`和`const`定义变量时，仅作用于当前声明的块级结构里

**CODE02**

```js
// 对比打印结果  
 if (true) {
    var num = 123;
    let num2 = 456;
    const num3 = 789
    console.log('块内', num, num2, num3)
  }
  console.log('块外1', num)
  console.log('块外2', num, num2, num3)
```

### 2.5 变量的作用域🔥🔥🔥

由作用域，衍生出来了变量作用域，也就是变量起作用的范围

根据作用域的不同，变量可以分为两种：

- 全局变量
- 局部变量

#### 2.5.1 全局变量

> 在**全局作用域**下声明的变量叫做**全局变量**
>
> 在函数外部定义的变量

- 全局变量在代码的任何位置都可以使用
- 在全局作用域下 var 声明的变量 是全局变量
- 特殊情况下，在函数内不使用 var 声明的变量也是全局变量（不建议使用）

#### 2.5.2 局部变量

> 在**局部作用域**下声明的变量叫做**局部变量**
>
> 在函数内部定义的变量

1. 局部变量只能在该**函数内部**使用
2. 在函数内部 var 声明的变量是局部变量
3. 函数的形参实际上就是局部变量
4. 当函数运行结束，就会被销毁，因此更节省内存空间

**CODE03**

```JS
//全局变量 ：在全局作用域下声明的变量叫做全局变量
var num = 10; // num就是一个全局变量
console.log(num);

function fn() {
    console.log(num);
}
fn();

// 2. 局部变量： 在局部作用域下的变量
function fun(aru) {// 注意： 函数的形参也可以看做是局部变量
    var num1 = 10; // num1就是局部变量 只能在函数内部使用
    num2 = 20;//隐式全局变量，不推荐使用
}

console.log(num1, num2)
fun();
```

### 2.6 作用域链 🔥🔥

> 叠盒子，叠叠乐

只要是代码, 就至少有一个作用域.

1. 写在函数内部的局部作用域;
2. 未写在任何函数内部即在全局作用域中；

如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域；

根据在**<font color='red'>[内部函数可以访问外部函数变量]</font>**的这种机制，用链式查找决定哪些数据能被内部函数访问，就称作作用域链

**CODE04**

```js
function f1() {
    var num = 123;
    function f2() {
        console.log( num );
    }
    f2();
}
var num = 456;
f1();
```



**作用域链：采取就近原则的方式来查找变量最终的值。**

**练习：看看返回结果是什么？**

```JS
var a = 1;
function fn1() {
    var a = 2;
    var b = '22';
    fn2();
    function fn2() {
        var a = 3;
        fn3();
        function fn3() {
            var a = 4;
            console.log(a); //a的值 ?
            console.log(b); //b的值 ?
        }
    }
}
fn1();
```

**总结**：

1. **作用域链：**函数嵌套函数，作用域中有作用域，形成作用域链。
2. 规律：采取就近原则-由下至上的方式来查找变量最终的值。
3. 真正开发的时候，函数嵌套之后，变量名一般不会起一样的名字，但是理解作用域链很重要！

## 3.  变量声明提升（预解析）🔥🔥🔥

目标

1. 变量声明如何提升
2. 函数声明如何提升

### 3.1 概念

1. JavaScript 代码是由浏览器中的 JavaScript 解析器来执行的。

2. JavaScript 解析器在运行 JavaScript 代码的时候分为两步：**声明提升(预解析)**和**代码执行**。

3. **声明提升(预解析)：**在当前作用域下, JS 代码执行之前，浏览器会默认把带有 `var` 和 `function` 声明的变量在内存中进行提前声明或者定义
   - **其实相当于提前读一遍代码，找`var，function`，将变量和函数声明进行提升**
4. 代码执行： 从上到下执行JS语句

### 3.2 变量声明提升

**变量声明提升（变量预解析）：** 变量的声明会被提升到**当前作用域的最上面**，**变量的赋值不会提升**

![img](https://gtd-imgs-md.oss-cn-beijing.aliyuncs.com/imgs/20211203115319.png)

**CODE05**

```JS
console.log(num);  // 结果是多少？
var num = 10;      // ？
//结果：undefined

//注意：**变量提升只提升声明，不提升赋值**
```

### 3.3 函数声明提升

**函数声明提升（函数预解析）：** 函数的声明会被提升到**当前作用域的最上面**，但是不会调用函数

![img](https://gtd-imgs-md.oss-cn-beijing.aliyuncs.com/imgs/20211203115323.png)

```JS
fn();
function fn() {
    console.log('打印');
}
//结果：控制台打印字符串 --- ”打印“ 
```

### 3.4 函数表达式声明函数问题

> 函数表达式创建函数，会执行变量提升（因为是var关键字）

**CODE06**

```js
console.log(fn)
fn();
var fn = function() {
    console.log('想不到吧');
}
//结果：报错提示 ”fn is not a function"

//解释：该段代码执行之前，会做变量声明提升，fn在提升之后的值是undefined；而fn调用是在fn被赋值为函数体之前，此时fn的值是undefined，所以无法正确调用
```

### 3.5 声明提升案例

```js
// 预解析案例
// 案例1
var num = 10;
fun();

function fun() {
    console.log(num);
    var num = 20;
}

// 换个写法
// function fun() {
//     var num;
//     console.log(num);
//     num = 20;
// }
// num = 10;
// fun();


// 案例2
var num = 10;

function fn() {
    console.log(num);
    var num = 20;
    console.log(num);
}
fn();

// 换个写法
// function fn() {
//     var num;
//     console.log(num);
//     num = 20;
//     console.log(num);
// }
// num = 10;
// fn();

// 案例3
var a = 18;
f1();

function f1() {
    var b = 9;
    console.log(a);
    console.log(b);
    var a = '123';
}

// 换个写法
// function f1() {
//     var b;
//     var a;
//     b = 9;
//     console.log(a);
//     console.log(b);
//     a = '123';
// }
// a = 18;
// f1();

// 案例4
f1();
console.log(c);
console.log(b);
console.log(a);

function f1() {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}

// 换个写法
// function f1() {
//     var a;
//     a = b = c = 9;
//     // 相当于 var  a  = 9; b = 9; c = 9; b 和 c 直接赋值 没有var 声明 当 全局变量看
//     // 集体声明  var a = 9, b = 9, c = 9;
//     console.log(a);
//     console.log(b);
//     console.log(c);
// }
// f1();
// console.log(c);
// console.log(b);
// console.log(a);
```

### 3.6 变量总结

1. 变量声明提升 ：变量的声明会被提升到当前作用域的最上面，变量的赋值不会提升。
2. 函数声明提升 ：函数的声明会被提升到当前作用域的最上面，但是不会调用函数。
3. 代码阅读方式：**提前读一遍代码，找var，function，将变量和函数声明进行提升**

## 4.  对象🔥🔥🔥

目标：

1. 对象的使用场景
2. **<font color='red'>创建对象</font>**
3. new的执行过程
4. **<font color='red'>遍历对象</font>**

### 4.1 对象的概念

> 对象是一组**<font color='red'>无序</font>**的相关**属性**和**方法**的集合（可以存放任意类型的元素）
>

- 对象是一组**<font color='red'>无序</font>**的相关**属性**和**方法**的集合，所有的事物都是对象，例如字符串、数值、数组、函数等。

- 对象是由**属性**和**方法**组成的

  - 属性：**事物的特征**，在对象中用属性来表示（常用名词）
  - 方法：**事物的行为**，在对象中用方法来表示（常用动词）

  

*注意：一个对象中**属性**和**方法**并不是都具有的，看具体情况来设置一个对象中的内容*

- 对象中的变量，称之为属性 
- 对象中的函数，称之为方法 

### 4.2 为什么需要对象

> 对象的数据结构清晰，数据更语义化，表意明显，更适合遍历

**场景：** 存一个值时，可以使用变量，保存多个值（一组值）时，可以使用数组。那么如果想储存一组有意义且方便查找的数据呢？

数组：

```js
var arr = ['张三', '男', 150, 154];
```

**引发的问题问题：** 用数组保存数据的缺点 - 数据只能通过索引值访问，开发者需要清晰的清楚所有的数据的排行才能准确地获取数据，而当数据量庞大时，不可能做到记忆所有数据的索引值。

**解决方案：为了让更好地存储一组数据，就可以用到对象。对象中为每项数据设置了属性名称，可以访问数据更语义化，数据结构清晰，表意明显，方便开发者使用**。

```js
 var obj = {
      "name":"张三",
      "sex":"男",
      "age":128,
      "height":154
  }
```

### 4.3 创建对象的三种方式🔥🔥🔥

#### 4.3.1 利用字面量创建对象

```js
var obj = {
    key: value,
    key2: value2
    ...
};
```

- key - 键：相当于**属性名**
- value - 值：相当于**属性值**，可以是任意类型的值（数字类型、字符串类型、布尔类型，函数类型等）

  - 在对象中的方法，也可以理解为是一个属性，可以称之为方法属性
- 对象里面的数据, 可以简称为键值对.

**代码实例：**

**CODE07**

```js
var star = { // star即是创建的对象。
    name : '张三',
    age : 18,
    sex : '男',
    sayHi : function(){
        alert('Hi~~');
    }
};
```

**练习：以自己喜欢的角色创建一个对象，对象中要包含他的姓名，性别，特点等等**

#### 4.3.2 对象的访问和调用

**访问对象的属性**

- 点语法：对象.属性

  **CODE07**

  ```JS
  console.log(star.name)
  ```

- 中括号语法：对象['属性']

  **CODE07**

  ```JS
  console.log(star['name'])//star[name],先找name变量的值：'age'，star['age']---- 18
  ```

**调用对象的方法**

- 点语法：对象.方法名()

  **CODE07**

  ```
  star.sayHi(); // 调用方法,注意，一定不要忘记带后面的括号
  ```

- 中括号语法：对象['属性']

  **CODE07**

  ```JS
  star['sayHi']();
  ```

**总结**

- 其实调用属性和方法语法都一样
- 只不过方法调用需要添加小括号

#### 4.3.3 变量、属性、函数、方法总结

- 属性是对象的一部分，而变量不是对象的一部分，变量是单独存储数据的容器
  - 变量：单独声明赋值，单独存在
  - 属性：对象里面的变量称为属性，不需要声明，用来描述该对象的特征

- 方法是对象的一部分，函数不是对象的一部分，函数是单独封装操作的容器
  - 函数：单独存在的，通过“函数名()”的方式就可以调用
  - 方法：对象里面的函数称为方法，方法不需要声明，使用“对象.方法名()”的方式就可以调用，方法用来描述该对象的行为和功能。 (思考：能不能不用来描述该对象呢？)
- **总结**：
  - 对象中的变量，称之为属性 
  - 对象中的函数，称之为方法 

#### 4.3.4 利用 new Object 创建对象

**语法**

```js
// 创建空对象
var obj = new Object();
```

通过内置构造函数Object创建对象，此时andy变量已经保存了创建出来的空对象

**代码实例：**

**CODE08**

```js
// 创建空对象
var person = new Object();
person.name = '张三'; // 给andy添加name属性，并赋值
person.age = 18;
person.sex = '男';
person.sayHi = function(){ // 给andy添加sayHi方法，并赋值
    alert('Hi~~');
}
```

**注意：**

- Object() ：第一个字母大写   
- new Object() ：需要 new 关键字
- 使用的格式：对象.属性 = 值;     

**练习：以自己喜欢的角色创建一个对象，对象中要包含他的姓名，性别，特点等等**

比如  :用new Object 形式创建一个鸣人对象  他有姓名 性别 年龄, 技能skill 影分身之术



#### 4.3.5 利用构造函数创建对象

##### 4.3.5.1 构造函数概念

**场景：**一个对象中有很多个属性和方法，当我们需要创建许多个键相同，但内容有差异的对象时该怎么办？只能复制粘贴吗？

**答:** 可以用函数的方式，去封装创建这个对象时的代码



- 因我们前面两种创建对象的方式一次只能创建一个对象

- 里面很多的属性和方法是大量相同的 我们只能复制 

- 所以JS提供给我们另一种创建对象的方式, 构造函数

  

**构造函数：**创建对象的方法 - 把对象里面一些相同的属性和方法抽象出来封装到函数里面

##### 4.3.5.2  语法

- 定义构造函数的语法如下：

  ```js
  function 构造函数名(形参1,形参2,形参3) { // 构造函数的形参与对象的普通属性是一致的
       this.属性名1 = 形参1; //形参就是要给属性赋值
       this.属性名2 = 形参2;
       this.属性名3 = 形参3;
       this.方法名 = function(){
           
       };
  }
  ```

- 构造函数的调用语法：**通过new调用**

  ```js
  var obj = new 构造函数名(实参1，实参2，实参3)
  ```

  **注意事项**

  1.   构造函数约定**首字母大写**。
  2.   函数内的属性和方法前面需要添加 **this** ，表示当前对象的属性和方法。
  3.   构造函数中**不需要 return 返回结果**。
  4.   当我们创建对象的时候，**必须用 new 来调用构造函数**。

- 实例

  **CODE09**

  ```JS
  //需求：定义一个人类构造函数，创建的人类对象包含属性：姓名，年龄，性别，方法：打招呼。
  
  function Person(name, age, sex) {
  	// 1. 在函数内部创建了一个空对象
      // 2. 让this指向这个空对象 (等于)
      // 3. 执行构造函数里的代码, 给这个空对象添加属性和方法
      // 4. 返回这个对象(this)
     // var this = new Object();
     this.name = name;// 属性的值，都是通过同名的形参来赋值的
     this.age = age;
     this.sex = sex;
     this.sayHi = function() { //函数不需要通过形参来赋值
         console.log('nice to meet u :)')
     }
      // return this; 
  }
  // 创建出来一个张三的人类对象，张三的名字是张三，100，男
  var zs = new Person('张三', 19, '男'); 
  // this 就是即将创建出来的对象
  // this:这个，这个对象
  console.log(zs.name);// 张三
  
  var ls = new Person('李四', 18, '男');
  console.log(ls.name);
  ls.sayHi()
  ```

  **练习：创建一个游戏角色的构造函数，里面包含角色名称，血量，攻击力，攻击方式（方式使用对象方法的形式构建console.log输出打印），然后通过new的形式去构建对象**

  **CODE10**
  
  ```js
  // 如
  function Hero(name, blood, attack) { // 构造函数的参数，就是对象的属性
      this.name = name
      this.blood = blood
      this.attack = attack
      this.attackType = function(att) {
          alert('攻击方式：' + att)
      };
  }
  var raye = new Hero('零依', '1500', '1500')
  console.log(raye.name)
  lianPo.attackType('Sky Striker Mecha')
  ```

#### 4.3.6 构造函数与对象的区别

- **构造函数：**如 Stars()，**抽象**了对象的公共部分，封装到了函数里面，它**泛指某一大类**（class）  
  **对象：**如 var ldh = new Stars()，**特指某一个（具体的某一个）**，通过 new 关键字创建对象的过程我们也称为对象实例化

  

- **实例：就是实际的例子**（某一大类中的实际的例子）

- 对象又叫做**实例**

- 创建对象的过程，也叫做实例化

  

#### 4.3.7 new关键字的执行过程🔥🔥🔥

> new → 新建

1. 在内存中创建了一个空的对象 .  new 构造函数  ==>  内存创建了一个空的对象
2. 让this指向这个空对象.    ==> 指向, 可以理解为等于. 把this替换为这个空对象看待.
3. 执行构造函数里面的代码 给这个空对象添加属性和方法.  ==> 这个对象就不再空了
4. 返回这个对象



>  如果你需要一个对象怎么做, 通过构造函数new一个对象.



#### 4.3.8 遍历对象的属性🔥🔥

> for...in 语句用于对对象的属性进行循环操作。
>
> **理解**：遍历obj对象中的所有属性名key，然后我们可以根据obj[key]获取属性值

- 语法

  ```js
  for (变量 in 对象名字) {
      // 在此执行代码
  }
  ```

- 语法中的变量是自定义的，它需要符合命名规范，通常我们会将这个变量写为 k 或者 key。

  **CODE11**

  ```js
  for (k in obj) {
  	// ...
  }
  
   var obj = {
       name: '张三',
       age: 18,
       sex: '男',
       fn: function() {}
   };
  for (var k in obj) { // for in遍历obj，其实遍历的是obj中的属性名 ['name','age']
      console.log(k);       // 这里的 k 是属性名 （字符串）  ‘name’,'age'
      console.log(obj[k]); // 这里的 obj[k] 是属性值  obj['name'] obj['age']
  }
  // obj.k, obj['k'] // 找obj中属性名字叫做k的属性的值
  // obj[k]  // 先找变量k，拿到k的值，然后再去obj中查找
  // 如果遍历第一次： k = ‘name’ ，obj['name']
  
  // 结论： 中括号语法  ****
  // 如果带上引号，引号中是属性名
  // 如果没有带引号，说明是变量名
  ```





























































