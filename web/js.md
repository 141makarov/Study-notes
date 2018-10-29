# js
## 两种方式
### <script>
	alert(yo);
	...
	...
</script>
### <script src="main.js"></script>
## 数据类型
### Number  数值
* 123 //整型
* 1.2 //浮点
* -1 //负数
* 1.2e4   //12000
* NaN  //Not a number
* Infinity    //无限大
### String  字符串
* “王花花”
* '王花花'
* '王花花说： "你好"'(外边单引号，里边要双引号)
* 转义'\'  'he\'s'
* `
hello
world
`
### Boolean 布尔值
* true 
* false
### Array  数组
> 各元素并列，是简单的集合
> 

* 字符串
* 数值
* 布尔型
* 对象
### Object 对象
* var o = {
    a: 1,
    b: 2
}

var x = o.a + o.b
### console.log(typeof bag)
## 控制流
### var isAdmin = false;
isAdmin = 0;
isAdmin = '';
isAdmin = NaN;
isAdmin = null;   //空
isAdmin = undefined;   //未定义

if(isAdmin)
    console.log('他是管理员');
else
    console.log('他不是管理员')
### if(今天星期一){
    //...
}else if (今天星期二){
    //...
} else if(今天星期三){
    //...
}
### var day = 1;
switch (day) {
    case 1:
    //...
    console.log('今天吃牛肉面');
    break;
    case 2:
    //...
    console.log('今天吃米饭');
    break;
    case 3:
    //...
    console.log('今天吃臊子面');
    break;
    default:
    console.log('今天吃火锅');
    break;
}
## 运算符
### + - * /   (只有+可以连接字符串)
### % 求余
### ++ 自加     --自减
### > < >=  <=
### = 赋值
### == 判断是否相等
### === 判断是否相等（严格模式）
### ！= 不等于
### +=    -=     *=           /=
### &&     ||
## 循环
### /*
var i;
for(i=1;i <= 100;i++){
    console.log(i)
}
*/

var result = [
    '百度一下，你就知道',
    '百度百科',
    '百度网盘',
    '百度软件中心'
]

for(i=0;i<result.length;i++){
    console.log(result[i])
}
### var attempt = 0;
while (attempt < 5){ //括号内不能是1或者true，否则会一直循环下去
    //继续尝试...
    attempt++;
    console.log(attempt)
}
console.log('loop stopped');

## 函数
### 形式
* function f() {
    ...
    ...
}

f()
### 优点
* 代码封装
* 控制数据流
    * function buy(money) {
    if(!money){
        alert('警察叔叔就是这个人')
    }else {
        alert('您好')
    }

}

buy()
* 解决作用域污染问题
    * ;()();

//第二个括号是触发用的，真正的代码内容写在function里，
//变量定义在函数体里边，无论怎么定义都是局部变量，不会污染全局变量，作用域污染问题解决
//function是匿名函数，把所有代码都写在function里边
;(function () {
    //...
    //...
})();
### function add(a,b) {
    return a+b

}

function sub(a,b) {
    return a-b

}

function mul(a,b) {
    return a*b

}

function div(a,b) {
    return a/b

}

var x1 = add(1,6);
var x2 = sub(8,1);
var x3 = mul(1,7);
var x4 = div(7,1);
console.log("x1: ",x1);
console.log("x2: ",x2);
console.log("x3: ",x3);
console.log("x4: ",x4);
## 闭包
### function user(name) {
    var age, sex;
    return{
        getName: function () {
            return name;
        },
        setName: function (newName) {
            name = newName;
        },
        getAge: function () {
            return age;
        },
        setAge: function (newAge) {
            age = newAge;
        },
        getSex: function () {
            return sex;
        },
        setSex: function (newSex) {
            sex = newSex;
        }
    }
}


var whh = user('王花花');
whh.setAge(22);
whh.setSex('女');
var name = whh.getName();
var age = whh.getAge();
var sex = whh.getSex();
console.log(name, sex, age);
## windows下的方法和属性
### //纯提醒
alert('您的电脑中了病毒！');
### //确定某些事情
var r = confirm('您是否年满十八周岁?');
console.log("r:", r);
### //可以获取用户输入内容
var name = prompt('你叫什么名字？');
console.log("name:", name);
### setTimeout(function () {
    console.log('时间到了');
},0);
console.log('Muhaha');
console.log('yo');
### var count = 0;
var timer = setInterval(function () {
    count++;
    if(count>7){
        clearInterval(timer);
        return;
    }
    console.log("Yo " + count);
},1000)


*XMind: ZEN - Trial Version*