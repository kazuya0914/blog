jQuery 是一个高效、精简并且功能丰富的 JavaScript 工具库。它提供的 API 易于使用且兼容众多浏览器，这让诸如 HTML 文档遍历和操作、事件处理、动画和 Ajax 操作更加简单。

# 获取、选择页面元素

就如 jQuery 的宣传语 "write less, do more"一样，从使用 jQuery的第一步开始，jQuery就提供了非常简洁方便的方法来获取、选择页面元素。  
通过在构造函数 `jQuery()`（也可以简写为`$()`）中传入参数，来得到被选中的元素。

- 参数可以为CSS选择器，也可以是jQuery的特有表达式：

```js
$(document) //选择整个文档对象

$('#myId') //选择ID为myId的网页元素

$('div.myClass') // 选择class为myClass的div元素

$('input[name=first]') // 选择name属性等于first的input元素

$('a:first') //选择网页中第一个a元素

$('tr:odd') //选择表格的奇数行

$('#myForm :input') // 选择表单中的input元素

$('div:visible') //选择可见的div元素

$('div:gt(2)') // 选择所有的div元素，除了前三个

$('div:animated') // 选择当前处于动画状态的div元素
```

# 链式操作

为了将 write less, do more 更进一步发挥，在选中想要的元素后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来。比如：

```js
$('div').find('h3').eq(2).html('Hello')
```

可以分开理解为：

```js
$('div') //找到div元素

  .find('h3') //选择其中的h3元素

  .eq(2) //选择第3个h3元素

  .html('Hello'); //将它的内容改为Hello
```

这可以说是 jQuery的精髓，真正做到写得更少，做得更多。其原理是在每一步 jQuery操作后，返回的不是选择的元素，而是一个 jQuery对象，所以不同的操作可以链在一起。  
进行一个简单的类似实现：

```js
window.jQuery = function (selectorOrArray) {
  let elements
  if (typeof selectorOrArray === 'string') {
    elements = document.querySelectorAll(selectorOrArray)
  } else if (selectorOrArray instanceof Array) {
    elements = selectorOrArray
  }
  return {//返回一个匿名对象作为api来操作选中的元素
    find(selector) {
      let array = []//因为可能存在多个元素，所以声明一个空数组来存放找到的元素
      for (let i = 0; i < elements.length; i++) {//遍历每个被选择器参数选中的元素，转化为数组拼接到空数组中，
        array = array.concat(Array.from(elements[i].querySelectorAll(selector)))
      }
      return jQuery(array)//用jQuery选中这个数组再return，就能又返回匿名对象，来达到链式操作
    },
    addClass(className) {
      for (let i = 0; i < elements.length; i++) {//遍历每个元素，给每个元素添加类名
        elements[i].classList.add(className)
      }
      return this//this 指向匿名对象
    },
  }
}
jQuery('.test')
  .find('.child')
  .addClass('red')
//在class为test的元素中找到带有class为child的元素，并为它们添加class为red的标签
```

# 创建元素

用 jQuery创建新元素的方法也很简洁、直观，只要把新元素传入 jQuery构造函数就行，：

```js
$('<p>Hello</p>')

$('<li class="new">new list item</li>')

$('ul').append('<li>list item</li>')
```

# 移动元素

## 现有元素外

```js

$('p').before($('div'))//div元素移动到p元素前面,或者在p元素前添加div元素

$('p').after($('div'))//div元素移动到p元素后面，或者在p元素后添加div元素

$('div').insertBefore($('p'))

$('div').insertAfter($('p'))

```

`.before()` 和`.insertBefore()`实现同样的功能。主要的不同是语法——内容和目标的位置不同。对于`.before()`, 选择器表达式在方法的前面，参数是将要插入的内容。对于`.insertBefore()`
刚好相反，内容在方法前面，无论是作为一个选择表达式或作为标记上创建动态，它将被放在目标容器的前面。对于`.after()`和`.insertAfter()`是一样的。

## 现有元素内

```js
$('.container').append($('h2'))//把h2移动到container内,作为最后一个子元素

$('.container').prepend($('h2'))//把h2移动到container内,作为第一个子元素

$('h2').appendTo($('.container'))

$('h2').prependTo($('.container'))
```

`.prepend()`和`.prependTo()`实现同样的功能，主要的不同是语法，插入的内容和目标的位置不同。 对于`.prepend()`
而言，选择器表达式写在方法的前面，作为待插入内容的容器，将要被插入的内容作为方法的参数。而`.prependTo()`
正好相反，将要被插入的内容写在方法的前面，可以是选择器表达式或动态创建的标记，待插入内容的容器作为参数。对于`.append()`和`.appendTo()`是一样的。

# 修改元素属性

- `.attr()`获取匹配的元素集合中的第一个元素的属性的值。设置每一个匹配元素的一个或多个属性。

```js
$('em').attr('title')//在页面的第一个<em>中找到title属性

$('#greatphoto').attr('alt', 'Beijing Brush Seller')//修改或添加 id 为 greatphoto 的 alt 值（已存在就修改，不存在就添加）
```

- `.removeAttr()`匹配的元素集合中的每个元素中移除一个属性（attribute）。
- `.addClass()`为每个匹配的元素添加指定的样式类名
- `.removeClass()`同上，删除类名
- `.toggleClass()`如果存在（不存在）就删除（添加）一个类
- `.text()`得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。

```
<div class="demo-container">
      <div class="demo-box">Demonstration Box</div>
  <ul>
  <li>list item 1</li>
  <li>list <strong>item</strong> 2</li>
  </ul>
  </div>
  
$('div.demo-container').text()

Demonstration Box list item 1 list item 2
```

- `.val()`获取匹配的元素集合中第一个元素的当前值或设置匹配的元素集合中每个元素的值。

```js
let userName = $('input[name="user"]').val()//获取输入框内容
```

# 参考链接

- [jQuery设计思想](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html) ，by 阮一峰
- [jQuery API 中文文档](https://www.jquery123.com/)