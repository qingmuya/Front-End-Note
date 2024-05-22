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