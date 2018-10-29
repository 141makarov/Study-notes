# jQuery
## 安装
### [jQuery.com](jQuery.com)
* 复制链接地址
    * <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
### [https://www.bootcdn.cn/](https://www.bootcdn.cn/)
* 将jquery.js文件保存为本地文件
    * <script src="jQuery.js"></script>
## 选择器
### js与jquery对比
* <div id="a">A</div>
<div id="b">B</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
* document
    .getElementById('a')
    .style
    .background = 'blue';
* //jQuery('#b')
$('#b')
    .css('background','green');
### 元素选择器
* $('div')
    .css('color','gray');
### id选择器
* $('div')
    .css('color','gray');
$('#a')
    .css('background','pink');
### 类选择器
* <div id="a">A</div>
<div id="b" class="b">B</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
* $('div')
    .css('color','gray');

$('#a')
    .css('background','pink');

$('.b')
    .css('background','blue')
### 选择器的组合
* <div id="a">A
<p>
    A1
</p>
</div>
<div id="b" class="b">B</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
* $('div')
    .css('color','gray');
$('#a ')
    .css('background','pink');

$('#a p')
    .css('border','2px solid black');

$('.b')
    .css('background','blue')
### 属性选择器
* <div id="a">A
<p>
    A1
</p>
</div>
<div id="b" class="b">B</div>
<input type="number">
<br>
<input type="text">
<script src="jQuery.js"></script>
<script src="main.js"></script>
* $('div')
    .css('color','gray');
$('#a ')
    .css('background','pink');

$('#a p')
    .css('border','2px solid black');

$('.b')
    .css('background','blue');

$('input[type="number"]')
    .css('background','yellow');
### 伪类选择器
* $('div')
    .css('color','gray');

$('div:first')
    .css('border','5px solid red');

$('#a ')
    .css('background','pink');

$('#a p')
    .css('border','2px solid black');

$('.b')
    .css('background','blue');

$('input[type="number"]')
    .css('background','yellow');
## 过滤器
### <style>
    div{
        padding: 5px;
        margin-bottom: 2px;
        background: rgba(0,0,0,.1);
    }
</style>
<div class="grandpa">
    <div class="pa">
        <div id="child1" class="child"></div>
        <div id="child2" class="child"></div>
    </div>
</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
* $('div')
    .find('.child')
    .css('border','2px solid #999')
* $('grandpa')
    .find('.child')
    .css('border','2px solid #999');
* $('#child1')
    .parent()
    .css('border','2px solid #666');
* $('#child1')
    .parents('.grandpa')
    .css('border','2px solid #666');
* 概要: 从上往下找
* 概要: 从下往上找
### <style>
    div{
        padding: 5px;
        margin-bottom: 2px;
        background: rgba(0,0,0,.1);
    }
</style>
<div class="grandpa">
    <div class="pa">
        <div id="child1" class="child not-gay"></div>
        <div id="child2" class="child"></div>
        <div id="child3" class="child"></div>
    </div>
</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
* $('.child')
    .filter('.not-gay')
    .css('background','red');
## 操作样式
### 加入多个样式的方法
* <div class="a">A</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
    * $('.a')
    .css({
        color:'black',
        background:'red',
        border: '1px solid black' ,
    });
    * 如果属性含有‘-’，有两种方式解决
        * background-color
        * 方法一：驼峰命名法
backgroundColor:'red'
        * 方法二：加引号作为字符串形式
'background-color':'red'
* 不在.js中写入类，在.html中写入类，在.js文件中引入
    * <style>
.black{
    background: #000;
    color: #fff;
}
</style>
<div class="a">A</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
        * var a = $('.a')
    .addClass('black')
    .removeClass('b')
   ;
console.log(a.hasClass('black'));
console.log(a.hasClass('b'));
            * a.hide();
a.show();
a.fadeOut();
a.fadeIn(1000);
a.slideUp(1000);
a.slideDown(1000);
### 举例
* <html>
<meta charset="utf8">
<style>
#board{
    background: #000;
    padding: 5px;
    font-family: sans-serif;
}
#board.active{
    color: red;
}
</style>
<div id="board">Hello World!</div>
<script src="jQuery.js"></script>
<script src="main.js"></script>
</html>
    * var board = $('#board');

function toggle() {
    if(board.hasClass('active')){
        board.removeClass('active');
    }else{
        board.addClass('active');
    }
}

setInterval(toggle,200);
## 分支主题 5
## 分支主题 6

*XMind: ZEN - Trial Version*