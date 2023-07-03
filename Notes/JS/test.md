# 1.语法和数据类型

## 小坑

```jsx
/**
 * 例子 1
 */
var x;
console.log(x === undefined); // true
x = 3;

/**
 * 例子 2
 */
var myvar = "my value";

(function() {
  var myvar;
  console.log(myvar); // undefined
  myvar = "local value";
})();
```

这个例子中的知识点：

这段代码主要涉及以下JavaScript的知识点：

1. **变量作用域（Variable Scope）**：在JavaScript中，变量可以存在于两种作用域中：全局作用域或局部作用域。在函数外部声明的变量是全局变量，它可以在代码的任何地方使用。函数内部声明的变量具有局部作用域，它只能在声明它的函数内部使用。在这段代码中，最开始声明的 `myvar` 是全局变量，而在函数内部声明的 `myvar` 是局部变量。
2. **变量提升（Variable Hoisting）**：在JavaScript中，无论变量在哪里声明，都会被提升到其作用域的顶部。变量提升只会提升变量名，而不会提升变量的值。所以，当在声明之前访问变量时，其值会是 `undefined`。在这段代码中，虽然 `myvar` 在 `console.log` 之后被赋值，但由于变量提升，函数内的 `console.log(myvar);` 打印出来的是 `undefined`。
3. **立即执行函数表达式（Immediately Invoked Function Expression, IIFE）**：这是一种在JavaScript中定义并立即执行一个函数的方法。IIFE可以用来创建一个新的作用域，防止变量的污染。这段代码中的 `(function() {...})();` 就是一个IIFE，它创建了一个新的作用域，使得函数内部的 `myvar` 不会影响到全局的 `myvar`。
4. **赋值操作**：这段代码中的 `myvar = "my value";` 和 `myvar = "local value";` 是赋值操作，将值赋给变量。

总的来说，这段代码展示了如何在JavaScript中使用变量作用域，变量提升，IIFE以及赋值操作。

```jsx
/* 函数表达式 */

baz(); // 类型错误：baz 不是一个函数

var baz = function() {
  console.log("bar2");
};

//变量提升以后以后

var baz; // 变量提升阶段，baz 被声明，但是值是 undefined

baz(); // 这个阶段 baz 的值还是 undefined，不是一个函数，所以会报类型错误

baz = function() { // 这个阶段才对 baz 进行初始化，给它赋值一个函数
  console.log("bar2");
};
```

## 同名
在同一作用域中，不能使用与变量名或函数名相同的名字来命名常量。

```jsx
// 这会造成错误
function f() {};
const f = 5;

// 这也会造成错误
function f() {
  const g = 5;
  var g;

  //语句
}
```

## **[数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)**

- 七种基本数据类型：
    - 布尔值（Boolean），有 2 个值分别是：`true` 和 `false`.
    - null，一个表明 null 值的特殊关键字。JavaScript 是大小写敏感的，因此 `null` 与 `Null`、`NULL`或变体完全不同。
    - undefined，和 null 一样是一个特殊的关键字，undefined 表示变量未赋值时的属性。
    - 数字（Number），整数或浮点数，例如： `42` 或者 `3.14159`。
    - 任意精度的整数 (BigInt) ，可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。
    - 字符串（String），字符串是一串表示文本值的字符序列，例如："Howdy" 。
    - 代表（Symbol）( 在 ECMAScript 6 中新添加的类型).。一种实例是唯一且不可改变的数据类型。
- 以及对象（Object）。

## **[数字转换为字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#%E6%95%B0%E5%AD%97%E8%BD%AC%E6%8D%A2%E4%B8%BA%E5%AD%97%E7%AC%A6%E4%B8%B2)**

仅仅对加法运算符有这个特性，减法没有

```jsx
"37" - 7 // 30
"37" + 7 // "377"
```

## **[字符串转换为数字](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%BD%AC%E6%8D%A2%E4%B8%BA%E6%95%B0%E5%AD%97)**

### 两个函数

- `[parseInt()` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- `[parseFloat()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)`

分别处理整数和浮点数，第一个参数接受字符串，第二个参数接受进制（阿拉伯数字）

### 一元加法运算符

将字符串转换为数字的另一种方法是使用一元**加法运算符**

```jsx
"1.1" + "1.1" = "1.11.1"
(+"1.1") + (+"1.1") = 2.2
// 注意：加入括号为清楚起见，不是必需的。
```

# 2.流程控制与任务处理

## 错误的值

下面这些值将被计算出 false (also known as [Falsy](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy) values):

- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- 空字符串（`""`）

## 原始布尔值和Boolean对象

请不要混淆原始的布尔值`true`和`false` 与 `[Boolean](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean)`对象的真和假。例如：

```jsx
var b = new Boolean(false);
if (b) //结果视为真
if (b == true) // 结果视为假
```

# 3.循环与迭代

## **`[label` 语句](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration#label_%E8%AF%AD%E5%8F%A5)**

一次只能标记一个语句块，语法上和C的goto有点像。

一个label可以通过break/continue来触发，触发的时候就直接结束当前语句块

```jsx
var num = 0;
for (var i = 0 ; i < 10 ; i++) {   // i 循环
  for (var j = 0 ; j < 10 ; j++) { // j 循环
    if( i == 5 && j == 5 ) {
       break; // i = 5，j = 5 时，会跳出 j 循环
    } // 但 i 循环会继续执行，等于跳出之后又继续执行更多次 j 循环
  num++;
  }
}

alert(num); // 输出 95
```

## **[剩余参数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions#%E5%89%A9%E4%BD%99%E5%8F%82%E6%95%B0)**

格式： …name

例子：

```jsx
function multiply(multiplier, ...theArgs) {
  return theArgs.map(x => multiplier * x);
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

# 6.数字和日期

## 三个符号值

`+[Infinity](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)`（正无穷）、`-[Infinity](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)`（负无穷）和 `[NaN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)` (not-a-number，非数字)。

## 日期对象

创建一个日期对象

```jsx
var dateObjectName = new Date([parameters]);
```

不使用new将创建一个字符串，所以要创建对象得用new

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79010ffc-74d3-4446-9931-3a4cbef86fdf/Untitled.png)

前边的语法中的参数（parameters）可以是一下任何一种：

- 无参数 : 创建今天的日期和时间，例如： `today = new Date();`.
- 一个符合以下格式的表示日期的字符串："月 日，年 时：分：秒"。例如： `var Xmas95 = new Date("December 25, 1995 13:30:00")。`如果你省略时、分、秒，那么他们的值将被设置为 0。
- 一个年，月，日的整型值的集合，例如： `var Xmas95 = new Date(1995, 11, 25)`。
- 一个年，月，日，时，分，秒，【毫秒】的集合，例如： `var Xmas95 = new Date(1995, 11, 25, 9, 30, 0);`.

Date的方法

- "set" 方法，用于设置 Date 对象的日期和时间的值。
- "get" 方法，用于获取 Date 对象的日期和时间的值。
- "to" 方法，用于返回 Date 对象的字符串格式的值。
- parse 和 UTC 方法，用于解析 Date 字符串。

通过“get”和“set”方法，你可以分别设置和获取秒，分，时，日，星期，月份，年。这里有个 getDay 方法可以返回星期，但是没有相应的 setDay 方法用来设置星期，因为星期是自动设置的。这些方法用整数来代表以下这些值：

- 秒，分：0 至 59
- 时：0 至 23
- 星期：0 (周日) 至 6 (周六)
- 日期：1 至 31
- 月份：0 (一月) to 11 (十二月)
- 年份：从 1900 开始的年数

# 7.文本格式化

## 模版字符串

模板字符串使用反勾号 (` `) ([grave accent](https://en.wikipedia.org/wiki/Grave_accent)) 包裹内容而不是单引号或双引号。模板字符串可以包含占位符。占位符用美元符号和花括号标识 (`${expression}`).

```jsx
const five = 5;
const ten = 10;
console.log(`Fifteen is ${five + ten} and not ${2 * five + ten}.`);
// "Fifteen is 15 and not 20."
```

## 多行

```jsx
console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"
```

注意用的是反勾号，最简单的的写法

# 8.正则表达式

## 反斜杠消消乐

`/[a-z]:\\/i` 和 `new RegExp("[a-z]:\\\\","i")` 会创建相同的表达式，即匹配类似 "C:\" 字符串。

为什么嘞？

在JavaScript中，有两种创建正则表达式的方式：

1. 使用正则表达式字面量，如 `/pattern/flags`；
2. 使用`RegExp`构造函数，如 `new RegExp(pattern, flags)`。

这两种方式在大部分情况下都可以互换使用，但在处理特殊字符和转义字符时，有一些区别。

正则表达式字面量 `/[a-z]:\\\\/i` 中，`\\\\` 是一个转义字符，表示一个字面量的反斜杠 `\\`。这个正则表达式会匹配一个小写字母，后面跟着一个冒号和一个反斜杠，如 `"c:\\"`。

在`RegExp`构造函数 `new RegExp("[a-z]:\\\\\\\\","i")` 中，`\\\\\\\\` 也表示一个字面量的反斜杠 `\\`。这是因为在JavaScript字符串中，`\\\\` 是一个转义字符，表示一个字面量的反斜杠 `\\`。所以，`\\\\\\\\` 在字符串中表示两个字面量的反斜杠 `\\\\`，而在正则表达式中，`\\\\` 又表示一个字面量的反斜杠 `\\`。因此，这个正则表达式和上面的正则表达式是相同的。

所以，`/[a-z]:\\\\/i` 和 `new RegExp("[a-z]:\\\\\\\\","i")` 会创建相同的正则表达式，都会匹配类似 `"c:\\"` 的字符串。

# 9.索引集合类（**Indexed collections）**

## Array

三种初始化数组的方法

```jsx
// 这种方式...
const arr1 = new Array(arrayLength);

// ...与这种方式会形成相同数组
const arr2 = Array(arrayLength);

// 这个效果也一样
const arr3 = [];
arr3.length = arrayLength;
```

注意数组是可以自己设置属性的

```jsx
const arr = [];
arr[3.4] = 'Oranges';
console.log(arr.length); // 0
console.log(Object.hasOwn(arr, 3.4)); // true
```

像length就是数组自带的属性，数组允许自定义属性，不计入数组的长度，因为不属于数组的内容

## 遍历数组

### forEach()方法

```jsx
const colors = ['red', 'green', 'blue'];
colors.forEach((color) => console.log(color));
// red
// green
// blue
```

forEach()接受一个函数作为参数，会自动对数组的每一个值运用该函数

### forEach VS map

JavaScript数组的`forEach`方法和`map`方法都是用于遍历数组并对每个元素执行一个函数。然而，它们的主要区别在于它们如何处理函数的结果。

- `forEach`方法只是简单地对数组中的每个元素执行函数，不返回任何值（即返回undefined）。这个方法主要用于需要遍历数组并执行一些操作，但不需要收集结果的情况，例如日志记录、推送到服务器、更新界面等。

```jsx
let arr = [1, 2, 3, 4];
arr.forEach(item => {
  console.log(item); // 输出 1, 2, 3, 4
});

```

- `map`方法也对数组中的每个元素执行函数，但它返回一个新数组，新数组的元素是原始数组中的元素通过函数处理后的结果。`map`方法不会修改原始数组。这个方法主要用于需要将一个数组转换为另一个数组的情况，例如提取对象数组的某个属性、将数字数组转换为其对应的平方数组等。

```jsx
let arr = [1, 2, 3, 4];
let squares = arr.map(item => {
  return item * item;
});
console.log(squares); // 输出 [1, 4, 9, 16]

```

总的来说，当你需要遍历数组并进行一些操作但不关心返回结果时，你应该使用`forEach`。当你需要从一个数组创建一个新数组时，你应该使用`map`。

注意：

尽管`forEach`可以修改原始数组，但并不推荐这样做，因为这可能会导致代码更难理解和维护。在很多情况下，更好的做法是使用`map`函数创建一个新的数组，而不是修改原始数组。这是函数式编程原则的一部分，即避免修改状态和可变数据。

# 10.带键集合

## **`[Object`和`Map`的比较](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Keyed_collections#object%E5%92%8Cmap%E7%9A%84%E6%AF%94%E8%BE%83)**

- `Object` 的键均为 `String` 类型，在 `Map` 里键可以是任意类型。
- 必须手动计算`Object`的尺寸，但是可以很容易地获取使用`Map`的尺寸。
- `Map`的遍历遵循元素的插入顺序。
- `Object`有原型，所以映射中有一些缺省的键。（可以用 `map = Object.create(null) 回避`）。

这三条提示可以帮你决定用`Map`还是`Object`：

- 如果键在运行时才能知道，或者所有的键类型相同，所有的值类型相同，那就使用`Map`。
- 如果需要将原始值存储为键，则使用`Map`，因为`Object`将每个键视为字符串，不管它是一个数字值、布尔值还是任何其他原始值。
- 如果需要对个别元素进行操作，使用`Object`。

# 11.使用对象

## 枚举一个对象的所有属性

- [for...in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环 该方法依次访问一个对象及其原型链中所有可枚举的属性。
- [Object.keys(o)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) 该方法返回对象 `o` 自身包含（不包括原型中）的所有可枚举属性的名称的数组。
- [Object.getOwnPropertyNames(o)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames) 该方法返回对象 `o` 自身包含（不包括原型中）的所有属性 (无论是否可枚举) 的名称的数组。

## 创建对象

### **[使用对象初始化器](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_objects#%E4%BD%BF%E7%94%A8%E5%AF%B9%E8%B1%A1%E5%88%9D%E5%A7%8B%E5%8C%96%E5%99%A8)**

```jsx
var obj = { property_1:   value_1,   // property_# 可以是一个标识符...
            2:            value_2,   // 或一个数字...
           ["property" +3]: value_3,  //  或一个可计算的 key 名...
            // ...,
            "property n": value_n }; // 或一个字符串
```

这里 `obj` 是新对象的名称，每一个 `property_i` 是一个标识符（可以是一个名称、数字或字符串字面量），并且每个 `value_i` 是一个其值将被赋予 `property_i` 的表达式。`obj` 与赋值是可选的；如果你不需要在其他地方引用对象，你就不需要将它赋给一个变量。（注意在接受一条语句的地方，你可能需要将对象字面量括在括号里，从而避免将字面量与块语句相混淆）

### **[使用构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_objects#%E4%BD%BF%E7%94%A8%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)**

1. 通过创建一个构造函数来定义对象的类型。首字母大写是非常普遍而且很恰当的惯用法。
2. 通过 `new` 创建对象实例。

# 12.Using Classes

```jsx
class MyClass {
  // Constructor
  constructor() {
    // Constructor body
  }
  // Instance field
  myField = "foo";
  // Instance method
  myMethod() {
    // myMethod body
  }
  // Static field
  static myStaticField = "bar";
  // Static method
  static myStaticMethod() {
    // myStaticMethod body
  }
  // Static block
  static {
    // Static initialization code
  }
  // Fields, methods, static fields, and static methods all have
  // "private" forms
  #myPrivateField = "bar";
}
```

上面的JavaScript类MyClass使用了以下的知识点：

1. **构造函数 (Constructor)**: 类的构造函数是一种特殊的方法，用于创建和初始化类创建的对象。一个类只能有一个名为 "constructor" 的特殊方法。一个构造函数可以使用 "super" 关键字来调用一个父类的构造函数。
2. **实例字段 (Instance field)**: 这是类的一个属性，它在每个类的实例中都是唯一的。在这个例子中，`myField` 是一个实例字段，其值被初始化为字符串 "foo"。
3. **实例方法 (Instance method)**: 这是附加在类的实例上的一个函数。在这个例子中，`myMethod` 是一个实例方法。
4. **静态字段 (Static field)**: 静态字段是附加在类本身上的属性，而不是类的实例。在这个例子中，`myStaticField` 是一个静态字段，其值被初始化为字符串 "bar"。
5. **静态方法 (Static method)**: 静态方法是附加在类本身上的函数，而不是类的实例。在这个例子中，`myStaticMethod` 是一个静态方法。
6. **静态块 (Static block)**: 静态块允许在类的静态上下文中编写代码，这在初始化静态字段或执行其他静态设置操作时可能有用。注意，这是JavaScript的一个新特性，可能在所有环境中都不支持。
7. **私有字段 (Private field)**: 这是类的一个私有属性，只能在类的内部访问。在这个例子中，`#myPrivateField` 是一个私有字段，其值被初始化为字符串 "bar"。私有字段、方法或访问器在其名称前有一个井号 (#)。

以上所有这些元素都是定义类的组成部分，并提供了类和其实例的状态和行为。

### static

实例不能直接访问静态属性，除非你在类的实例方法中显式引用它，例如 **`MyClass.myStaticField`**。也就是说，虽然实例无法直接访问静态属性，但可以通过类名来访问。
