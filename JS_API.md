# JS-APIS 内容整理

by：Ray1n

------

[TOC]



## DOM

文档对象模型

### DOM对象

------

​	浏览器根据html标签生成的JS对象

###### 核心思想

​	把网页内容当成对象处理

###### document

​	DOM提供的一个对象，网页所有内容都在document里面

```javascript
document.body  //body是子元素
```



#### 1.获取DOM对象

```html
<div class="box" id="box_id">123</div>
<div class="box">456</div>
<ul class="nav">
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
```

```javascript
//获取匹配的第一个元素（css选择器），返回对象
const div = document.querySelector('div')
const box = document.querySelector('.box')
const box_id = document.querySelector('#box_id')
const l = document.querySelector('ul li:first-child') 

//获取匹配的所有元素，返回匹配的对象集合(伪数组，没用pop push等方法，需要遍历来获取每个元素)
const divALL   = document.querySelectorAll('div')
```

#### 2.操作对象内容

```javascript
//对象.innerText   纯文本，不解析标签
const box = document.querySelector('.box')
console.log(box.innerText) // 获取文字内容
box.innerText = '456' //修改文字内容
console.log(box.innerText)

//对象.innerHTML  解析标签 
box.innerText = '<strong>456</strong>'

```

#### 3.操作对象属性

##### 一般属性

```javascript

const pic =document.querySelector('img')
pic.src = './img/1.jpg'//更改常用属性
pic.alt = '1.jpg'
pic.title = '1.jpg'

pic.style.width = '200px' //更改样式属性

div.style.backgroundColor = 'pink' //多组单词组成的采取小驼峰命名法
 

//通过className操作样式
div.calssName = 'box1' //操作元素类名  

//通过classList操作样式  
div.classList.add('box1')     //追加类
div.classList.remove('box1')  //移除类
div.classList.toggle('box1')  //切换类  有就删掉，没有就加上

```

##### 表单属性

```javascript
//表单
const uname = document.querySelector('input')
uname.value='hello'  //表单内容在value里
uname.type='password'  //表单属性
uname.checked= true  //disabled  selected同理
```

##### 自定义属性

```html
<div data-id="1001" data-no='1'>box</div>    data-自定义属性
```

```javascript
const box = document.querySelector('div')
console.log(box.dataset.id)  //dataset.id 调用data-id属性
```



### DOM节点

------

DOM树里的每个内容都叫节点

四个类型：元素节点，属性节点，文本节点，其它节点

#### 1.查找节点

```html
<div class="grandfather">
  <div class="father">
    <div class="son1"></div>
    <div class="son2"></div>
    <div class="son3"></div>
  </div>
</div>
```

```javascript
//父节点查找
console.log(son.parentNode) //返回父节点 返回father

//子节点查找
console.log(father.children)//返回一个伪数组，包含所有子节点

//兄弟节点查找
console.log(son2.nextElementSibling) //返回下一个兄弟节点 返回son3
 console.log(son3.previousElementSibling) //返回上一个兄弟节点 返回son2
```

#### 2.增加节点

```javascript
const son4 = document.createElement('div')  //新增son4节点，类型为div
son4.className = 'son4'
father.appendChild(son4) //将son4节点追加到father中
```

#### 3.删除节点

```javascript
//删除节点
father.removeChild(son3) //删除son3节点
```

#### 4.克隆节点

```javascript
//克隆一个已有的节点
const son4Clone = son4.cloneNode(true)  //true  连同后代节点一起克隆
father.appendChild(son4Clone)			//false 不包含后代节点，默认为false
```



### 事件

------

#### 1.事件监听

让程序检测是否有事件发生，如果有则调用对应函数

###### 三要素

事件源, 事件类型, 事件处理程序

###### 语法:

元素对象.addEventListener('事件类型', 要执行的函数)



#### 2.事件类型

##### 鼠标事件

```javascript
const btn = document.querySelector('.btn')
btn.addEventListener('click',function() { //鼠标点击
   alert('hello')
})

btn.addEventListener('mouseenter',function() { //鼠标经过
   alert('hello')
})

btn.addEventListener('mouseleave',function() { //鼠标离开
   alert('hello')
})
```

##### 焦点事件

```javascript
const input = document.querySelector('.input')
input.addEventListener('focus',  function() { //获得焦点
   alert('获得焦点')
})

input.addEventListener('blur',function() { //失去焦点
   alert('失去焦点')
})

```

##### 键盘事件

```javascript
btn.addEventListener('Keydown',function() { //键盘按下  
   alert('hello')
})

btn.addEventListener('Keyup',function() { //键盘抬起
   alert('hello')
})
```

##### 文本事件

```javascript
btn.addEventListener('input',function() { //用户输入文本则触发
   alert('hello')
})

```

#### 3. 事件对象

 在事件绑定的回调函数里的第一个参数就是事件对象

 事件对象包含了事件触发时的相关信息,可以用于判断用户按下哪个键,点击了哪个元素等

```javascript
btn.addEventListener('click',function(event) { //event 为事件对象
   console.log(event)
})
```

##### 常见事件对象属性

| 属性            | 作用                                     |
| --------------- | ---------------------------------------- |
| type            | 获取当前的事件类型                       |
| clientX/clientY | 获取光标相对于浏览器可见窗口左上角的位置 |
| offsetX/offsetY | 获取光标相对于当前DOM元素左上角的位置    |
| key             | 用户按下的键盘的键值                     |

```javascript
//示例
btn.addEventListener('Keydown',function(evt) { //检测按下回车键
   if(evt.key == 'Enter'){  
       console.log('hello')
	}
})
```

#### 4.事件流

事件流是事件完整执行过程中的流动路径

两个阶段：事件捕获和事件冒泡

###### 事件捕获

从DOM根元素执行对应的事件

```javascript
document.addEventListener('click',function(){
       alert('点击了');
},true)  // 第三个参数表示是否使用事件捕获机制 （很少使用），开启后会导致事件从外到里执行 ，默认为false（事件冒泡）
```

##### 事件冒泡

一个元素事件触发时，会依次向上调用所有父级元素的同名事件（与事件捕获相反）

##### 阻止冒泡

将事件限制在当前元素内，不会影响父级元素

语法: 事件对象.stopPropagation()    （本质是阻止事件流动传播，对捕获也有效）

```javascript
document.addEventListener('click',function(){
    alert('点击了')
})
father.addEventListener('click',function(){
    alert('点击了father')
})
son.addEventListener('click',function(e){
    alert('点击了son')
    e.stopPropagation() //阻止冒泡
})
```

##### 解绑事件

```javascript
function fn(){
	alert('点击了son')
}

son.addEventListener('click', fn)
son.removeEventListener('click',fn) //解绑（匿名函数无法解绑）
```

#### 5.事件委托

利用事件流特性解决一些开发需求（事件冒泡的特点）

原理：给父元素注册事件，当我们触发子元素时，会冒泡到父元素上，从而触发父元素的事件

##### 优势：

- 减少注册次数，提高程序性能

```javascript
const ul = document.querySelector('ul');
const li = document.querySelectorAll('li');
        // 事件委托
ul.addEventListener('click',function(e){
      if(e.target.tagName === 'LI'){//三等判断是否全等   找到真正的触发元素
          e.target.style.color = 'red';
      }
})
```



#### 6.其他事件

##### 页面加载事件

```javascript
window.addEventListener('load',function(){//等待页面所有资源加载完毕（适用于script写在页面代码前面的情况）
            const btn = document.querySelector('button');
            btn.addEventListener('click',function(){
                alert('点击了按钮');
            })
        })

//也可以绑定例如img等某个资源


document.addEventListener('DOMContentLoaded',function(){//等待页面DOM加载完毕  无需等待样式表，图像等加载
            const btn = document.querySelector('button');
            btn.addEventListener('click',function(){
                alert('点击了按钮');
            })
        })
```

##### 页面滚动事件

```javascript
window.addEventListener('scroll',function(){
            console.log('滚动了');
  					console.log(document.documentElement.scrollTop);  //获取页面滚动的距离（获取html元素写法）
        })

div.addEventListener('scroll',function(){
            console.log(div.scrollLeft);  //可以获取滚动的距离
            console.log(div.scrollTop);
        })
```

##### 页面尺寸事件

```javascript
window.addEventListener('resize',function(){
  					const width = document.documentElement.clientWidth;  //获取页面的宽高
            const height = document.documentElement.clientHeight;
            console.log('尺寸改变了');
        })
```

###### client和offset

```javascript
offsetWidth //获取元素自身宽高，padding， border  的总和      
offsetHeight

clientWidth
clientHeight //只有自身宽高


offsetTop
offsetLeft //只读属性，获取元素距离自己定位父级元素的左，上距离
```

#### 7.移动端事件

| 触屏事件   | 说明                          |
| ---------- | ----------------------------- |
| touchstart | 手指触摸到一个DOM元素时出发   |
| touchmove  | 手指在一个DOM元素上滑动时触发 |
| touchend   | 手指从一个DOM元素上移开时触发 |



### 环境对象

------

指函数内部特殊的变量 **this**, 它代表这当前函数运行时所处的环境

可以用于简化代码   

粗略规则: this指向调用者

```javascript
function fn() {
    console.log(this)  //普通函数中的this指向window
}
window.fn() //window调用了fn,那么this就指向window 


btn.addEventListener('click',function() { 
   this.style.color = 'red'  //btn调用了函数,this就指向btn
})
```

##### 阻止默认行为

```javascript
const form = document.querySelector('form');
form.addEventListener('submit',function(e){
     e.preventDefault();   //阻止表单的默认提交行为
})
```



### 日期对象

------

用来表示时间的对象，可以得到当前系统时间

#### 实例化

```javascript
const date = new Date()  //获取当前时间

const date1 = new Date('2025-5-1 08:30:00') //获取指定时间
```

#### 日期对象方法

| 方法          | 作用               | 取值         |
| :------------ | ------------------ | ------------ |
| getFullYear() | 返回年份           | 四位年份     |
| getMonth()    | 返回月份           | 0～11        |
| getDate()     | 返回月份中的每一天 | 取决于该月份 |
| getDay()      | 返回星期           | 0～6         |
| getHours()    | 返回小时           | 0～23        |
| getMinutes()  | 返回分钟           | 0～59        |
| getSeconds()  | 返回秒             | 0～59        |

```javascript
//示例
console.log(date.getFullYear())   //获得年份
```

#### 时间戳

指1970年1月1日 00:00:00 起至现在的毫秒数，时一种特殊的时间计量方式

##### 三种获取方法

```javascript
console.log(date.getTime());//此法需要实例化
console.log(+new Date());//本质是把实例化的字符串型转换成数字型   前两种可以返回指定时间的时间戳

console.log(Date.now());//只能得到当前时间戳
```



### 回调函数

------

将函数 **A** 作为参数传给函数 **B** 时,称 **A** 为回调函数

```javascript
function fn() {
	console.log('hello')
}
setInterval(fn,1000)  //fn作为参数传给setInterval,此处fn为回调函数
```



### 其它函数

------

##### 间歇函数

```javascript
//setInterval(函数， 间隔时间(ms))   设立定时器  
setInterval(function() {
  console.log('hello')
},1000) //每隔1秒调用一次    

function fn() {
	console.log('hello')
}

let n = setInterval(fn,1000)   //有名函数只写函数名  

clearInterval(n)   //关闭定时器n  需要写在fn函数里面
```

##### trim()

```javascript
str = '    hello world      '
console.log(str.trim())   //hello world   去除字符串左右的空格
```

##### 延时函数（定时器）

```javascript
let timer =  setTimeout(function(){
  console.log('hello world')
},1000   //等待的毫秒数，只执行一次
                        
clearTimeout(timer)            //清除延时函数，和setInterval类似             
```



## BOM

浏览器对象模型，包含DOM

### 事件循环机制（event loop）

主线程先执行所有的同步任务，执行完毕后查询任务队列（异步队列），取出一个任务推入主线程处理。重复该动作

**异步任务**：包含ajax网络模块，DOM事件，setTimeout，setInterval等api

### Window对象

全局对象，js中的顶级对象



#### location对象

一个对象类型，拆分并保存了URL地址的各个组成部分

##### href属性

```javascript
console.log(location.href) //返回网页地址

location.href = 'https://www.baidu.com'  //利用赋值操作让页面自动跳转
```

##### search属性

```javascript
console.log(location.search) //获取地址中携带的参数（符号？后面的部分）
```

##### hash属性

```javascript
console.log(location.hash)//获取#后面的部分
```

##### reload属性

刷新页面

```js
const reload = document.querySelector('.reload')  
reload.addEventListener('click',function(){ 
  location.reload()       //绑定按键点击事件，    点击后刷新页面
  location.reload(true)   //强制刷新
})
```



#### navigator对象

一个对象类型，记录了浏览器自身的相关信息，可用于检测为pc端或移动端

```js
//检测移动端代码，即插即用
!function(){
    const userAgent = navigator.userAgent
    // 验证是否为Android或iPhone
    const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
    const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
    // 如果是Android或iPhone，则跳转至移动站点
    if (android || iphone) {
        location.href = '你的移动端地址'
    }
}()
```



#### history对象

 一个对象类型，管理浏览器的历史记录，与浏览器地址栏操作相对应（前进后退等）

| 方法      | 作用                                                  |
| --------- | ----------------------------------------------------- |
| back()    | 后退                                                  |
| forward() | 前进                                                  |
| go(参数)  | 前进或后退  参数为1前进一个页面，参数为-1后退一份页面 |

```js
back.addEventListener('click',function(){//后退
    history.back()
  	//history.go(-1)  
})
forward.addEventListener('click',function(){//前进
    history.forward()
    //history.go(-1)  
})
```



### 本地存储

将数据存在浏览器中

#### localStorage

可以将数据永久存储在本地，除非手动删除（关闭页面也会存在） 

只能存字符串类型

##### 特点

多页面共享

以键值对的形式存储使用

##### 语法

localStorage.setItem(key,value)

```js
localStorage.setItem('name','张三') //存入

console.log(localStorage.getItem('name')) //查询  返回 值 张三

localStorage.removeItem('name') //删除

localStorage.setItem('name','李四')  //修改  再存入一次就是修改
```

##### 存储复杂数据类型

需要将复杂数据类型转换成JSON字符串

```js
const obj = {
      name:'张三',
      age: 18,
      gender:'男'
}

localStorage.setItem('obj',JSON.stringify(obj))  //存 

console.log(JSON.parse(localStorage.getItem('obj')))  //取

JSON.stringify()//把对象转换成json字符串
JSON.prase()//把json字符串转换为对象
```

## 正则表达式

### 介绍

用于匹配字符串的一种模式, 在js中是一种对象

可用于：表单验证， 过滤敏感词， 字符串中提取目标部分



### 基本语法

```javascript
const 变量名 = /表达式/

//示例

const str = 'hello javascript world'
//定义规则
const reg = /java/  //查什么写什么
//查找是否匹配
console.log(reg.test(str))   //返回布尔值true 说明有java
console.log(reg.exec(str)) //exec方法返回一个数组
```



### 进阶语法

#### 元字符

一些具有特殊含义的字符，极大提高了灵活性，具有强大的匹配功能

例如26个英文字母     元字符写法:[a-z]

##### 边界符

用来提示字符所处的位置

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| ^      | 表示匹配行首的文本（以谁开始） |
| $      | 表示匹配行尾的文本（以谁结束） |

```js
console.log(/^哈/.test('哈'))//true
console.log(/^哈/.test('哈哈'))//true
console.log(/^哈/.test('二哈'))//false

console.log(/^哈$/.test('哈'))//true   //表示精确匹配，只能有一个'哈'
console.log(/^哈$/.test('哈哈'))//false 
```

##### 量词

用来设定某个模式出现的次数

| 量词  | 说明            |
| ----- | --------------- |
| *     | 重复0次或更多次 |
| +     | 重复1次或更多次 |
| ？    | 重复0次或1次    |
| {n}   | 重复n次         |
| {n,}  | 重复n次或更多次 |
| {n,m} | 重复n次到m次    |

```js
console.log(/^哈$/.test('哈'))//true
console.log(/^哈*$/.test(''))//true
console.log(/^哈*$/.test('哈哈'))//true
console.log(/^哈*$/.test('二哈哈二'))//false  没有以 哈 结尾


console.log(/^哈{4}$/.test('哈'))//false
console.log(/^哈{4}$/.test('哈哈'))//false
console.log(/^哈{4}$/.test('哈哈哈'))//false
console.log(/^哈{4}$/.test('哈哈哈哈'))//true  必须出现4次
console.log(/^哈{4,}$/.test('哈哈哈哈哈'))//true 大于等于4次
```

##### 字符类

###### 一般

```js
console.log(/[abc]/.test('safac'))//true  包含中括号内任意一个字符，返回true
console.log(/^[abc]$/.test('safac'))//true
//可以使用连字符-表示范围
console.log(/^[a-zA-Z0-9]$/.test('safac22'))//true   匹配所有英文字母和数字

//中括号里的^表示取反
console.log(/^[^a-z]$/.test('safac22'))//false 匹配小写字符以外的字符
```

###### 预定义类

一些常见模式的简写方式

| 预定义类 | 说明                                                       |
| -------- | ---------------------------------------------------------- |
| \d       | 匹配0-9间的任意数字                                        |
| \D       | 匹配0-9以外的任意字符                                      |
| \w       | 匹配任意的字母，数字，下划线 相当于[A-Za-z0-9]             |
| \W       | 匹配除字母，数字，下划线以外的字符                         |
| \s       | 匹配空格（包括换行符，制表符，空格符等）相当于[\t\r\n\v\f] |
| \S       | 匹配非空格字符                                             |

###### 修饰符

/表达式/修饰符

```js
console.log(/a/i.test('a'))//true   i表示匹配时字母不区分大小写
console.log(/a/i.test('A'))//true

console.log(/a/g.test('A'))//   g表示全局查找
```

### replace方法

```js
字符串.replace(/正则表达式/, '替换的文本')
const str = 'java是一门编程语言，学好java'
str.replace(/java/i, 'python')  //将 第一个 java 替换为 python
str.replace(/java/ig, 'python')  //将 所有的 java 替换为 python
```

