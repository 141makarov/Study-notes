# CSS引入方式 #
（最常用）在<head>元素下引入

    <link //rel="stylesheet" href="xx.css">

在CSS文件中导入

	 @import url(xx.css) 

（语句需写在css文件的开头）

在style元素下写样式

	<style //>...</style> 

在元素标签里直接设定

	 <p //style="color: red"></p>

# 元素选择器 #
HTML中元素 `<p></p>`，在CSS中选中该元素改变样式
	 p{...}
#  类选择器与ID选择器 #
## 类选择器 ##
	 <div// class = "a"></div>
	CSS中用“.”号选中该类【 .a{...} 】
	若某元素同时属于多个类 eg. <div// class = "a" class = "b"></div>
	CSS中用紧挨着多个“.”号选中【 .a.b{...} 】（若之间有空格如.a .b则含义为选中类a下的类b元素）
## ID选择器 ##
	eg. <div// id = "a"></div>
	CSS中用“#”号选中 【 #a{...} 】
# 属性选择器 #
	eg. <button// title= "abc"></button>
1)用“【xx】”选中含有xx属性的元素

【 【title】{...} 】

2)用“ 【xx="yy"】 ”选中xx属性为"yy"的元素

【 【title="abc"】{...} 】

3)用“ 【xx^="yy"】 ”选中xx属性最前面一部分内容为"yy"的元素

【 【title^="a"】{...} 】

4)用“ 【xx$="yy"】 ”选中xx属性最后面一部分内容为"yy"的元素

【 【title$="c"】{...} 】

# 后代选择器 #
CSS中用空格隔开的类选择器选中某元素的某后代元素

	eg. 选中类a下所有的类b后代：【 .a .b{...} 】
	用“*”表示某元素的所有后代元素（单独“*”号则代表页面中所有元素）
	【 .a * {...} 】**
# 相邻选择器及通用相邻选择器 #
1）用“+”来选择紧接在某元素后的一个元素（二者要有相同的父元素）
eg.选择类a的后一个相邻的兄弟div：【 .a + div {...} 】

2）用“~”来选择紧接在某元素后的所有元素（二者要有相同的父元素）
eg.选择类a后面所有的兄弟div：【 .a ~ div {...} 】
# 伪类 #
    【 a:link {...} //未访问过的链接 】
	【 a:visited {...} //已访问过的链接 】
	【 a:hover {...} //鼠标移动到链接上 】
	【 a:active {...} //鼠标点击链接瞬间 】
	【 input:focus {...} //鼠标选中输入框 】
（ps： a:hover 必须被置于 a:link 和 a:visited 之后，a:active 必须被置于 a:hover 之后）
# 伪元素 #
用“:”或“::”来选择某伪元素<br>
常用伪元素eg.<br>
【 p:first-leter {...} //段落的首字母 】<br>
【 h1:before {content:"xx";} //在h1元素前插入内容“xx”】<br>
【 h1:after {content:"xx";} //在h1元素后插入内容“xx”】<br>

# 选择器权重 #
style属性（内联） > ID选择器 > 类选择器/属性选择器/伪类选择器 > 元素选择器
# 字体属性 #
常用举例：<br>
字体类型<br>

	【 font-family: "微软雅黑", "Microsoft Yahei"; 】

（用","隔开多个值将会从前往后找，直到找到匹配字体，找不到则为默认字体）<br>
字体粗细（字重）

	【 font-weight: xx(100~900之间的一个值); 】

字体大小

	【 font-size: 1**x / xx%(母元素的百分比大小); 】
# 文字属性 #
常用举例：
对齐方式

	【 text-align: left(左对齐)/right(右对齐)/center(居中)/justify(两段对齐); 】
行高

	【 line-height: 1.3(文字倍数)/ 10px(像素表示); 】
文字装饰

	【 text-decoration: underline(下划线)/overline(上划线)/line-through(删除线); 】

#  display属性 #
显示为块级元素（与母元素同宽，padding填充上下有效）

	【 display: block; 】
显示为行内元素（可随别的元素浮动，padding填充上下无效）

	【 display: inline; 】
显示为行内块元素（既具有块级元素属性又可浮动）

	【 display: inline-block; 】
# 框 #