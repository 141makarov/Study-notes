# ES6
## let命令
### let遇到代码块算一个域，出了域将不再存在
* for(var i = 0;i < 5;i++){
    console.log("i:",i);
}
console.log("i:",i);
* for(let i = 0;i < 5;i++){
    console.log("i:",i);
}
console.log("i:",i);
## const命令
### 常量命名一般为大写
### 声明和赋值同时完成
### const可以指定true，1，2，字符串，对象
* let user = {name:'王花花',age:10}

const LOVE_YOU = user;
user.age=12;  //正确
LOVE_YOU = {}   // 错误
    * 指定的对象里的值可以改变，但是指向对象的指针不能改变
## 变量的解构赋值
> 在数组里顺序很重要，在对象里顺序不重要，名称很重要
> 

### 数组的解构赋值
* ES6之前：var a = 1,b = 2,c = 3;
ES6之后：var [a, b, c] = [1, 2, 3];
* var [a,...c] = [1,2,3]

console.log("a:",a);
console.log("c:",c);
* var [a, , c] = [1, 2, 3];
console.log("a:",a);
console.log("c:",c);
console.log("b:",b);

* 
var [a, , c] = [1, 2, 3];
console.log("a:",a);
console.log("b:",b);
console.log("c:",c);
* arr=[1,2,3]
var a = arr[0];
var b = arr[1];
var c = arr[2];

if(arr[3])
    var d = arr[3];
else
    var d = 'default';

console.log("a:",a);
console.log("b:",b);
console.log("c:",c);
console.log("d:",d); #ES6前
    * arr=[1,2,3]
var [a,b,c='default',d='default'] = arr;

console.log("a:",a);
console.log("b:",b);
console.log("c:",c);
console.log("d:",d); #ES6后
* arr = [1,2]
let [a,b,c] = arr;
if(typeof arr[2] === 'undefined')
     c = undefined

console.log(c)
### 对象的解构赋值
* var obj={
    a : 1,
    b : 2
}

let{a,b} = obj;  //相当于let{a:a,b:b} = obj
console.log("a:",a);
console.log("b:",b);
    * var obj={
    a : 1,
    b : 2
}

let{c,b} = obj;
console.log("c:",c);
console.log("b:",b);
* var obj={
    a : 1,
    b : 2
}

let{a:A,b} = obj;  //重命名

console.log("A:",A);
console.log("b:",b);
console.log("a:",a);

* var obj={
    a : 1,
    b : 2
}
let a; 
let{a,b} = obj;   //这种方式重复命名

console.log("a:",a);
console.log("b:",b);
    * var obj={
    a : 1,
    b : 2
}
let a = 0;
console.log("a:",a);
/*{}在解构赋值时，不能出现在一行的最前边，否则js解析器会把它当成一个代码块，但它不是代码块是解构语法，"="会出错,用()把它包起来，说明是一个语句*/
({a,b} = obj);

console.log("a:",a);
console.log("b:",b);
* var obj={
    arr: [
        'Yo.',
        {
            a: 1,
        }
    ]
}
let {arr:[greet,{a}]} = obj

console.log("greet:",greet);
console.log("a:",a);
* let {a=1,b=2} = {a:10}  //默认值的指定方式
console.log("a:",a);
console.log("b:",b);
    * let {a:A=1,b=2} = {a:10}   //重命名后指定默认值
console.log("A:",A)
console.log("b:",b);
* let res = {
    status:200,
    id:12,
    data:[{name:'Bob'},{name:'Shuan Dan'}]
}
 //传统方法
var status = res.status;   
var id = res.id;
var data = res.data;

 //es6
// let {status, id, data} = res; 

console.log(status)
 #解构数据
    * let {floor,pow} = Math;
let a = 1.9;
console.log("floor(a):",floor(a));
console.log("pow(2,3):",pow(2,3)); #解构方法，Math是对象，对象中有方法
### 其他
* var len = 'Yo.'.length;
console.log("len:",len);
    * let {length} = 'Yo.';
console.log("length:",length);
     * > length是字符串的固有属性
     * > 
     * > 

* let [a,b,c] = 'Yo.';
console.log(a,b,c); #解构字符串
* var arr = [1,2];
function test(a,b) {
    console.log("a:",a);
    console.log("b:",b);
}

test(arr[0],arr[1]) #臃肿
    * var arr = [1,2];
function test([a,b]) {
    console.log("a:",a);
    console.log("b:",b);
}

test(arr)   //传入瞬间被解构 #传参顺序不能更改
        * var obj = {b:2,a:1}
function test({a,b}) {
    console.log("a:",a);
    console.log("b:",b);
}

test(obj)
            * var obj = {b:2}
function test({a = 10,b}) {
    console.log("a:",a);
    console.log("b:",b);
}

test(obj)
## 字符串
### 新增字符串方法
* console.log('Google'.indexOf('e') !== -1);   //是否包含该字符 #之前
    * console.log('Google'.includes('e'));   //是否包含该字符

console.log('Google'.startsWith('o'));

console.log('Google'.endsWith('e'));

console.log('Google '.repeat(7)); #新增
### 模板字符串
* let title = '野外基地 心愿乌托邦'
var tpl1 = '<div>' +
    '<span>' + title + '</span>'+
    '</div>';


let tpl2 = `
<div>
    <span>${title + `
    <span> ${1234} 2016</span>
    `}</span>
</div>    
`;


console.log("tpl1:",tpl1);
console.log("tpl2:",tpl2);
    * tpl1不能分行
## Symbol类型
### Symbol   //新增，作为对象的属性名称，防止对象属性被重写
undefined
null
Boolean
String
Number
Object
### // file1.js
let name = Symbol();
{
    var person = {};
    person[name] = 'Files1';
    console.log("person[name]:",person[name]);

}

//file2.js
{
    let name = Symbol();
    person[name] = 'File2';
    console.log("person[name]:",person[name]);
}

console.log("person[name]:",person[name]);
* 
## proxy
### var user = {};
user.fname = 'Bob';
user.lname = 'Wood';

var full_name = user.fname + ' '+ user.lname;
console.log("fullname:",full_name)
### var user = {
    full_name:function () {
        return this.fname + ' '+ this.lname;
    }
};
user.fname = 'Bob';
user.lname = 'Wood';


console.log("user.full_name:",user.full_name;
### var user = new Proxy({},{
    get: function (obj,prop) {
        if(prop == 'full_name')
            return obj.fname + ' ' + obj.lname;
    }
})

user.fname = 'Bob';
user.lname = 'Wood';


console.log("user.full_name:",user.full_name)
## Set
### var arr = [1,2,3,3];
var s = new Set([1,2,3,3]);
console.log("arr:",arr);
console.log("s:",s);
s.add(4);
console.log("s:",s);
s.delete(2);
console.log("s:",s);
console.log("s.has(5):",s.has(5));
console.log("s.has(3):",s.has(3));
s.clear();
console.log("s:", s);
### 

*XMind: ZEN - Trial Version*