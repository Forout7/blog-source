---
title: Javascript的基础入门
tags:
  - Javascript基础
categories:
  - Javascript
date: 2026-05-28 21:21:38
---

# day01 JavaScript的基础入门

### 概述

JavaScript是一个弱语言（赋值的类型是什么那就是什么类型），它是一个脚本语言（侵入性 xss攻击），它是一个解释型语言（内置的的是一个解释器用于解释执行 （v8引擎  （解释加编译）））。JavaScript是一个单线程的语言（渲染线程和执行线程只有一个），JavaScript主要有三部分组成，DOM(document object model 文档对象模型)，BOM（bowser object model 浏览器对象模型），ECMAScript （ES3(基础版本),ES5,ES6....）基础语法。遵从w3c规范（浏览器规范）。

### JavaScript中的编译器和解释器

![image-20260528211641945](image-20260528211641945.png)

### 编译相关内容

- AOT (ahead of time) 预编译
- JIT （just in time）边编译边执行

### JavaScript的相关编译流程

![image-20260528211700927](image-20260528211700927.png)

### JavaScript的执行流程

![image-20260528211722338](image-20260528211722338.png)



### JavaScript的书写位置

##### 在script标签中声明

```html
<script>
  console.log('hello world')
</script>
```

##### 在html的事件属性中书写

```html
<button onclick="console.log('click')"></button>
```

##### 通过script标签链入第三方js

```html
<!-- 书写在对应的JavaScript文件中 通过src属性联入 其实也是将对应的文件的内容加载到script标签中 -->
<script src="./test.js"></script>
```

### JavaScript中的命名规范

- 不能以数字开头
- 只能包含字母数字下滑线及$符号
- 采用驼峰命名法 （大驼峰  （组件命名）  小驼峰（变量和方法命名））
- 常量名全部大写
- 不能以关键词及保留字用于命名 （如this  private...）
- ....

### JavaScript的注释

- 单行注释 (快捷键 ctrl + /)

  ```javascript
  //
  ```

- 多行注释 (快捷键 alt + shift + a)

  ```javascript
  /*
  多行注释
  */
  ```

- 文档注释 （其实也是多行注释）

  ```javascript
  /**
  @param
  @return
  **/
  ```

### JavaScript的变量声明

- var 声明全局变量 （伪全局变量 变量提升）
- let 声明块级变量（ES6新增）
- const 声明常量 （ES6新增）

```JavaScript
//通过var关键词进行声明
console.log(a) //var会进行预编译（执行之前） 赋值为undefined 
var a = 10 //将10值赋值给a的空间
var a = 20
//var关键词在全局作用域中声明的变量 会变成对应的globalThis（全局对象）的属性
//浏览器的globalThis为window   全局对象又称为全局上下文 globalContext
console.log(window.a)
//let 关键词
//存在块级作用域  它会在对应的块区间内容 有自己的值保存
for (let index = 0; index < 10; index++) {
    //定时器 定时器的线程 异步的   同步执行比异步快
    setTimeout(()=>{
        console.log(index)
    },0)
}
// let 关键词不允许重复声明 在同一块内 不允许重复声明
let b = 10
// let b = 20  报错
// const 声明常量 常量不能变 声明必须赋值 一旦赋值地址不可变
// const c  报错 声明必须初始化
// 拥有块级作用域 不能重复声明
const c = 20
// const c = 30 报错
// c = 30 执行出错  赋值后地址不可变
const obj = { age:10 }
obj.age = 30 //const 修饰的对象的属性是可以更改的
console.log(obj)
// obj = {age:40} //对象 声明使用new关键词 或 字面量 {}
console.log({} == {}) //false
```

### JavaScript的数据类型

##### 值类型

- number类型 （浮点数 整数）
- string类型 （字符串 单引号 和 双引号 字符串模板 `` ）
- boolean 类型  （true 或者 false）
- null 类型 （空指针引用 gc回收 对象置空操作 null）
- undefined 未定义的值 （undefined）undefined是null的派生子类
- bigInt （ES6新增的 为了处理number处理不了的值）
- symbol （独一无二的值 底层实现用的是机器编码  为了底层设计）

###### 值类型使用typeof进行相关判断

##### 引用数据类型

object 、Array、method....

###### 引用数据类型可以使用instanceOf进行判断具体的类型

##### 浏览器内核中的内存划分

- 堆 引用类型存在于堆
- 栈 值类型存在于栈

##### 二进制转换

- **parseInt**方法将其他进制转为10进制
- **toString**方法将10进制转为其他进制

#### JavaScript的中的运算符

##### 算术运算

```
+ - * / % ++ -- 
```

- 使用加号出现字符串返回的值就是字符串
- 除上述情况其他的计算都会使用Number隐式转为数值类型
- true转为number为1  false为0

##### 赋值运算

```
= += *= %= /= -=
```

##### 比较运算 (最终返回boolean类型)

```
> < >= <= == === != !==
```

- 字符串1和数值1值是相等的
- 字符串和字符串进行比较比较的是acsii码
- undefined等于null 不恒等于null
- 出现NaN就是false
- 0.1+0.2 是不等于0.3的

##### 逻辑运算符

```
&&  ||  !
&& 全部为true取最后一个ture 有false出现取第一个false
|| 有一个为true取第一个ture 全部为false取最后一个false
! 取反 默认会进行转换（boolean类型转换）
```

##### 位运算符

```
& | ~ ^ >> <<  >>>
```

###### 通过对应的&判断奇偶

```JavaScript
//使用位与 来判断奇偶
console.log(2 & 1)//0 偶数
console.log(3 & 1)//1 奇数
```

### 条件分支语句

##### if else 区间判断

###### 基础语法

```
if(条件表达式){
	满足条件执行代码
}else{
	不满足条件的执行的代码
}
```

if else支持 多分支 （else if）支持嵌套 （嵌套不要超过俩层 ）

###### 基础案例（判断一个值是否为3的倍数或7的倍数）

```html
<script>
    //接收的这个数据它是一个字符串类型
    var print = prompt('请输入一个内容')
    if (print / 1 && print != 0) {
        //输入正确后
        //判断是否为3的倍数 是否为7的倍数  是否同时为3的倍数及7的倍数
        //if else 分支一旦进入其中一个分支 那么后续不会再执行
        if (print % 21 == 0) {
            console.log('即是三的倍数 又是七的倍数')
        } else if (print % 7 == 0) {
            console.log('七的倍数')
        } else if (print % 3 == 0 ) {
            console.log('三的倍数')
        } else{
            console.log('无关紧要')
        }
    } else {
        console.log('输入出错')
    }
</script>
```

##### switch case 值判断 break 跳槽对应的代码块

###### 基础语法

```
switch(表达式){
	case 值1:
		操作1;
		break;
	case 值2:
		操作2;
		break;
	default:
		默认操作
}
```

###### 基础案例（判断一个值是否为3的倍数或7的倍数）

```javascript
var input = prompt('请输入一个值')
switch (true) {
    case input % 21 == 0:
        console.log('即是三的倍数 又是七的倍数');
        break;
    case input % 7 == 0:
        console.log('七的倍数');
        break;
    case input % 3 == 0:
        console.log('三的倍数')
        break;
    case Boolean(input * 1):
        console.log('不是倍数')
        break;
    default:
        console.log('输入出错')
}
```

switch case 是以空间换时间的形式 相对if else而言对应的时间复杂度略低

### 循环控制语句

##### 注意事项

- 初始值  迭代量  迭代条件 缺少其中一个就会造成死循环 （需要避免死循环 （内存溢出））
- 循环允许嵌套 但是一般建议嵌套层数不要超过俩层 （On2）

##### for 循环

```
for(初始值;迭代条件;迭代量){
   循环执行的操作
}
```

###### 基础案例 乘法口诀表

```html
 <script>
    for (let i = 1; i <= 9; i++) { //外层控制行
      let print = ""
      for (let j = 1; j <= i; j++) { //里层控制列
        print += `${j}*${i}=${i*j}\t`
      }
      document.write(print+"<br/>") //打印及换行操作
    }
  </script>
```

##### while 循环

```
while(迭代条件){
  执行操作的时候需要控制对应的迭代量的变换或者使用break来跳出代码块
}
```

###### 基础案例 打印水仙数 100-1000

```javascript
let i = 100
while (i < 1000) {
    //取值
    let a = i % 10
    let b = parseInt(i / 10) % 10
    let c = parseInt(i / 100)
    if (Math.pow(a, 3) + Math.pow(b, 3) + Math.pow(c, 3) == i) {
        console.log(i)
    }
    i++; //迭代量 迭代
}
```

##### do while 循环 （至少做一次）

```
do{
 执行的操作 需要控制迭代量的变换
}while(迭代条件)
```

###### 基础案例 计算1到100的偶数和

```javascript
var i = 1
var sum = 0
do{
 if(!(i&1)){
 	sum+=i;
 }
 i++; //迭代量
}while(i<=100)
console.log(sum)
```

##### break 跳出代码块  continue  跳过此次循环

```javascript
//计算对应的1到10的阶乘
var result = 1
var i = 1
while(true){
    result *= i
    i++; //迭代条件
    if(i==10)
        break; //跳出整个代码块
}
console.log(result)
var sum = 0
//计算偶数和
for(let i=1;i<=10;i++){
    if(i & 1){ //奇数跳过
        continue; //跳过此处循环
    }
    sum += i
}
console.log(sum)
```

##### for in 对象迭代

```javascript
//key:value 构成的对象 迭代是key
let obj = {
	age:18,
	name:"jack",
	sex:'男'
}
//使用for in迭代
for(key in obj){ //默认以var关键词声明的
	console.log(key + ':'+obj[key])
}
```

##### for of 数组迭代（需要实现迭代器方法 iterable）

```javascript
//迭代的是值
let arr = ['水果','蔬菜','KFC']
//使用for of进行迭代
for(let value of arr){
	console.log(value)
}
```

### 字符串（增删改查的方法）

字符串的所有方法都不能原本的字符串 只会通过返回一个新的字符串来进行操作

##### 相关方法

- indexOf  根据字符串找第一次出现的下标 找不到返回-1
- lastIndexOf 从后面往前根据字符串找第一次出现的下标 找不到返回-1
- charAt 根据对应的下标返回字符串
- charCodeAt 根据对应下标返回字符串的ascii码
- search 根据对应的正则或字符串查找对应的下标
- includes 是否包含 startsWith 是否开头 endsWith 是否结尾
- padEnd  padStart 添加内容到指定的数量
- substring  substr  slice 截取方法
- split 根据正则或字符串进行分割返回对应字符串数组 
- replace 根据正则或字符串进行对应的字符串的替换
- match 根据正则或字符串返回匹配的正则匹配对象数组
- trim 去除前后的空格  concat 连接
- toLowerCase  toUpperCase 转大小写
- repate 重复
- localeCompare 参照对应的顺序进行比较 为-1 在之前 为1在之后
- normalize 将对应的Unicode编码变成显示正常的内容

##### 静态方法

- String.fromCharCode 将ascii码转为字符串

##### 属性

- length属性

##### 支持正则的方法

search  match  replace  split

##### 字符串的遍历

###### 使用下标访问对应的字符

```
console.log('abc'[0])
```

###### 使用for of进行遍历

```javascript
//使用for of进行遍历
for(let char of 'abc'){
    console.log(char)
}
```

### 数组（增删改查的相关方法）

#### 数组的声明

###### 使用字面量声明

```javascript
var arr = []
```

###### 使用new关键词构建（构造函数调用）

```javascript
var arr = new Array();//空数组 长度为0
//传递一个number类型的参数
var arr = new Array(10); //构建长度为10的数组 里面内容为empty
//传递多个参数
var arr = new Array(1,2,3);//将多个内容填入到数组 并开辟空间 长度为传入的个数
```

#### 数组的特性

具备下标 可以通过下标进行访问（从0开始）

```javascript
var arr = [1,2,3]
console.log(arr[0]) //获取下标为0的内容 1
```

具备length属性获取对应的长度

```javascript
var arr = [1,2,3]
console.log(arr.length)
```

#### 数组的相关方法

- push 添加到后面 （返回新的长度）  pop 删除最后一个的内容 （返回删除的内容）
- unshift 添加内容到前面（返回新的长度） shift 删除第一个的内容 （返回删除的内容）
- splice 删除 传递对应的开始的下标和对应的删除个数进行删除 也可以传入插入的内容进行插入
- reverse 翻转  sort 排序  concat 连接 
- join 将数组连接成一个字符串 
- slice 截取  includes 是否包含
- indexOf  lastIndexOf 查找下标
- flat 数组扁平化方法 
- fill 填充内容
- 高阶函数 ES5新增 map  forEach reduce reduceRight  filter  some  every 
- ES6新增 find  findIndex 查找 

##### 静态方法

- Array.of  传入对应的参数组成一个新的数组
- Array.from  将伪数组转换为数组