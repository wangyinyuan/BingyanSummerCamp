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
