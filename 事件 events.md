# 什么是事件

事件是在编程时系统内发生的动作或者发生的事情——系统会在事件出现时产生或触发某种信号，并且会提供一个自动加载某种动作（例如：运行一些代码）的机制，比如在一个机场，当跑道清理完成，飞机可以起飞时，飞行员会收到一个信号，因此他们开始起飞。

在 Web 中, 事件在浏览器窗口中被触发并且通常被绑定到窗口内部的特定部分 — 可能是一个元素、一系列元素、被加载到这个窗口的 HTML 代码或者是整个浏览器窗口。举几个可能发生的不同事件：

- 用户在某个元素上点击鼠标或悬停光标。
- 用户在键盘中按下某个按键。
- 用户调整浏览器的大小或者关闭浏览器窗口。
- 一个网页停止加载。
- 提交表单。
- 播放、暂停、关闭视频。
- 发生错误。

一个简单的点击事件：

```html

<button>Change color</button>
```

```js
const btn = document.querySelector('button')

function bgChange() {
  const rndCol = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  document.body.style.backgroundColor = rndCol
}

btn.onclick = bgChange //按钮被点击时，执行bgChange函数改变背景色
```

# `addEventListener()`

`addEventListener()`的工作原理是将实现`EventListener`的函数或对象添加到调用它的`EventTarget`上的指定事件类型的事件侦听器列表中。

- 用`addEventListener()`改写之前的点击事件代码：

```js
const btn = document.querySelector('button');

function bgChange() {
  const rndCol = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
  document.body.style.backgroundColor = rndCol;
}

btn.addEventListener('click', bgChange);
```

可以看到，在 `addEventListener()` 函数中，有了两个参数——事件名称和回应事件的函数代码。与之对应的，有了 `removeEventListener()`
方法来移除事件监听器。这让 `addEventListener()` 在复杂、大型的项目中非常高效，比如可以在一个元素上多次调用 `addEventListener()` ,在第二个参数中指定不同的函数。

# 事件冒泡与捕获

事件冒泡和捕捉是两种机制，主要描述当在一个元素上有两个相同类型的事件处理器被激活会发生什么。

当一个事件发生在具有父元素的元素上时，现代浏览器运行两个不同的阶段 - 捕获阶段和冒泡阶段。 在捕获阶段：

- 浏览器检查元素的最外层祖先<html>，是否在捕获阶段中注册了一个onclick事件处理程序，如果是，则运行它。
- 然后，它移动到<html>
  中单击元素的下一个祖先元素，并执行相同的操作，然后是单击元素再下一个祖先元素，依此类推，直到到达实际点击的元素。

在冒泡阶段，恰恰相反：

- 浏览器检查实际点击的元素是否在冒泡阶段中注册了一个onclick事件处理程序，如果是，则运行它。
- 然后它移动到下一个直接的祖先元素，并做同样的事情，然后是下一个，等等，直到它到达<html>元素。

![bubbling-capturing](images/bubbling-capturing.png)
根据上图，引入一个容易理解的例子：

```html
<!--有一个包含了<video>的<div>默认是隐藏状态-->
<button>Display video</button>

<div class="hidden">
  <video>
    <source src="rabbit320.mp4" type="video/mp4">
  </video>
</div>
```

```js
btn.onclick = function () {
  videoBox.setAttribute('class', 'showing');
}
//button 元素按钮被点击时，<div>由 hidden 变为 showing
videoBox.onclick = function () {
  videoBox.setAttribute('class', 'hidden');
};
//<div> 被点击时，再次隐藏
video.onclick = function () {
  video.play();
};
//<video>被点击时，视频开始播放
```

可以发现，如果点击按钮，`<video>`会从隐藏变为显示，但是当点击`<video>`，想让视频播放时，同时导致了`<div>`被隐藏。

这是因为在默认情况下，所有事件处理程序都在冒泡阶段进行注册。因此，在示例中，当单击视频时，这个单击事件从 `<video>`元素向外冒泡直到`<html>`元素。沿着这个事件冒泡线路：

- 它发现了`video.onclick`...事件处理器并且运行它，因此这个视频`<video>`第一次开始播放。
- 接着它发现了（往外冒泡找到的） `videoBox.onclick`...事件处理器并且运行它，因此这个视频`<video>`
  也隐藏起来了。

## `stopPropagation()`

`stopPropagation()`用来阻止捕获和冒泡阶段中当前事件的进一步传播。所以上述例子可以在`video.onclick`中用此函数解决问题：

```js
video.onclick = function (e) {
  e.stopPropagation()
  video.play();
};
```

这样，事件不会向上冒泡，自然不会触发隐藏`<div>`的点击事件。

- 但是，此方法不能防止任何默认行为的发生； 例如，对链接的点击仍会被处理；scroll 事件不可阻止默认动作。
- 要阻止默认行为，可以使用`preventDefault()`

## 回看`addEventListener()`

理解了冒泡与捕获后，可以引入理解 `addEventListener()`的第三个参数：`useCapture`

- 不传、默认值为 false：先进行事件冒泡
- true：先进行事件捕获

# 事件委托

事件冒泡允许我们使用**事件委托**，比如：如果想要在大量子元素中单击任何一个都可以运行一段代码，您可以将事件监听器设置在其父节点上，并让子节点上发生的事件冒泡到父节点上，而不是每个子节点单独设置事件监听器。

例子：如果想让每一项`<li>`被点击时弹出信息，可以将 click 单击事件监听器设置在`<ul>`上，点击事件会从`<li>`冒泡到`<ul>`上，而不必给每一项`<li>`都设置一个监听器。

```html

<ul id="parent-list">
  <li id="post-1">Item 1</li>
  <li id="post-2">Item 2</li>
  <li id="post-3">Item 3</li>
  <li id="post-4">Item 4</li>
  <li id="post-5">Item 5</li>
  <li id="post-6">Item 6</li>
</ul>
```

```js
document.getElementById("parent-list").addEventListener("click", function (e) {
  if (e.target && e.target.nodeName == "LI") {
    console.log("List item ", e.target.id.replace("post-", ""), " was clicked!");
  }
});
```

# 参考链接

- [事件介绍](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events)