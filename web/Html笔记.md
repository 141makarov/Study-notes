# Html
## body标签
	<body></body>
放入可见元素
## head标签
	 <head></head>
储存一些必要信息，为浏览器和搜索引擎所用，尽量不要写显示信息
## title标签
	<title></title>
 指定页面标题
## 标题标签
	<h1></h1>
可以为浏览器所渲染，概括整个页面的主题，一个页面只存在一个h1

	`<h2></h2>`
可以包含多个，块级元素，可以包含子元素，默认样式不同

	`<h3></h3>
	<h4></h4>
	<h5></h5>
	<h6></h6>`
## p标签
	 <p></p>
p标签可以嵌套子元素，甚至是自己
## div标签
	<div></div>
容纳其他元素，相当于目录，整理其他内容
## a标签
	 <a></a>
标签里可以有属性
* href  地址
* target  _self代表是在当前页打开，_blank代表在新标签页打开(原生属性)
## img标签
	<img src="网址">
	<img src="本地地址">
	<img src="dizhi"   alt="Hello">(alt为图片出错后显示的信息)
## 表标签table, 最外层，告诉浏览器要加表格
tr,   每一行
td,   一个单元格，属性对应的数据
th,   属性
thead,  表头容器
tbody  表身容器
### <!DocType html>
<html>
<body>
<table border="1">
    <thead>
    <tr>
        <th>
            Name
        </th>
        <th>
            Mood
        </th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
            Wang Huahua
        </td>
        <td>
            :)
        </td>
    </tr>    <tr>
        <td>
            Li Ming
        </td>
        <td>
            :D
        </td>
    </tr>
    </tbody>
</table>
</body>
</html>
* 
## header/footer标签
	 <header></header>
* 存放标题相关的，概括整个页面的内容
    * <h1></h1>大标题
    * <small></small>副标题
	 <footer></footer>
* 指定页脚
### <h1> 水平线

<meta charset="utf8">

<html>

<body>

<header>

 <h1>

  Hello World!

 </h1>

<small>你好，世界！</small>

<hr>

</header>

Our diurnal existence is divided into two phases, as distinct as day and night.

We call them work and play. We work so many hours a day.

And, when we have allowed the necessary minimum for such activities as eating and shopping, the rest we spend in various activities which are known as recreations, an elegant word which disguises the fact that we usually do not even play in our hours of leisure,

but spend them in various forms of passive enjoyment or entertainment―not playing football but watching football matches；not acting but theatre-going；Not walking but riding in a motor coach.

<footer>

<hr>

Contact | Terms | Privacy |About

</footer>

</body>

</html>



## link/script标签
	 <link>
* 加载.css文件
	 <script></script>
* 加载.js文件
 <meta charset="utf8">
<title>test</title>
<html>
<head>
   <link href="index.css">
   <script src="main.js"></script> //如果对js依赖很大，就放在<head>里
</head>
<body>
<script src="main.js"></script>   //main.js文件太大，放在<head>不合适，对js依赖不是特别大，可以放在最后
</body>
</html>
## button标签

	<button></button>
 此时button意义就是触发表单提交
* <form>
username:<input><br>
password:<input><br>
<button>Signup</button>
</form>
只有一个button标签的时候
只能和js结合，产生一定的功能
## abbr标签
	 <abbr></abbr>
### 缩略词标签
	 <abbr title="Hyper Text Markup Language">HTML</abbr>is cool!
## code、pre标签
	<code></code>
	 <pre></pre>
 code行元素，pre块级元素
### 优点
* 代码都是等宽字体，更容易编排
* 不用单独指定类或者id再去添加样式
### <meta charset="utf8">
<title>test</title>
<html>
<head>
   <style media="screen">
  code{
  background: rgba(0,200,0,.3);
 border-radius: 3px;
  } pre{
  background: rgba(0,200,0,.3);border-radius: 3px;
 }
   </style>
</head>
<body>
If variable<code>$a==1</code>
If <code>$b == 2</code>
...
...
e.g.
<pre>
if($a == 1){
    ...
    ...
    }
</pre>
...
...
</body>
</html>
