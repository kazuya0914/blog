# JavaScript 基本语法

## 表达式和语句

- 表达式是值、变量和运算符的组合，计算结果是值。比如：  
  `1 + 2`表达式的值是3  
  `x * y * 10`包含变量值的表达式  
  `add(1,2)`表达式的值为函数的返回值

```js
console.log(3)
3
undefined
//console.log(3)是一个函数，打印出了传入的参数3，但是返回值是undefined
```

- 语句可以包含：值、运算符、表达式、关键词和注释，通常用来改变环境（声明、赋值）  
  `let a = 1`该语句声明一个变量 a 并赋值1
- JavaScript 对大小写敏感：  
  `var a` 和 `var A`是不同的  
  `object` 和 `Object`是不同的  
  `function` 和 `Function`也是不同的
- 空格与回车大部分时候没有实际意义，编辑器也会自动格式化修正，但是`return`后面不能加**回车**

```js
function fn() {
  return 3
}

fn()
3

function fn() {
  return
  3
}

fn()
undefined         /*return后面加了回车再写3，函数返回undefined*/
```

## 标识符的规则

标识符用来命名或标识变量、函数或属性

- 标识符只能包含字母或数字或下划线（“_”）或美元符号（“$”），且**不能以数字开头**。
- 标识符与字符串不同之处在于字符串是数据，而标识符是代码的一部分。

```js
let _ = 1
let $20 = 20
let _________ = 3 /*小心被打*/
let 你好 = 'hellow'
```

## `if else` 语句

当指定条件为真，if 语句会执行一段语句。如果条件为假，则执行另一段语句。

```js
  if (条件表达式) {语句1} else {语句2}
 ```

**变态情况：**

- 多层 if...else 语句可使用 else if 从句

  ```js
  if (condition1)
    statement1
  else if (condition2)
    statement2
  else if (condition3)
    statement3
  else
    statementN
  ```

  上面的else if等价于下面的嵌套

  ```
  if (condition1)
     statement1
  else
     if (condition2)
        statement2
     else
        if (condition3)
  ```

- 一直使用语句块`{...}`是个好习惯

  ```j
  a = 1
  if (a === 2)
    console.log('a')
    console.log('a等于2')
    /*a等于2*/
  ```
  因为没有使用正确的缩进，而且没有使用语句块`{}`，if {语句1}只包含了`console.log('a')`

简捷形式——条件运算符：`condition ? exprIfTrue : exprIfFalse`

```js
function max(a, b) {
  if (a > b)
    return a
  else
    return b
}

// 等价于
function max2(a, b) {
  return a > b ? a : b

}
```

&&短路逻辑：`expr1 && expr2`

- 解释为：如果 expr1 是真，就返回 expr2，否则返回 expr1（并不会取true/false）

```js
a1 = 'Cat' && 'Dog'      // t && t returns "Dog"
a2 = false && 'Cat'      // f && t returns false
a3 = 'Cat' && false      // t && f returns false
console && console.log && console.log('hi')
```

||短路逻辑：`expr1 || expr2`

- 解释为：如果 expr1 是真，就返回 expr1，否则返回expr2

```js
o5 = 'Cat' || 'Dog'      // t || t returns "Cat"
o6 = false || 'Cat'      // f || t returns "Cat"
o7 = 'Cat' || false      // t || f returns "Cat"
a = a || 100
```

## `while for` 语句

while 语句可以在某个条件表达式为真的前提下，循环执行指定的一段代码，直到那个表达式不为真时结束循环。

```js
while (condition)
  statement
```

- 陷阱：

```js
while (a !== 1) {
  console.log(a)
  a = a + 0.1
}
// 会形成死循环，因为浮点数运算精度问题， 
```

for 语句用于创建一个循环，它包含了三个可选的表达式，这三个表达式被包围在圆括号之中，使用分号分隔，后跟一个用于在循环中执行的语句。

```
for ([初始化]; [条件表达式]；[最终表达式]){
  循环体
  }
```

```js
for (var i = 0; i < 5; i++) {
  console.log(i)
}
// 依次打印出01234，最后i的值为5，因为还要执行完循环体还要再执行依次i++
```

## `break continue`

- break 语句中止当前循环

```js
for (var i = 0; i < 10; i++) {
  if (i % 2 === 1) {
    break
  }
}

// i的值为1
```

- continue 声明终止当前循环或标记循环的当前迭代中的语句执行，并在下一次迭代时继续执行循环。

```js
for (var i = 0; i < 10; i++) {
  if (i % 2 === 1) {
    continue
  } else {
    console.log(i)
  }
}
// 分别打出02468
```

## `label`

在一条语句前面加个可以引用的标识符

```js
var a = {
  foo: 2
}
//a是一个对象
{
  foo:2
}
// foo是一个标签，值为2
```