# JavaScript 基础概念

## 目录

- [什么是 JavaScript](#什么是-javascript)
- [JavaScript 的特点](#javascript-的特点)
- [JavaScript 的组成](#javascript-的组成)
- [JavaScript 语法基础](#javascript-语法基础)
- [数据类型](#数据类型)
- [变量与常量](#变量与常量)
- [运算符](#运算符)
- [流程控制](#流程控制)
- [函数](#函数)
- [对象](#对象)
- [数组](#数组)
- [最佳实践](#最佳实践)

## 什么是 JavaScript

JavaScript（简称 JS）是一种轻量级的、解释型的编程语言，用于为网页添加交互功能。它是 Web 开发的三大核心技术之一（HTML、CSS、JavaScript）。

JavaScript 最初是为浏览器设计的，但现在已经广泛应用于服务器端（Node.js）、移动应用、桌面应用等领域。

## JavaScript 的特点

1. **脚本语言**：不需要编译，直接由浏览器解释执行
2. **弱类型语言**：变量类型可以动态改变
3. **面向对象**：支持面向对象编程，但也支持函数式编程
4. **解释执行**：逐行执行代码
5. **事件驱动**：通过事件触发函数执行
6. **跨平台**：可以在不同的操作系统和浏览器上运行
7. **动态性**：可以动态修改 HTML 和 CSS，添加或删除元素

## JavaScript 的组成

JavaScript 由以下三个部分组成：

1. **ECMAScript**：JavaScript 的核心语法标准，定义了语言的基础语法、数据类型、函数等
2. **DOM（Document Object Model）**：文档对象模型，用于操作 HTML 文档的 API
3. **BOM（Browser Object Model）**：浏览器对象模型，用于操作浏览器窗口的 API

## JavaScript 语法基础

### 注释

JavaScript 支持单行注释和多行注释：

```javascript
// 单行注释

/*
  多行注释
  多行注释
*/
```

### 语句

JavaScript 语句以分号 `;` 结尾，分号可以省略，但建议使用：

```javascript
console.log("Hello, World!"); // 完整语句
console.log("Hello, World!")  // 分号省略，不推荐
```

### 标识符

标识符是用于命名变量、函数、对象等的名称，必须遵守以下规则：

- 只能包含字母、数字、下划线 `_` 和美元符号 `$`
- 不能以数字开头
- 区分大小写
- 不能使用 JavaScript 关键字和保留字

## 数据类型

JavaScript 有两种数据类型：**基本数据类型**和**引用数据类型**。

### 基本数据类型

- **Number**：数字类型，包括整数和浮点数
  ```javascript
  let age = 18;       // 整数
  let price = 19.99;  // 浮点数
  let pi = 3.14159;   // 浮点数
  ```

- **String**：字符串类型，用于表示文本
  ```javascript
  let name = "John";           // 双引号
  let message = 'Hello';       // 单引号
  let html = `
    <div>
      <p>Hello, World!</p>
    </div>
  `;                            // 模板字符串（ES6+）
  ```

- **Boolean**：布尔类型，只有两个值：`true` 和 `false`
  ```javascript
  let isActive = true;
  let isClosed = false;
  ```

- **Null**：表示空值或不存在的对象
  ```javascript
  let emptyValue = null;
  ```

- **Undefined**：表示未定义的值
  ```javascript
  let undefinedValue; // 声明但未赋值的变量
  ```

- **Symbol**：表示唯一的标识符（ES6+）
  ```javascript
  let symbol1 = Symbol();
  let symbol2 = Symbol("description");
  ```

- **BigInt**：表示大整数（ES2020+）
  ```javascript
  let bigNumber = 123456789012345678901234567890n;
  ```

### 引用数据类型

- **Object**：对象类型，是 JavaScript 中所有引用类型的基础
  ```javascript
  let person = {
    name: "John",
    age: 30,
    sayHello: function() {
      console.log(`Hello, my name is ${this.name}`);
    }
  };
  ```

- **Array**：数组类型，用于存储多个值
  ```javascript
  let numbers = [1, 2, 3, 4, 5];
  let fruits = ["apple", "banana", "orange"];
  ```

- **Function**：函数类型，用于封装可重复执行的代码
  ```javascript
  function add(a, b) {
    return a + b;
  }
  ```

- **Date**：日期类型，用于处理日期和时间
  ```javascript
  let now = new Date();
  let birthday = new Date(1990, 0, 1); // 1990年1月1日
  ```

- **RegExp**：正则表达式类型，用于匹配字符串
  ```javascript
  let pattern = /\d+/;
  let result = pattern.test("123"); // true
  ```

## 变量与常量

### 变量声明

JavaScript 中使用 `var`、`let` 或 `const` 关键字来声明变量：

- **var**：ES5 中的变量声明方式，存在变量提升和函数作用域
  ```javascript
  var x = 10;
  ```

- **let**：ES6 中的变量声明方式，具有块级作用域，不存在变量提升
  ```javascript
  let y = 20;
  ```

- **const**：ES6 中的常量声明方式，一旦赋值就不能修改，具有块级作用域
  ```javascript
  const z = 30;
  ```

### 变量命名规则

1. 只能包含字母、数字、下划线 `_` 和美元符号 `$`
2. 不能以数字开头
3. 区分大小写
4. 不能使用 JavaScript 关键字和保留字
5. 建议使用驼峰命名法（camelCase）

## 运算符

JavaScript 支持多种运算符：

### 算术运算符

```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.3333333333333335
console.log(a % b);  // 1
console.log(a ** b); // 1000
```

### 赋值运算符

```javascript
let x = 10;
x += 5;  // 等同于 x = x + 5
x -= 3;  // 等同于 x = x - 3
x *= 2;  // 等同于 x = x * 2
x /= 4;  // 等同于 x = x / 4
x %= 3;  // 等同于 x = x % 3
```

### 比较运算符

```javascript
let a = 10;
let b = "10";

console.log(a == b);   // true（值相等）
console.log(a === b);  // false（值和类型都相等）
console.log(a != b);   // false
console.log(a !== b);  // true
console.log(a > b);    // false
console.log(a < b);    // false
console.log(a >= b);   // true
console.log(a <= b);   // true
```

### 逻辑运算符

```javascript
let x = true;
let y = false;

console.log(x && y);  // false（逻辑与）
console.log(x || y);  // true（逻辑或）
console.log(!x);      // false（逻辑非）
```

### 三元运算符

```javascript
let age = 18;
let message = age >= 18 ? "成年人" : "未成年人";
console.log(message); // "成年人"
```

## 流程控制

### 条件语句

- **if-else 语句**
  ```javascript
  let age = 18;
  
  if (age >= 18) {
    console.log("成年人");
  } else {
    console.log("未成年人");
  }
  ```

- **if-else if-else 语句**
  ```javascript
  let score = 85;
  
  if (score >= 90) {
    console.log("优秀");
  } else if (score >= 80) {
    console.log("良好");
  } else if (score >= 60) {
    console.log("及格");
  } else {
    console.log("不及格");
  }
  ```

- **switch 语句**
  ```javascript
  let day = 3;
  let dayName;
  
  switch (day) {
    case 1:
      dayName = "星期一";
      break;
    case 2:
      dayName = "星期二";
      break;
    case 3:
      dayName = "星期三";
      break;
    case 4:
      dayName = "星期四";
      break;
    case 5:
      dayName = "星期五";
      break;
    case 6:
      dayName = "星期六";
      break;
    case 7:
      dayName = "星期日";
      break;
    default:
      dayName = "无效的日期";
  }
  
  console.log(dayName); // "星期三"
  ```

### 循环语句

- **for 循环**
  ```javascript
  for (let i = 0; i < 5; i++) {
    console.log(i); // 0, 1, 2, 3, 4
  }
  ```

- **while 循环**
  ```javascript
  let i = 0;
  while (i < 5) {
    console.log(i); // 0, 1, 2, 3, 4
    i++;
  }
  ```

- **do-while 循环**
  ```javascript
  let i = 0;
  do {
    console.log(i); // 0, 1, 2, 3, 4
    i++;
  } while (i < 5);
  ```

- **for-in 循环**：用于遍历对象的属性
  ```javascript
  let person = { name: "John", age: 30, city: "New York" };
  
  for (let key in person) {
    console.log(`${key}: ${person[key]}`);
  }
  ```

- **for-of 循环**：用于遍历可迭代对象（如数组、字符串等）
  ```javascript
  let fruits = ["apple", "banana", "orange"];
  
  for (let fruit of fruits) {
    console.log(fruit); // "apple", "banana", "orange"
  }
  ```

## 函数

函数是封装了一段可重复执行的代码块，通过调用函数来执行这段代码。

### 函数声明

```javascript
function add(a, b) {
  return a + b;
}

let result = add(5, 3);
console.log(result); // 8
```

### 函数表达式

```javascript
let add = function(a, b) {
  return a + b;
};

let result = add(5, 3);
console.log(result); // 8
```

### 箭头函数（ES6+）

```javascript
let add = (a, b) => a + b;

let result = add(5, 3);
console.log(result); // 8
```

### 函数参数

- **默认参数**（ES6+）
  ```javascript
  function greet(name = "World") {
    console.log(`Hello, ${name}!`);
  }
  
  greet(); // "Hello, World!"
  greet("John"); // "Hello, John!"
  ```

- **剩余参数**（ES6+）
  ```javascript
  function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
  }
  
  console.log(sum(1, 2, 3)); // 6
  console.log(sum(1, 2, 3, 4, 5)); // 15
  ```

### 函数作用域

- **全局作用域**：在函数外部声明的变量，在整个程序中都可以访问
- **函数作用域**：在函数内部声明的变量，只能在函数内部访问
- **块级作用域**：使用 `let` 或 `const` 声明的变量，只能在块（`{}`）内部访问

## 对象

对象是 JavaScript 中的核心概念，它是一组键值对的集合。

### 对象创建

- **对象字面量**
  ```javascript
  let person = {
    name: "John",
    age: 30,
    city: "New York",
    sayHello: function() {
      console.log(`Hello, my name is ${this.name}`);
    }
  };
  ```

- **构造函数**
  ```javascript
  function Person(name, age, city) {
    this.name = name;
    this.age = age;
    this.city = city;
    this.sayHello = function() {
      console.log(`Hello, my name is ${this.name}`);
    };
  }
  
  let person = new Person("John", 30, "New York");
  ```

- **Object.create()**
  ```javascript
  let personProto = {
    sayHello: function() {
      console.log(`Hello, my name is ${this.name}`);
    }
  };
  
  let person = Object.create(personProto);
  person.name = "John";
  person.age = 30;
  person.city = "New York";
  ```

### 对象属性访问

```javascript
let person = { name: "John", age: 30 };

// 点表示法
console.log(person.name); // "John"

// 方括号表示法
console.log(person["age"]); // 30

// 动态属性名
let propName = "name";
console.log(person[propName]); // "John"
```

### 对象方法

对象的方法是函数类型的属性：

```javascript
let person = {
  name: "John",
  age: 30,
  
  // 普通方法
  sayHello: function() {
    console.log(`Hello, my name is ${this.name}`);
  },
  
  // 箭头函数方法（注意：箭头函数没有自己的 this）
  getAge: () => {
    return this.age; // 这里的 this 指向全局对象
  }
};

person.sayHello(); // "Hello, my name is John"
```

## 数组

数组是用于存储多个值的有序集合。

### 数组创建

- **数组字面量**
  ```javascript
  let numbers = [1, 2, 3, 4, 5];
  let fruits = ["apple", "banana", "orange"];
  ```

- **构造函数**
  ```javascript
  let numbers = new Array(1, 2, 3, 4, 5);
  let fruits = new Array("apple", "banana", "orange");
  ```

### 数组访问

```javascript
let fruits = ["apple", "banana", "orange"];

console.log(fruits[0]); // "apple"
console.log(fruits[1]); // "banana"
console.log(fruits[2]); // "orange"
console.log(fruits.length); // 3
```

### 数组方法

JavaScript 提供了许多内置的数组方法：

- **添加/删除元素**：`push()`, `pop()`, `shift()`, `unshift()`, `splice()`
- **数组遍历**：`forEach()`, `map()`, `filter()`, `reduce()`, `find()`, `findIndex()`
- **数组转换**：`join()`, `split()`, `toString()`, `toLocaleString()`
- **数组排序**：`sort()`, `reverse()`
- **数组检测**：`includes()`, `indexOf()`, `lastIndexOf()`
- **数组合并**：`concat()`, `...`（扩展运算符）

### 示例

```javascript
let numbers = [1, 2, 3, 4, 5];

// 添加元素到末尾
numbers.push(6); // [1, 2, 3, 4, 5, 6]

// 删除末尾元素
numbers.pop(); // [1, 2, 3, 4, 5]

// 遍历数组
numbers.forEach((num) => {
  console.log(num); // 1, 2, 3, 4, 5
});

// 数组映射
let doubled = numbers.map((num) => num * 2); // [2, 4, 6, 8, 10]

// 数组过滤
let evenNumbers = numbers.filter((num) => num % 2 === 0); // [2, 4]

// 数组归约
let sum = numbers.reduce((total, num) => total + num, 0); // 15
```

## 最佳实践

1. **使用 `let` 和 `const` 代替 `var`**：避免变量提升和函数作用域带来的问题
2. **使用严格模式**：在脚本开头添加 `"use strict"`，提高代码质量
3. **避免全局变量**：减少全局变量的使用，避免命名冲突
4. **使用驼峰命名法**：变量名、函数名使用驼峰命名法
5. **使用箭头函数**：简化函数语法，避免 `this` 指向问题
6. **使用模板字符串**：简化字符串拼接
7. **使用解构赋值**：简化变量赋值
8. **使用默认参数**：提高函数的健壮性
9. **使用剩余参数和扩展运算符**：简化函数调用和数组操作
10. **使用 `===` 代替 `==`**：避免类型转换带来的问题

## 参考资源

- [MDN Web Docs - JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [JavaScript 高级程序设计（第 4 版）](https://book.douban.com/subject/35175321/)
- [你不知道的 JavaScript（上卷）](https://book.douban.com/subject/26351021/)
