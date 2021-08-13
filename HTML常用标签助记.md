# `<a>`

## 属性

- `href`  
  `href` 属性是全称 hyper reference超级引用的简写
- `target`  
  `target="_blank"` 在新窗口打开网页
- `download`  
  可下载，但很多浏览器不支持
- `rel=noopener`

### `<a>` 的 href取值

- 网址  
  https://google.com  
  http://google.com  
  //google.com
    - `//` 的优先级最高，他会自动选择使用 https 还是 http 协议。  
      用本地文件 index.html 中添加 `<a href="//google.com">谷歌</a>`会发现，在 chrome中通过 F12→network→勾选 preserve log会发现，//地址会继承
      http，（这里的http一般是继承了 localhost端口或者 http-server给出的IP）访问 http://google.com，
      然后重定向到 http://www.google.com，然后再重定向到 https://www.google.com。

- 路径  
  /a/b/c以及 a/b/c
    - 如果在当前目录开启了 http 服务，那么当前目录就变成了**根目录**，所以可以使用绝对路径。  
      相反，如果直接双击打开 index.html，再点击里面的 a 链接，由于协议是 file 不是 http，所以根目录会是 /c/Users/用户名，里面当然没有 /a/b/c。  
      所以一定不要双击打开 index.html

  index.html 以及 ./index.html
- 伪协议  
  javascript:代码;
    - 一个什么都不做的 a 标签 `<a href="javascript:;">查看</a>`

  mailto:邮箱  
  tel:手机号

### `<a>` 的 target取值

- _blank  
  在新窗口打开页面
- _top  
  当前链接所有 iframe 标签最上面的窗口打开
- parent  
  当前链接所在 iframe 的上一层打开
- self  
  默认值，在当前窗口打开页面
- window.name  
  比如 `target=x`，则会新建一个 window.name 为 x 的窗口打开

# `<table>`

## 标签

`<table>` 里只能包含下面三个标签，如果直接在里面写 `<tr> <td>`，浏览器会直接生成 `<tbody>`标签包住刚才的 `<tr> <td>`

- `<thead>`
- `<tbody>`
- `<tfoot>`
    - `<tr>` row行
        - `<th>` 表头单元格
        - `<td>` 表格数据

```html

<table>
    <thead>
    <tr>
        <th></th>
        <th>小红</th>
        <th>小明</th>
        <th>小王</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>语文</th>
        <td>88</td>
        <td>98</td>
        <td>100</td>
    </tr>
    <tr>
        <th>数学</th>
        <td>99</td>
        <td>87</td>
        <td>90</td>
    </tr>
    <tr>
        <th>英语</th>
        <td>95</td>
        <td>80</td>
        <td>97</td>
    </tr>
    </tbody>
    <tfoot>
    <tr>
        <th>总分</th>
        <td>282</td>
        <td>265</td>
        <td>287</td>
    </tr>
    </tfoot>
```

一个完整的表格不应该只使用 `<tr>` 和 `<td>`，

## 属性

- `table-layout`
    - `auto`  
      大多数浏览器采用自动表格布局算法对表格布局。表格及单元格的宽度取决于其包含的内容。
    - `fixed`  
      表格和列的宽度通过表格的宽度来设置，某一列的宽度仅由该列首行的单元格决定。在当前列中，该单元格所在行之后的行并不会影响整个列宽。
- `border-collapse`
    - `collapse` 合并间隙

# `<img>`

`<img src="" alt="">`的作用是发出 get 请求，展示一张图片

## 属性

- `alt` alternative 可替代的  
  一般写一些文字描述，在图片加载失败时，可以告诉用户此图片的相关信息
- `height` & `width`  
  只写高度，宽度会自适应；只写宽度，高度会自适应。两者都写死会使图片失去原有宽高比而变形，这是绝对不应该发生的。

## 事件

- `onload`
- `onerror`  
  JavaScript 中用于监听图片是否加载成功，可用于在图片加载失败的时候进行挽救。

```js
image.onload = function () {
  console.log("图片加载成功")
};
image.onerror = function () {
  console.log("图片加载失败")
  image.src = "/404.png"
}
```

## 响应式

一句话搞定`max-width:100%`

# `<form>`

`<form>`的作用是发起 get 或 post 请求，然后刷新页面

## 属性

- action  
  `<form action="/xxx"></form>`处理表单提交的 URL
- method  
  `<form action="/xxx" method="POST"></form>`可以定义用 get 还是 post 来提交
- autocomplete  
  用于指示 input 元素是否能够拥有一个默认值，此默认值是由浏览器自动补全的。
    - off：浏览器可能不会自动补全条目
    - on：浏览器可自动补全条目

## 事件

- onsubmit 监听提交事件  
  一个 form 表单必须含有一个`type="submit"`的 input 或 button。  
  相较于 input，button 里可以有任何标签比如`<strong>`和`<img>`，而 input 中不行，只能通过`"value="`更改按钮文本。