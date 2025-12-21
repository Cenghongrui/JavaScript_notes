# **JavaScript基本语法整理**  

by:Ray1n

------

### 一.输入输出

###### 	输出

```javascript
document.write('hello world')//页面输出
document.write('<h1>hello world</h1>')

alert('hello world!')//页面弹出提示框

console.log('hello world!')//控制台打印输出
```

###### 	输入

```javascript
prompt('请输入你的姓名')//弹出输入对话框

let name =prompt('请输入你的姓名')//输入赋值给name
```

------

### 二.变量

```javascript
let name = '张三' //声明和赋值
alert(name)  //输出'张三'
name='李四
alert(name)

//同一变量不能重复声明
```

------

### 三.常量

```javascript
const PI=3.14;
alert(PI);

const G=9.8;
alert(G);
```

------

### 四.数组

```javascript
//数组可以存任意类型数据
let arrs=['a','b','c']
alert(arrs);

arrs[0]=1
alert(arrs[0])

//添加元素到末尾
arrs.push('d'); 
alert(arrs); 

//返回数组长度
len=arrs.length;

```

##### 数组的增删改查

###### 增加元素

```javascript
let fruits = ['苹果', '香蕉', '橙子'];

// push() - 在数组末尾添加元素
fruits.push('葡萄');//['苹果', '香蕉', '橙子', '葡萄']
       
// unshift() - 在数组开头添加元素
fruits.unshift('草莓');//['草莓', '苹果', '香蕉', '橙子', '葡萄']


// splice() - 在指定位置添加元素
//第一个参数表示从数组索引为2处开始操作
//第二个参数表示要删除的元素的数量，为0代表只插入
fruits.splice(2, 0, '猕猴桃', '菠萝');//['草莓', '苹果', '猕猴桃', '菠萝', '香蕉', '橙子', '葡萄']

```

###### 删除元素

```javascript
     
// pop() - 删除数组末尾元素，可视为出栈操作
let lastFruit = fruits.pop();//['草莓', '苹果', '猕猴桃', '菠萝', '香蕉', '橙子']
        
// shift() - 删除数组开头元素
let firstFruit = fruits.shift();//['苹果', '猕猴桃', '菠萝', '香蕉', '橙子']
        
// splice() - 删除指定位置的2个元素
let removedFruits = fruits.splice(1, 2);//fruits=['苹果', '香蕉', '橙子']    removedFruits=['猕猴桃', '菠萝']

```

###### 修改

```javascript

// 直接索引赋值
fruits[0] = '红苹果';//['红苹果', '香蕉', '橙子'] 

// splice() - 替换元素
fruits.splice(1, 1, '黄香蕉');//删除'香蕉'并替换'黄香蕉'  ['红苹果', '黄香蕉', '橙子'] 

```

###### 查找

```javascript

// indexOf() - 查找元素的索引
let index = fruits.indexOf('黄香蕉');  //返回 1

// includes() - 检查元素是否存在
let hasOrange = fruits.includes('橙子');//返回 true
        
// find() - 查找第一个符合条件的元素
let findFruit = fruits.find(fruit => fruit.includes('苹果'));//返回第一个包含'苹果'的元素   红苹果
        
// filter() - 查找所有符合条件的元素
let allApples = fruits.filter(fruit => fruit.includes('苹果'));//返回所有包含'苹果'的元素:  红苹果
        
```

------

### 五.数据类型

###### 检测数据类型方法:   typeof x

```javascript
let num=10
console.log(typeof num)
console.log(typeof(num))
```



##### 1.数字

​	弱数据类型，可以是小数也可以是整数

##### 2.字符串

###### 	字符串拼接

```javascript
let a='hello world'
let b='hello js'
console.log(a+b);//'+'可实现字符串拼接，结果为'hello worldhello js'

```

###### 	模板字符串

```javascript
let age=18;
document.write(`<h1>我今年${age}岁</h1>`);  //注意要用反引号！

let age=prompt('请输入你的年龄');
document.write(`<h1>我今年${age}岁</h1>`);
```

##### 3.布尔（boolean)

 	true, false 

##### 4.未定义类型(undefined)

```javascript
let age 
document.write(age)  //输出 undefined
```

##### 5.空类型（null)

​	通常用于创建新对象

```javascript
let obj=null
console.log(obj)  //输出 null
```

##### 6.数据类型转换

```javascript
let str='123'
console.log(Number(str))//转换成数字型  显式转换
console.log(+prompt('请输入一个数字'))//转换成数字型  隐式转换

console.log(parseInt('12px'))//12
console.log(parseInt('12.34px'))//12
console.log(parseInt('12.345px'))//12   只保留整数部分
console.log(parseInt('abab12.345px'))//  不识别

console.log(parseFloat('12px'))//12
console.log(parseFloat('12.34px'))//12.34
console.log(parseFloat('12.345px'))//12.345  保留整数和小数部分
```

------

### 六.分支语句

##### 1.if分支

```javascript
if(true){
    console.log('hello world')
}else if(false){
    console.log('hello js')
}else{
    consol.log('aaa')
}

if(3>5){
    console.log('hello js')  //3>5 = false 不执行
}
```



##### 2.三元运算符

语法： 条件 ？满足条件执行的代码  ： 不满足条件执行的代码

```javascript
3<5 ? alert('true') : alert('false')  //输出true
```



##### 3.switch分支

```javascript
let num = prompt('请输入1-3之间的数字')
switch(num){
  case '1':
    console.log('你输入的是1')
    break
   case '2':
    console.log('你输入的是2')
    break
   case '3':
    console.log('你输入的是3')
    break
   default:
    console.log('你输入的数字不在1-3之间')
```

------

### 七.循环语句

##### 1.wihle循环

```javascript
let i=1
while(i<=3){
    document.write(`第:${i}次循环<br>`)
    i++
}
```



##### 2.for循环

```javascript
for(let i=0;i<10;i++){
    console.log(i)
}
```

------

### 八.函数

##### 声明 function 函数名( 参数 )

```javascript
function mx(a, b) {
    if (a > b) {
      return a;
    } else {
      return b;
    }
}
```

##### 匿名函数

```javascript
let fn = function(a, b) {
    if (a > b) {
      return a;
    } else {
      return b;
    }
}//将函数赋值给fn 也称为函数表达式  必须声明后再调用
```

##### 立即执行函数

```javascript
(function getSum(x,y){ console.log(x+y)})(1,2);  //3

(function (x,y){ console.log(x+y)}(1,2));

//两种写法  可避免全局变量间的污染  结尾必须加';'
```

------

### 九.对象

##### 对象声明

```javascript
let obj = {} 
let obj= nwe Object()//两种声明方法

let person={
	name:'jack',
    age:18,
    gender:'male'
    'nick-name':'jim'
    
    sayHello: function(){     //对象的方法 可以添加实参形参
		alert('Hello world!')
    }
}

```

##### 对象的增删改查

###### 增

```javascript
person.hobby='rap'  //增加hobby属性   对象名.新属性
```

###### 删

```javascript
delete person.gender  //删除gender属性
```

###### 改

```javascript
person.age = 20  //修改age为20
```

###### 查（属性访问）

```javascript
alert(person.name)//访问name='jack'   对象名.属性

alert(person['nick-name'])//第二种写法 对象名[属性名]
alert(person['age'])   //无论左边是否为字符串，属性名必须加''


person.sayHello() //调用方法
```



##### 遍历对象

```javascript
for(let i in person){  //for in 不推荐用于遍历数组 因为i返回字符串型数组索引
	console.log(i)    //遍历对象 i 返回属性名  'name' 'age'
    console.log(person[i])  
}
```





###  常用数学方法

###### random

```javascript
//左闭右开  
console.log(Math.random())//取0-1之间的随机小数
console.log(Math.random()*10)//0-10之间的随机小数

//0-10之间的随机整数 可以取到10
console.log(Math.floor(Math.random()*(10+1))) 

//取N-M间的随机整数
Math.floor(Math.random()*(M-N+1))+N


```



###### 其它

```javascript
// 圆周率
console.log(Math.PI)


// 向上取整
console.log(Math.ceil(1.1))//2
console.log(Math.ceil(1.5))//2



// 向下取整
console.log(Math.floor(1.1))//1
console.log(Math.floor(1.5))//1



// 四舍五入
console.log(Math.round(1.1))//1
console.log(Math.round(1.49))//1
console.log(Math.round(1.5))//2
console.log(Math.round(1.9))//2

console.log(Math.round(-1.1))//-1
console.log(Math.round(-1.49))//-1
console.log(Math.round(-1.5))//-1   注意这里是向小取整
console.log(Math.round(-1.51))//-2
console.log(Math.round(-1.9))//-2



console.log(Math.max(1,2,3,4))//4
console.log(Math.min(1,2,3,4))//1

 console.log(Math.abs(-1))//1   取绝对值
console.log(Math.pow(2,3))//8   2的3次方
console.log(Math.sqrt(9))//3   开方


```

