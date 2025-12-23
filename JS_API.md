# JS API

by：Ray1n

------



## DOM

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



### 事件

------

#### 1.事件监听

让程序检测是否有事件发生，如果有则调用对应函数

###### 三要素

事件源, 事件类型, 事件处理程序

###### 语法:

- 元素对象.addEventListener('事件类型', 要执行的函数)



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

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20251223151642593.png" alt="image-20251223151642593" style="zoom: 80%;" />

```javascript
//示例
btn.addEventListener('Keydown',function(evt) { //检测按下回车键
   if(evt.key == 'Enter'){  
       console.log('hello')
	}
})
```



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



### 回调函数

将函数 **A** 作为参数传给函数 **B** 时,称 **A** 为回调函数

```javascript
function fn() {
	console.log('hello')
}
setInterval(fn,1000)  //fn作为参数传给setInterval,此处fn为回调函数
```



### 常用函数

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

##### trim

```javascript
str = '    hello world      '
console.log(str.trim())   //hello world   去除字符串左右的空格
```



## BOM