# Front-End-Note



## ES6

### let和const和var的区别

let是ES6的一种对于var的改进，它解决了变量穿透问题，使得变量的使用更为安全，限制了作用域；const作为常量解决了var声明的变量的可更改问题。

所谓变量穿透问题：

```javascript
for(var i = 0;i < 5;i++){
	console.log(i);
}
// 这里会造成变量穿透
console.log(i);
```



### 模板字符串

对于模板字符串而言其也是新的特性，对于原始的字符串和变量的拼接需要使用`+`进行连接，而对于ES6的模板字符串而言，其更为简便：

```js
let person = {
	name : "丁真珍珠",
	address : "理塘"
};
let str = `我叫${person.name}，来自${person.address}`;
console.log(str);
```

需要注意的是模板字符串需要使用 ` 进行开头，即波浪键。



### 默认参数

对于函数而言，如果传递的参数个数与预期不符，那么未被传递参数的参数其会被定义为undefined，涉及到其参与运算的部分也会变成undefined。



### 箭头函数

本质上就是lambda表达式，依据语法进行简化即可。



### 对象初始化简写和对象解构

对象的初始化简写实际上就是直接把变量赋值给对象的属性；

对象解构就是抽取对象的若干属性进行赋值，例如：

```js
let info = {
    name:"丁真",
    address:"理塘"
};
let {name, address} = info;
```

同时，对于对象的取值方式也分为两种：通过`.`取值和通过`[]`取值，例如

```js
let info = {
    name:"丁真",
    address:"理塘",
    shuozanghua(){
    	console.log("我测你们🐎");
	}
};

// 通过 . 进行取值
console.log(info.name);
console.log(info.address);
info.shuozanghua();

// 通过 [] 进行取值
console.log(info["name"]);
console.log(info["address"]);
info["shuozanghua"]();
```



### 对象传播操作符

对象传播操作符就是对于对象的解构而言，可以将对象的一部分属性变为一个新的对象，如下

```js
let person = {
    name : "丁真",
    address : "理塘",
    age : 18,
    work : "shuozanghua"
};
let {name, address, ...person2} = person;

console.log(person2);
```



### 数组Map

对于数组而言其有一个实用的方法为map，是数组本身自带的循环，而且会把处理的值回填对应的位置。例如：

```js
let arr = [1,2,3,4,5];

// 传统方式
let newarr = [];
for(let i = 0;i < arr.length;i++){
    newarr.push(arr[i] * 2);
}
console.log(newarr);

// 使用数组自带的map循环，会将处理的值回填对应的位置
let newarr2 = arr.map(ele => ele * 2);
console.log(newarr2);
```



### 数组Reduce

对于数组还有一个方法：Reduce，用户遍历数组且减少所用的参数。如下：

```js
let arr = [1,2,3,4,5,6,7,8,9,10];
let res = arr.reduce((a, b) => a + b);
console.log("res = ", res);
```

