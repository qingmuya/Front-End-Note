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




### 自定义脚本

改写package.json，添加自己需要的语句

```json
"scripts": {
    "build": "babel src\\example.js -o dist\\comiled.js"
},
```

直接使用npm指令即可运行脚本

```bash
npm run build
```



## 模块化

### CommonJS规范

​		对于JS代码而言，其代码量繁多，而且其并没有像Java、Python一样可以直接使用`import`导入其他代码并使用其中的方法，JS并不是一种模块化编程语言，但是通过CommonJS规范可以实现模块化开发：即每个文件是一个独立的模块。

​		使用CommonJS进行模块化开发时，使用`module.exports`方法将本文件中的方法导出，其他文件只需要导入本文件即可使用本模块中的方法。

导出过程如下：

```js
// 存在四个方法：加减乘除
module.exports = {
    sum,
    sub,
    mul,
    di
}
// 以上写法是将方法名直接设置为方法名，实际上可以替换，如：
module.exports = {
    sum:sum1
}
// 即将本文件中的sum方法导出为sum1方法，其他文件调用本模块时使用sum1方法。
```

导入过程如下：

```js
const m = require('文件路径，即模块位置')
m.sum(1, 1)
```





### ES6规范

对于ES6的语法相对要简单

对于导出而言，有两种方式

- 对每个方法前加`export`修饰，导出该函数，如下

```js
export function getList(){
    console.log("获取数据列表");
}
```

- 使用export default控制导出域，其内部方法均会被导出

```js
export default{
    getList(){
        console.log("获取数据列表");
    }
}
```



导入方法同样有两种

- 控制导入方法，使用时直接调用即可

```js
import {getList} from '模块位置'
```

- 全部导入，调用时要使用模块.方法名使用

```js
import user from '模块位置'
```



注意：浏览器默认不支持ES6语法，需要使用Babel降级为ES2015



## WebPack

使用WebPack可以将js文件、css文件打包并加密，简化了文件数量



### 合并JS

创建nodejs项目之后，如有js代码，将其归类到一个目录下，并准备好一个入口文件main.js，就是对模块集中进行引入

在根目录下定义一个webpack.config.js文件配置打包的规则，最后执行`webpack`命令进行打包

在webpack.config.js中应按照如下配置:

```js
// 导入path模块：nodejs内置模块
const path = require("path");

// 定义JS打包的规则
module.exports = {
    // 入口函数从哪里开始进行
    entry:"./src/main.js",
    // 编译成功后把内容输出到哪里去
    output:{
        // 定义属于出的指定目录，__dirname代表当前项目根目录，生成dist文件夹
        path:path.resolve(__dirname, "./dist"),
        // 合并的js文件存储在dist/bundule.js文件中
        filename:"bundle.js"
	}
}
```



### 合并CSS

合并CSS需要先使用npm安装style-loader和css-loader，再到webpack.config.js配置规则，最后创建一个main.js，第一行引入style.css，编译即可。

webpack.config.js内部应如此定义：

```js
module.exports = {
    ...
    module:{
        rule:[{
            test:/\.css$/,	// 把项目中所有的.css结尾的文件进行打包
            use:["style-loader","css-loader"]
        }]
    }
}
```



## VUE

> 渐进式JS框架



### 安装VUE

使用`npm init vue@version`命令即可完成安装。

再次使用`npm install`命令将所需拓展下载即可。



### 模板语法

#### 文本插值

最基本的数据绑定形式，使用“Mustache”语法（即双大括号）

```vue
<template>
    <p>{{ msg }}</p>
</template>

<script>
export default{
    data(){
        return {
            msg:"这是一个p标签"
        }
    }
}
</script>
```



#### Js表达式

每个绑定仅支持**单一表达式**，也就是一段可以代表某数值的js代码。例如`let a = 3`是一个赋值语句，其本身不能代表一个具体的数值，所以不可绑定使用。

需要注意的是其也不支持条件控制，但是可以改为三元表达式：这也对应了其单一表达式的性质。

```vue
<template>
    <p>{{ num + 1 }}</p>
    <p>{{ ok ? "Yes" : "No" }}</p>
    <p>{{ msg.split("").reverse().join("") }}</p>
</template>

<script>
export default{
    data(){
        return {
            num:10,
            ok:true,
            msg:"0123456789"
        }
    }
}
</script>
```





#### 原始HTML

双大括号会将数据插值转换为纯文本而不是解析为HTML，可以使用`v-html`标签插入HTML。

```vue
<template>
    <p v-html="link"></p>
</template>

<script>
export default{
    data(){
        return {
            link:"<a href='https://www.baidu.com'>百度</a>"
        }
    }
}
</script>
```



### 属性绑定

使用`v-bind`注明属性，无需使用双大括号，直接引用即可。

```vue
<template>
    <div v-bind:id="id" v-bind:class="class">
        测试
    </div>
</template>

<script>
export default{
    data(){
        return {
            class:"appclass",
            id:"appid"
        }
    }
}
</script>
```

需要注意的是如果绑定的值是`null`或者`undefined`，那么该属性将会从渲染的元素上移除。

同时可以将v-bind直接简写为`:`

此外还可以**动态绑定多个值**

```vue
<template>
    <div v-bind="Attrs">测试</div>
</template>

<script>
export default{
    data(){
        return {
            Attrs: {
                id:"id",
                class:"class"
            }
        }
    }
}
</script>
```



### 条件渲染

#### v-if

用于条件性地渲染一块内容，这块内容只会在指令地表达式返回值为真时才会被渲染。



#### v-show

也可以控制渲染，与上面用法一致，但是i其无法多分支判断。



二者之间地不同之处在于：

- `v-if`是真实的按照条件渲染，在判断条件切换时，条件区块内的事件监听器和子组件都会被销毁与重建。`v-if`也是**惰性**的，如果在首次渲染时条件之为false，则不会做任何事，只有当条件首次变为true时才会渲染。
- `v-show`不论初始条件如何都会渲染，只有css的`display`属性会切换

> 总的来说，v-if有更高的切换开销，而v-show有更高的初始化渲染开销。因此，如果需要频繁切换，则使用v-show较好；如果在运行时绑定条件很少改变，则v-if会更合适。



### 列表渲染

通过使用`v-for`指令基于一个数组渲染一个列表。`v-for`指令的值需要使用`item in items`形式的特殊语法，其中`items`是源数据的数组，而`item`是迭代项的别名。此处可以使用`of`代替`in  `

```vue
<template>
    <p v-for="name in names">{{ name }}</p>
</template>

<script>
export default{
    data(){
        return {
            names:['丁真', '理塘', '雪豹']
        }
    }
}
</script>
```

 

v-for也支持使用可选的第二个参数表示当前项的位置索引

```vue
<template>
    <p v-for="name,index in names">{{ index }}:{{ name }}</p>
</template>

<script>
export default{
    data(){
        return {
            names:['丁真', '理塘', '雪豹']
        }
    }
}
</script>
```

其也支持三个参数，也就是`key`对应的值，需要注意的是遍历顺序为`value-key-index`

```vue
<template>
    <p v-for="value, key, index in names">{{ index }}-{{ key }}:{{ value }}</p>
</template>

<script>
export default{
    data(){
        return {
            names:{
                name:'顶针',
                address:'理塘',
                pony:'雪豹'
            }
        }
    }
}
</script>
```



#### 通过key管理状态

对于v-for循环产生的元素，应定义一个唯一的`key`属性方便vue追踪每个节点的标识，从而重用和重新排序现有的元素。

```vue
<template>
    <p v-for="name, index in names" :key="index">{{ name }}</p>
</template>

<script>
export default{
    data(){
        return {
            names:['理塘', '丁真', '珍珠']
        }
    }
}
</script>
```

`key`是一个通过`v-bind`绑定的特殊属性，`key`绑定的值期望是一个基础类型的值，例如字符串或number类型。  

注意，`key`的值应该是不会变动的，所以不要使用index。



### 事件处理

可以使用`v-on`指令（简写为`@`）来监听DOM时间，并在时间触发时执行对应的JavaScript。用法：`v-on:click="methodName"`或`@click="handler"`。

事件处理器的值可以是：

1. **内联事件处理器**：时间被触发时执行的内联JavaScript语句(与onclick类似)
2. **方法事件处理器**：一个指向组件上定义的方法的属性名或是路径



#### 内联事件处理器

适用于简单场景

```vue
<template>
    <button @click="num++">add</button>
    <p>{{ num }}</p>
</template>

<script>
export default{
    data(){
        return {
            num:0
        }
    }
}
</script>
```



#### 方法事件处理器

适用于复杂场景

```vue
<template>
    <button @click="addNum">add</button>
    <p>{{ num }}</p>
</template>

<script>
export default{
    data(){
        return {
            num:0
        }
    },
    methods:{
        addNum(){
            this.num++
        }
    }
}
</script>
```



### 事件传参

事件参数可以获取`event`对象和通过事件传递数据



#### 获取event对象

直接获取e即可

```vue
<template>
    <button @click="addNum">add</button>
    <p>{{ num }}</p>
</template>

<script>
export default{
    data(){
        return {
            num:0
        }
    },
    methods:{
        addNum(e){
            e.target.innerHTML = "add " + this.num;
            this.num++
        }
    }
}
</script>
```



#### 传递参数过程中获取event

需要在`event`前添加`$`

```vue
<template>
    <p @click="getNameHandler(name, $event)" v-for="(name, index) in names" :key="index">{{ name }}</p>
</template>

<script>
export default{
    data(){
        return {
            names:['理塘', '丁真', '珍珠']
        }
    },
    methods:{
        getNameHandler(name, e){
            console.log(name)
            console.log(e)
        }
    }
}
</script>
```



### 事件修饰符

在处理事件时调用event.preventDefault()或event.stopPropagation()是很常见的。尽管我们可以直接在方法内调用，但如果方法能更专注于数据逻辑而不用去处理DOM事件的细节会更好。

常用的事件修饰符有：

- .stop
- .prevent
- .once
- .enter



#### 阻止默认事件

通过方法体进行阻止

```vue
<template>
    <a @click="clickHandler" href="www.baidu.com">百度</a>
</template>

<script>
export default{
    data(){
        return {}
    },
    methods:{
        clickHandler(e){
            e.preventDefault()
        }
    }
}
</script>
```

通过修饰符直接阻止

```vue
<template>
    <a @click.prevent href="www.baidu.com">百度</a>
</template>

<script>
export default{
    data(){
        return {}
    },
}
</script>
```



#### 阻止事件冒泡

```vue
<template>
    <div @click="clickdiv">
        <p @click.stop="clickp">你好</p>
    </div>
</template>

<script>
export default{
    data(){
        return {}
    },
    methods:{
        clickdiv(){
            console.log("div")
        },
        clickp(){
            console.log("p")
        }
    }
}
</script>
```



### 数组变化侦测

#### 变更方法

Vue能够侦听响应式数组的变更方法，并在它们被调用时触发相关的更新。这些变更方法包括:

push()、pop()、shift()、unshift()、splice、sort()、reverse()

也就是说在调用这些方法后，数据会立即更新同时引起页面的变化。

```vue
<template>
    <button @click="addName">添加数据</button>
    <li v-for="name, index in names" :key="index">{{ name }}</li>
</template>

<script>
export default{
    data(){
        return {
            names:['理塘', '丁真', '珍珠']
        }
    },
    methods:{
        addName(){
            this.names.push('雪豹')
        }
    }
}
</script>
```



#### 替换一个数组

变更方法，顾名思义，就是会对调用它们的原数组进行变更。相对地，也有一些不可变(immutable)方法，例如`fiter()`，`concat()`和`slice()`，这些都不会更改原数组，而总是返回一个新数组。当遇到的是非变更方法时，我们需要将旧的数组替换为新的

```vue
<template>
    <button @click="addall">合并数据</button>
    <li v-for="name, index in names" :key="index">{{ name }}</li>
</template>

<script>
export default{
    data(){
        return {
            names:['理塘', '丁真', '珍珠'],
            names1:['原神']
        }
    },
    methods:{
        addall(){
            this.names = this.names.concat(this.names1)
        }
    }
}
</script>
```



### 计算属性

模板中的表达式虽然方便，但也只能用来做简单的操作。如果在模板中写太多逻辑，会让模板变得臃肿，难以维护。因此推荐使用计算属性来描述依赖响应式状态的复杂逻辑 。

```vue
<template>
    <h1>{{ title }}</h1>
    <p>{{ IsTitleExist }}</p>
</template>

<script>

export default{
    data(){
        return {
            title:"这是一个标题"
        }
    },
    computed:{
        IsTitleExist(){
            return this.title.length > 0 ? 'Yes' : 'No'
        }
    }
}
</script>
```

区别在于计算属性值会基于其响应式依赖被缓存。一个计算属性仅会在其响应式依赖更新时才重新计算；方法调用总是会在重渲染发生时再次执行函数。

也就是说在对一些多用的渲染实例使用计算属性会节省性能。



### Class绑定

数据绑定的一个常见需求场景是操纵元素的CSS class列表，因为`class`是attribute，我们可以和其他attribute一样使用`v-bind`将它们和动态的字符串绑定。但是，在处理比较复杂的绑定时，通过拼接生成字符串是麻烦且易出错的。因此，Vue专门为`class`的`v-bind`用法提供了特殊的功能增强。除了字符串外，表达式的值也可以是对象或数组。

即可以在数组中嵌套渲染样式。

```vue
<template>
    <p :class="classobject">这是一段文字</p>
</template>

<script>

export default{
    data(){
        return {
            classobject:{
                'isactive':true,
                'text-red':true
            }
        }
    }
} 
</script>
<style>
.isactive{
    font-size: 30px;
}
.text-red{
    color:red;
}
</style>
```

只能数组嵌套对象而不能对象嵌套数组。



### Style绑定

数据绑定的一个常见需求场景是操纵元素的CSS style列表，因为`style`是attribute，我们可以和其他attribute一样使用`v-bind`将它们和动态的字符串绑定。但是，在处理比较复杂的绑定时，通过拼接生成字符串是麻烦且易出错的。因此,Vue 专门为style的v-bind用法提供了特殊的功能增强。除了字符串外，表达式的值也可以是对象或数组

与Class绑定一致



### 侦听器

可以使用`watch`选项在每次响应式属性发生变化时触发一个函数，该函数的名称必须与文本插值的变量名一致。
当数据发生变化后，都会自动执行`watch`标签内的同名函数。

```vue
<template>

    <p>{{ message }}</p>

    <button @click="updatevalue">修改数据</button>

</template>

  

<script>

  

export default{

    data(){

        return {

            message:"Hello World!"

        }

    },

    methods:{

        updatevalue(){

            this.message = "理塘丁真"

        }

    },

    watch:{

        // 这两个变量名随意命名，顺序是改变后变量和改变前数据

        message(newValue, oldValue){

            // 数据发送变化时自动执行

            console.log(newValue, oldValue)

        }

    }

}

</script>
```



### 表单输入绑定

在前端处理表单时，我们常常需要将表单输入框的内容同步给JavaScript 中相应的变量。手动连接值绑定和更改事件监听器可能会很麻烦, `v-model`指令简化了这一步骤：可以简化理解为双向绑定。

```vue
<template>

    <input type="text" v-model="message">

    <p>{{ message }}</p>

</template>

  

<script>

  

export default{

    data(){

        return {

            message:""

        }

    }

}

</script>
```

#### 复选框

可以绑定布尔数值。

```vue
<template>

    <input type="checkbox" id="checkbox" v-model="check" />

    <label for="checkbox">{{ check ? 'Yes' : 'No' }}</label>

</template>

  

<script>

  

export default{

    data(){

        return {

            check:false

        }

    }

}

</script>
```



#### 修饰符

v-`model`也提供了修饰符：`.lazy`、`.number`、`.trim`

##### .lazy

默认情况下，`v-model`会在每次`input`事件后更新数据。你可以添加`lazy`修饰符来改为在每次`change`事件后更新数据。

```vue
<template>

    <input type="text" v-model.lazy="message">

    <p>{{ message }}</p>

</template>

  

<script>

  

export default{

    data(){

        return {

            message:"",

        }

    }

}

</script>
```



### 模板引用

虽然Vue的声明性渲染模型为你抽象了大部分对DOM的直接操作，但在某些情况下，我们仍然需要直接访问底层DOM元素。要实现这一点，我们可以使用特殊的`ref` 属性。

挂载结束后引用都会被暴露在`this.$refs`之上。

```vue
<template>

    <div ref="temp" class="newdiv">{{ content }}</div>

    <input type="text" ref="name">

    <button @click="update">修改数据</button>

</template>

  

<script>

  

export default{

    data(){

        return {

            content:"此处可更改"

        }

    },

    methods:{

        update(){

            this.$refs.temp.innerHTML = this.$refs.name.value

        }

    }

}

</script>
```



### 组件组成

组件最大的优势就是可复用性；当使用构建步骤时，一般会将Vue 组件定义在一个单独的`.vue`文件中，这被叫做单文件组件(简称SFC)

```vue
<template>

    <!-- 标签形式 -->

    <newVue />

    <!-- 修改命名 -->

    <new-vue />

</template>

  

<script>

  

import newVue from "./components/newVue.vue"

  

export default{

    components:{

        newVue

    }

}

</script>
```

scoped：让当前样式只在当前组件中生效。



### 组件嵌套关系

> 组件允许我们将UI划分为独立的、可重用的部分，并且可以对每个部分进行单独的思考。在实际应用中，组件常常被组织成层层嵌套的树状结构。
> 
> 这和我们嵌套HTML元素的方式类似，Vue实现了自己的组件模型，使我们可以在每个组件内封装自定义内容与逻辑。