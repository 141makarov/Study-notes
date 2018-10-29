# CSS
## 四种方式
> ！important优先级最高，一般不用
> 

### 内嵌式
*     <style>
        ...
    </style>
    * 直接引入
### 链接式
* <link rel="stylesheet" href="index.css">
    * 最灵活，外部样式表引入
### @import url(test.css)
* 先引入css文件，在文件中用import，一般写在文件开始
### <p style="color: red">abc</p>
* 权限最高，最不灵活，优先级最高
## 选择器
### 类选择器 class
* <body>
    <p class="red bold">A</p>
    <p class="red">A</p>
    <div class="red bold">A</div>
    <p class="green">A</p>
    <p class='red'>
        <span class="bold">A</span>
    </p>
</body>
* .red{
    color: red;
}

.green{
    color: green;
}

.bold{
    font-weight: 900;
}

.red.bold{
    border: 1px solid rosybrown;
}

.red .bold{
    border: 1px solid rosybrown;
}
### ID选择器 id
* <body>
    <p id="logo">LOGO</p>
    <p id="footer">FOOTER</p>
</body>
* #logo{
    color: gray;
}

#footer{
    color: aqua;
}
### 属性选择器
* <body>
    <button title="点击此处登陆">登陆</button>
    <button>注册</button>
    <input type="submit">
    <br/>
    <br/>
    <input type="text">

    <a href="http://abc.com/gh/hhj">self</a>
    <a href="http://efg.com">efg</a>
    <a title="进入百度" href="http://baidu.com">百度</a>
</body>
* [title^="点击"]{
    color: gray;
    border: 1px dashed #000;
}

a[href]{
    color: red;
}

a[href^="http://abc.com"]{
    color: green;
}

.button,
input[type="submit"]{
    border: 0;
}

input[type="text"]{
    width: 50%;
    padding: 20px;
}
### 后代选择器
* <body>
    <div class="a">a
        <div class="b">b
            <div class="c">c1
            </div>
            <div class="c">c2
            </div>
            <span class="c">SPAN</span>
            <div >lorem</div>
        </div>
    </div>
</body>
* div{
    padding: 10px;
    background: rgba(255,0,0,.2);
}

.a .b .c{
    border: 2px solid bisque;
}

* <body>
    <div class="a">a
        <div class="b">b
            <div class="c">c1
                <div>
                    <div class="c">c1</div>
                </div>
            </div>
            <div class="c">c2
            </div>
            <span class="c">SPAN</span>
            <div >lorem</div>
        </div>
    </div>
</body>
### 相邻选择器
* <body>
    <div class="a">a</div>
    <div class="b">b</div>
    <div class="c">c</div>
</body>
* div{
    min-height: 50px;
    background: rgba(0,0,0,.1);
    margin: 10px;
}

.a + div{
    background: rgba(255,0,0,.3);
}
 #相邻选择器
* div{
    min-height: 50px;
    background: rgba(0,0,0,.1);
    margin: 10px;
}

.a + div{
    background: rgba(255,0,0,.3);
}

.a ~ div{
    background: rgba(0,255,0,.3);
} #通用相邻选择器
### 伪类选择器
* <body>
    <a href="http://baidu.com">百度</a>
    <br/>
    <a href="http://neu.edu.com">东大</a>
    <br/>
    <a href="http://google.cn">谷歌</a>
    <br/>
    <a href="http://taobao.com">淘宝</a>
    <br/>
    <input type="text">
    <button>点我</button>
</body>
* 子主题 2a:link{
    color: green;
}

a:visited{
    color: gray;
}

button:hover,
a:hover{
    background: #888;
}

button:active,
a:active{
    background: #333;
    color: #fff;
}

input:focus{
    outline: none;
    background: #aaa;
}
### 伪元素选择器
* <body>
    <div>
        <p>1</p>
        <p>2</p>
        <p>3</p>
    </div>
    <a class="help">什么是支付密码</a>
    <br/>
    <a class="help">什么是菜鸟驿站</a>
    <br/>
    <a class="help">什么是阿里巴巴</a>
    <br/>
    <p>Your mother is my home.</p>

</body>
* p:first-letter{
    font-size: 50px;
}

.help:before{
    content: "*";
}

.help:after{
    content: '[?]';
    color: blue;
}

/*div p:first-child{
    /*color: blue;
}*/

div p:nth-child(2){
    color: blue;
}
### 选择器权重
* 
* <body>
    <div>a</div>
    <!--/*1000*/-->
    <div style="color: lightseagreen" id="b" class="b">b</div>

</body>
* /*0100*/
#b{
    color: pink;
}

/*0010*/
.b{
    color: red;
}

/*0003*/
html body div{
    color: blue;
}

## 字体属性
### <body>
    <p>ABC abc</p>
</body>
### p{
    font-family: "微软雅黑","Microsoft YaHei UI";
    font-weight: normal;(bold / 100-900)
    font-size: 13px;(100%  /  inherit)
}
## 文字属性
### <body>
    <a href="#">click</a>
    <p>I was at a dinner in London given in honor of one of the most celebrated English military menof his time. I do not want to tell you his real name and titles. I will just call him LieutenantGeneral Lord Arthur Scoresby. I cannot describe my excitement when I saw this great andfamous man. There he sat, the man himself, in person, all covered with medals. I could not takemy eyes off him. He seemed to show the true mark of greatness. His fame had no effect onhim. The hundreds of eyes watching him, the worship of so many people did not seem to makeany difference to him.</p>
</body>
### a{
    text-decoration:none;
}
p{
    text-align: left;
    line-height: 2;
    text-decoration: line-through;
}
## display属性
### <body>
    <div class="block">
        块级元素
    </div>
    <div>
        Next

        <div style="padding: 30px" class="inline">
            行内元素
        </div>
        days later I got a chance to talk with the clergyman, and he told me more.
        </div>
        <div style="padding: 30px" class="inline-block">
            行内块元素
        </div>days later I got a chance to talk with the clergyman, and he told me more. These are hisexact words:
        <div class="block">
            恋恋笔记本
        </div>
</body>
### .block{
    display: block;
    background: #ccc;
    width: 100%;
}

.inline{
    display: inline;
}

.inline-block{
    display: inline-block;
}
## 框
### <div></div>
### div{
    width: 100px;
    height: 100px;
    background: #aaa;
    padding: 20px;
    border: 5px solid #777;
    margin: 20px;

}

*XMind: ZEN - Trial Version*