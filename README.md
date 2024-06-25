# Front-End-Note



## ES6

> ES6， 全称 ECMAScript 6.0 ，是 JavaScript 的下一个版本标准，2015.06 发版。
>
> ES6 主要是为了解决 ES5 的先天不足，比如 JavaScript 里并没有类的概念，但是目前浏览器的 JavaScript 是 ES5 版本，大多数高版本的浏览器也支持 ES6，不过只实现了 ES6 的部分特性和功能。



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



## Babel

Babel的作用在于将ES6代码进行降级，因为部分浏览器的版本较低可能不识别ES6，所以需要使用Babel。

### 创建项目工程的步骤

1. 创建文件夹，使用`npm init -y`命令进行初始化

2. 创建文件src/example.js，加入要写的ES6代码

3. 配置`.babelrc`文件，即创建名为`.babelrc`的文件，存放于项目的根目录下，该文件用于配置转码规则和插件，基本格式如下

   ```json
   {
   	"presets": [], 	// 转码规则，例如"es2015"
   	'plugins': []
   }
   ```

4. 安装转码器，在项目中安装

   ```bash
   npm install --save-dev babel-preset-es2015
   ```

5. 转码

   ```bash
   # 转码结果写入一个文件
   # --out-file 或 -o 参数指定输出文件
   babel src/example.js --out-file dist/compiled.js
   # 或者
   babel src/example.js -o dist/compiled.js
   
   # 整个目录转码
   # --out-dir 或 -d 参数指定输出文件
   babel src --out-dir dist
   # 或者
   babel src -d dist
   ```

   
