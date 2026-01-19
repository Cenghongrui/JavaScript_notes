# JS进阶

by：Ray1n

------

[TOC]



### 作用域

规定了变量能被访问的范围

#### 局部作用域

##### 函数作用域

在函数内部声明的变量只能在函数内部被访问

函数执行完毕后内部变量被清空

##### 块作用域

js中被{}包裹的代码称为代码块，代码块内部声明的变量在外部 [有可能] 无法被访问

注：let和const声明的变量会产生块作用域， var声明的变量不会

#### 全局作用域

<script> 标签内部或.js文件中声明的变量(不在局部作用域内)，其它任何作用域都可以访问

#### 作用域链

##### 作用域链本质上是底层的变量查找机制

在函数执行时，会优先在当前函数作用域中查找变量，若找不到则逐级查找父级作用域直到全局作用域

#### JS垃圾回收机制

##### （Garbage Collection）简称GC

js中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收

##### 内存生命周期

内存分配，内存使用，内存回收

##### 内存泄漏

程序中分配的内存由于某种原因程序未释放或无法释放

##### 回收算法

引用计数法，标记清除法

#### JS闭包

一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域

闭包=内层函数+外层函数的变量

```js
function outer(){
    const a=1
    function fn(){
        console.log(a)   //内层函数使用了外层函数的变量  ->  闭包
    }
    fn()
}
outer()
```

##### 作用

封闭数据，提供操作，外部也可以访问函数内部的变量，可以实现数据的私有

##### 基本格式

```js
function outer(){  
    let i=1
    function fn(){
        console.log(i)
    }
    return fn   //fn里是一个函数 return给outer
} 
const fun=outer()  //outer赋值给fun，所以fun也是个函数
fun()//1      调用fun，相当于调用fn 输出i
```

##### 应用

实现数据私有，如统计函数调用次数

```js
function fn(){
    let i=1
    function fun(){
        i++
        console.log(`函数被调用了${i}次`)
    }
    return fun
}
const result = fn()
result() //2
result() //3
i=1000       //不会改变内部变量的值，实现了数据的私有
result() //4
```



### 函数进阶

#### 参数

##### 动态参数

arguments 函数的内置伪数组变量，包含了调用函数时传入的所有实参

如下求和函数（任意数量求和）

```js
function getSum(){
    let sum=0
    for(let i=0;i<arguments.length;i++){
        sum+=arguments[i]  //是伪数组
    }
    return sum
}
console.log(getSum(1,2,3))//6
console.log(getSum(1,2,3,4))//10

```



##### 剩余参数

剩余参数允许我们将一个不定数量的参数表示为一个数组

自定义的剩余实参是个真数组

```js
function getSum(a, b, ...args){   //args 剩余参数 ... 后可以自己命名
    let sum=0						//获得的args是个真数组
    for(let i=0;i<args.length;i++){
        sum+=args[i]
    }
    return sum
}
console.log(getSum(1,2,3))//6
console.log(getSum(1,2,3,4,5))//15    args=[3,4,5]
```



##### 展开运算符(...)

可以将一个数组展开，不会改变原数组

```js
arr=[1,2,3,4,5]
console.log(...arr)//1 2 3 4 5

//可用于合并数组
arr1=[6,7,8,9,10]
arr2=[...arr,...arr1]
console.log(arr2)//1 2 3 4 5 6 7 8 9 10
```



#### 箭头函数（！重要！）

适用于那些本来需要匿名函数的地方,使函数表达式更加简洁

但DOM事件为了回调函数的简便，还是不太推荐使用箭头函数（this指向问题）

##### 语法

```js
const fn =function(a,b){
    console.log(a+b)
}

//箭头函数形式  基本语法
const fn1=(a,b)=>{
    console.log(a+b)
}

const fn2 = x =>{  //一个参数可以省略小括号
    console.log(x)
}

const fn3 = x => console.log(x)  //只有可以省略大括号

const fn = (a,b) => a+b   //相当于return x+x   只有一行代码可以省略return


//事件监听中使用  简洁语句
form.addEventListener('click',evt => evt.preventDefault())  


const fn3 = (name,age) =>({name,age}) //返回一个对象时加小括号 防止大括号冲突
const fn4 = age =>({name,age})

```

##### 箭头函数的参数

没有arguments动态参数，但是有剩余参数

```js
const getSum = (a, b, ...args) => {   
    let sum=0						
    for(let i=0;i<args.length;i++){
        sum+=args[i]
    }
    return sum
}
getSum(2,3,4,5) 
```

##### 箭头函数中的this

普通函数this指向自己的调用者

箭头函数不会自己创建this，但是会从自己作用域链的上一层沿用this

```js
const obj={
    name:'张三',
    func:()=>{
        console.log(this)  //此时this指向Window  而普通函数应该指向obj				                   //因为作用域链的上一层是全局作用域，即obj的this，则this为Window
    }
}
```

### 解构赋值

#### 数组解构

将数组的单元值快速批量赋值给一系列变量的简洁语法

```js
const arr=[100,60,80] 
const [max,min,avg]=arr //max=100,min=60,avg=80
console.log(max,min,avg)

//交换两个变量
let a=1,b=2
;[b,a]=[a,b]  //a=2,b=1  注意解构前面有代码的话需要加分号

const [i,j,...arr] =[1,2,3,4,5] //可以使用剩余参数

const [m,,n] =[1,2,3] //m=1,n=3 可以忽略某些值，按需导入
```



#### 对象解构

将对象属性和方法快速批量赋值给一系列变量的简洁语法

```js
const obj={
    name:'张三',
    age:18,
    sex:'男'
}
const {name,age,sex}=obj //name='张三',age=18,sex='男'
console.log(name,age,sex)

//对象重命名
const person = { name: 'Alice', age: 30 };
const { name: personName, age: personAge } = person;

console.log(personName); // 'Alice'
console.log(personAge);  // 30

//多级对象解构
const obj1={
    name:'张三',
    age:18,
    sex:'男',
    score:{
        math:100,
        english:90,
        chinese:80
    }
}
const {name,age,sex,score:{math,english,chinese}}=obj1  
console.log(name,age,sex,math,english,chinese)
```

### forEach遍历数组

加强版的for循环 ，只遍历，无返回值，适合遍历数组对象

```js
const arr=[1,2,3,4,5]
arr.forEach(item => console.log(item))  //只遍历元素
arr.forEach((item,index) => {
    console.log(item)
    console.log(index)
})  //遍历元素和索引
```

### 对象进阶

#### 构造函数

特殊的函数，用于初始化对象，命名一般用大写字母开头

```js
//构造函数
function Person(name,age,sex){
    this.name=name
    this.age=age
    this.sex=sex
}
//创建对象
const p1=new Person('张三',18,'男')  //new 实例化	
console.log(p1)  
//构造函数可以很方便的批量创建同类型对象

//静态成员
Person.sayHi = function(){  //为构造函数添加方法  
    console.log('hello')
}
Person.eyes = 2    //添加静态属性
//静态成员只能通过构造函数访问
```



#### 内置构造函数

##### Object

```js
const obj={
    name:'张三',
    age:18,
    sex:'男'
}
//获取对象的所有属性名
console.log(Object.keys(obj)) //['name','age','sex']
//获取对象的所有属性值
console.log(Object.values(obj)) //['张三',18,'男']
//将obj拷贝给{}
console.log(Object.assign(obj,{age:20})) //{name:'张三',age:20,sex:'男'}   //修改某属性的值
console.log(Object.assign(obj,{number:123456})) //{name:'张三',age:20,sex:'男',number:123456}  追加属性
```



##### Array

###### 实例方法（部分）

| 方法    | 作用     | 说明                                   |
| ------- | -------- | -------------------------------------- |
| forEach | 遍历数组 | 不返回数组，用于查找遍历数组元素       |
| filter  | 过滤数组 | 返回新数组，返回满足筛选条件的数组元素 |
| map     | 迭代数组 | 返回新数组，返回处理之后的数组         |
| reduce  | 累计器   | 返回累计处理的结果，用于求和           |

```js
const arr=[1,2,3,4,5,6,7,8,9,10]
arr.reduce((pre,cur)=>{
    return pre+cur
},0)                         
console.log(sum)//55    

arr.reduce((pre,cur) => pre+cur ,100)//155   此处设立初始值为100   初始值默认为0，尽量不省略
```



##### String

###### 实例方法（部分）

| 方法                                                  | 作用         | 说明                                                     |
| ----------------------------------------------------- | ------------ | -------------------------------------------------------- |
| split('分隔符')                                       | 拆分字符串   | 以给定分隔符分割，返回数组                               |
| substring(截取的第一个字符的索引，结束的索引（可选）) | 字符串截取   | 提取字符串中介于两个指定下标之间的字符，省略则截取到末尾 |
| startsWith(目标字符串，开始搜索位置索引（可选）)      | 检测字符串   | 判断字符串是否以指定的字符开头                           |
| includes(目标字符串,开始搜索位置索引（可选）)         | 检测目标字串 | 判断字符串是否包含指定的子字符串                         |

##### Number

```js
	const num=12
    console.log(num.toFixed(2))//12.00 设置b
```

### 原型

#### 原型对象

每个构造函数都有一个prototype属性，即原型对象，这个对象可以挂载函数。我们将那些不变的方法直接定义载prototype对象上，这样所有的对象实例就可以共享这些方法

构造函数和原型对象中的this都指向实例化的对象

```js
function Star(name,age){
    this.name=name
    this.age=age  
}

Star.prototype.sing=function(){   //在原型上定义公共方法
    console.log(this.name+'会唱歌')
}

const ldh=new Star('刘德华',18)
ldh.sing()//刘德华会唱歌
const zxy=new Star('张学友',19)
zxy.sing()//张学友会唱歌

console.log(ldh.sing === zxy.sing)  //true 调用的是同一个原型函数
```

#### constructor属性

该属性指向原型对象的构造函数

```js
	const ldh=new Star('刘德华',18)
    console.log(Star.prototype.constructor === Star)  //指向Star
```

#### 对象原型

对象都会有一个对象原型,指向原型对象prototype

同时也有一个constructor属性，指向构造函数

```js
//对象原型 __proto__
```

![image-20251227143955109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20251227143955109.png)

#### 原型继承

```js
function Person(name,age){
    this.name=name
    this.age=age  
}


function Star(){

}
//通过原型继承Person的属性
Star.prototype=new Person()//原型里的函数是指向Star的
```

#### 构造函数继承

```js
function Parent(name) {
    this.name = name;
    this.colors = ['red', 'blue'];
}

function Child(name, age) {
    Parent.call(this, name); // 继承实例属性 将parent的this绑定到child
    this.age = age;    //自定义其它属性
}

const child1 = new Child('Tom', 10);
child1.colors.push('green');

const child2 = new Child('Jerry', 8);
console.log(child2.colors); // ['red', 'blue'] - 不共享colors
```

#### 原型链

是js中实现继承和属性查找的核心机制，基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状结构，称为原型链

```
实例对象 (instance)
    ↓ __proto__ 指向
构造函数的原型 (Constructor.prototype)
    ↓ __proto__ 指向 
上一层构造函数的原型 (Parent.prototype)
    ↓ __proto__ 指向
上上一层构造函数的原型 (GrandParent.prototype)
    ↓ __proto__ 指向
... (中间可能有更多层级)
    ↓ __proto__ 指向
Object.prototype
    ↓ __proto__ 指向
null
```

##### 原型链的查找规则

- 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
- 如果没有就查找它的原型（也就是proto指向的prototype原型对象）
- 如果还没有就查找原型对象的原型（Object的原型对象）
- 依此类推一直找到 Object 为止（null)
- _proto_对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线
- 可以使用instanceof运算符用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上

### 深拷贝和浅拷贝

只针对于引用类型（数组，对象等）

#### 浅拷贝

拷贝地址

```js
//浅拷贝
const obj={
    name:'张三',
    age:18
}
const obj1=obj      //将obj的地址赋给obj1，相当于同一个地址指向两个对象
obj1.name='李四'		//对象属性存储在地址中，改变的却是地址中的值
console.log(obj.name)//李四     所以二者还是完全一样，name都变为李四
console.log(obj1.name)//李四     


//如果是多层对象
const ff={
    name:'张三',
    age:18,
    family:{
        baby:'小狗'
    }
}
const o={}
Object.assign(o,ff)
console.log(o)//{name: '张三', age: 18, family: {baby: '小狗'}}
o.age=20
console.log(o)//{name: '张三', age: 20, family: {baby: '小狗'}}
o.family.baby='小猫'
console.log(o)//{name: '张三', age: 20, family: {baby: '小猫'}}
console.log(ff)//{name: '张三', age: 18, family: {baby: '小猫'}}
//
//上述说明assign可以对最外层的简单数据实现拷贝，age的值互不影响，但是多层对象中的内层就还是只拷贝地址
```



#### 深拷贝

三种常见实现方法

##### 递归实现深拷贝（简化版）

```js
function deepClone(newObj,oldObj){
    for(let key in oldObj){
        if(oldObj[key] instanceof Array){
            newObj[key]=[]   //判断对象属性是否为一个数组   若为复杂数据类型，则递归
            deepClone(newObj[key],oldObj[key])
        }
        else if(oldObj[key] instanceof Object){
            newObj[key]={}   //判断对象属性是否为一个对象
            deepClone(newObj[key],oldObj[key])
        }
        
        else{
            newObj[key]=oldObj[key]   //简单数据类型直接赋值
        }
    }
}
```



##### lodash/cloneDeep

通过lodash.js 库的cloneDeep函数直接实现深拷贝

```js
let obj1 = _.cloneDeep(obj)
```



##### JSON.stringify()

```js
const obj1 = JSON.parse(JSON.stringify(obj));
//先转化成json字符串再转化成对象，也可以实现深拷贝
```



### 异常处理

#### throw抛异常

```js
function fn(x,y){
	if(!x||!y){
        throw new Error('参数不能为空')    //直接中断，程序终止执行，此处直接定义异常类型Error
	}
    return x+y
}
```



#### try/catch捕获异常

```js
try 												// 可能会抛出异常的代码
    const result = divide(10, 0);
    console.log("结果:", result);
} catch (error) {									// 如果发生错误，执行异常处理代码，程序不中断
    console.error("发生错误:", error.message);
    console.error("错误类型:", error.name);
    console.error("调用栈:", error.stack);
} finally {											// 无论是否发生异常都会执行的代码
    console.log("计算完成");
}

```



#### debugger

直接在代码中设置断点

debugger写在设置断点的代码处





### 改变this指向的方法

```js
const obj={
	age:18
}
function fn(x,y){
	console.log(this) //window
    console.log(x+y)   
}
fn()
```



#### call()

会调用函数

```js
fn.call(obj,1,2)   //传递普通的值
fn()    //obj
		// 1+2=3
```



#### apply()

会调用函数，参数必须包含在数组里

```js
fn.apply(obj,[1,2])   //传递的参数必须包含在数组 
fn()   //obj 

//可以用于求数组最大值
Math.max.apply(null,[1,2,3])  //3  相当于把参数1，2，3传给Math.max   即Math.max(1,2,3)
```

#### 

#### bind()

不会调用函数,但是会拷贝一份原型函数并返回

```js
const fn(){
	console.log(this)
}
const fun=fn.bind(obj)  //返回一个函数，但是函数内的this指向obj
```



### 性能优化

#### 防抖（debounce）

单位事件内，频繁触发事件，只执行最后一次

##### lodash库提供的防抖处理

```js
_.debounce(func, [wait=0], [options])
//func: 要防抖的函数
//wait: 等待时间（毫秒）
//options: 可选配置


//示例
// 模拟搜索函数
function search(query) {
    console.log(`正在搜索: ${query}`);
    // 这里实际会发送 API 请求
}

// 创建防抖版本的搜索函数
const debouncedSearch = _.debounce(search, 500);   //用户停止输入500ms后触发1次搜索

// 输入框事件监听
document.getElementById('search-input').addEventListener('input', function(e) {
    debouncedSearch(e.target.value);
});
```

#### 节流（throttle）

单位事件内，频繁触发事件，只执行一次 （相当于冷却事件，冷却事件内不能再执行，结束后可以执行一次又进入冷却）

##### lodash库提供的节流处理

```js
_.throttle(func, [wait=0], [options])
//func: 要节流的函数
//wait: 执行间隔时间（毫秒）
//options: 可选配置


// 模拟一个需要处理滚动事件的函数
function handleScroll() {
    console.log(`滚动位置: ${window.scrollY}px`);
    // 这里可能有一些复杂的计算或DOM操作
}

// 创建节流版本的滚动处理函数（每200ms最多执行一次）
const throttledScroll = _.throttle(handleScroll, 200);

// 监听滚动事件
window.addEventListener('scroll', throttledScroll);
```

