# **JavaScript基本语法整理**

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



### 二.变量

```javascript
let name = '张三' //声明和赋值
alert(name)  //输出'张三'
name='李四
alert(name)

//同一变量不能重复声明
```

### 三.常量

```javascript
const PI=3.14;
alert(PI);

const G=9.8;
alert(G);
```



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

