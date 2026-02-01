# JS

## 1.输入输出

---

* 文档输出内容

```js
document.write("我是div标签")
```

* 控制台输出内容

``` js
console.log("我是console输出内容")
```

* 输入

```js
prompt("请输入你的姓名")
```

* 弹出框输出内容

```js
alert("我是弹出框内容")
```

## 2.常量和变量

---

* 声明变量

```js
let age = 18，name = "hyw"
age = 18
console.log(age)
let userNAME = prompt("请输入用户名")
console.log("用户姓名：" + userNAME)
document.write("hello," + userNAME + ", nice to meet you!")
```

* 常量

```js
//常量的基本使用
const PI = 3.14
console.log(PI)
//声明常量必须赋值
```

## 3.数据类型

---

* Number
* String

```js
let age = 18
document.write(`i am ${age} years old`)
```

* Boolean

```js
true / false
let isMale = true
console.log(isMale)
```

* Undefined

```js
let a
console.log(a)
```

* Null

```txt
空对象
```

* Typeof

```js
console.log(typeof age)
console.log(typeof isMale)
console.log(typeof a)
console.log(typeof null)
```

* 数组

~~~js
// 数组的声明
        let arr = [ "a", "b", "c" ];
        console.log(arr);
        //使用数组 数组名[索引]
        console.log(arr[0]); //a
        //数组长度
        console.log(arr.length); //3
~~~

## 4.运算符

---

~~~js
 //赋值运算符
        let a = 10
        a += 5
        //需要重新赋值

        //一元运算符
        //++自增运算符
        //--自减运算符


        //比较运算符
        //==  !=  ===  !==  >  <  >=  <=
        console.log(3 === 5);
        console.log(3 !== 5);
        console.log(3 > 5);
        console.log(3 < 5);
        console.log(3 >= 5);
        console.log(3 <= 5);
        // 涉及nan都为false
        // 不同类型间比较会转换成隐式类型再比较
        //注意区分==和===的区别，//==比较值是否相等，===比较值和类型是否都相等


        //逻辑运算符
        //&&  ||   !
        //&&与运算，两个操作数都为true，结果才为true
        console.log(true && false); //false
        //||或运算，两个操作数有一个为true，结果就为true
        console.log(true || false); //true
        //!非运算，取反
        console.log(!true); //false

        let num = +prompt("请输入一个数字")
        console.log(num % 4 === 0 && num % 100 !==0);
        alert(Boolean(num % 4 === 0 && num % 100 !==0));
~~~

## 5.隐式转换和显式转换

---

~~~js
////显式转换
        console.log(1+1)

        console.log('1' + 1)  
        //+取消字符串和数字之间的运算，变成字符串拼接
        //结果是'11'

        console.log(1-1)

        console.log('1' - 1)  
        //-不会取消字符串和数字之间的运算，结果是数字0

        console.log(+'12')
        //一元运算符+，把字符串'12'转换成数字12

        console.log(-'12')
        //一元运算符-，把字符串'12'转换成数字12，然后取反，结果是-12


    //隐式转换
        let n = '123'
        console.log(Number(n))

        let num = Number(prompt("请输入一个数字"))
        console.log(num)

        let numBER = +prompt("请输入一个数字")
        console.log(numBER)

        console.log(parseInt('12.34abc'))//结果是12
        console.log(parseFloat('12.34abc'))//结果是12.34
        
        console.log(parseInt('abc12'))//结果是NaN
~~~

## 6.if语句

---

* 单分支

```js
if(条件){
	满足条件要执行的代码
}
```

* 双分支

~~~js
if(){

}else{

}
~~~

## 7.三元运算符

~~~js
条件 ? 满足条件执行代码 : 不满足条件执行代码
~~~

## 8.switch语句

~~~js
switch(数据){
	case 1:
		1
		break
	case 2:
		2
		break
	case 3:
		3
		break
    default:
        console.log('none')
}
~~~

## 9.while语句

~~~js
while(循环条件){
	重复执行代码(循环体)
}
~~~

  
