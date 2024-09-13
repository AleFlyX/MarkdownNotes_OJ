## 使用箭头函数编写简洁的匿名函数

~~~
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
ES6 提供了其他写匿名函数的方式的语法糖。 你可以使用箭头函数：

const myFunc = () => {
  const myVar = "value";
  return myVar;
}
当不需要函数体，只返回一个值的时候，箭头函数允许你省略 return 关键字和外面的大括号。 这样就可以将一个简单的函数简化成一个单行语句。

const myFunc = () => "value";
这段代码默认会返回字符串 value。


##########

编写带参数的箭头函数
和一般的函数一样，你也可以给箭头函数传递参数。

const doubler = (item) => item * 2;
doubler(4);
doubler(4) 将返回 8。

如果箭头函数只有一个参数，则可以省略参数外面的括号。

const doubler = item => item * 2;
可以给箭头函数传递多个参数。

const multiplier = (item, multi) => item * multi;
multiplier(4, 2);
multiplier(4, 2) 将返回 8。



############
设置函数的默认参数
ES6 里允许给函数传入默认参数，来构建更加灵活的函数。

请看以下代码：

const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John"));
console.log(greeting());
控制台将显示字符串 Hello John 和 Hello Anonymous。

默认参数会在参数没有被指定（值为 undefined）的时候起作用。 在上面的例子中，参数 name 会在没有得到新的值的时候，默认使用值 Anonymous。 你还可以给多个参数赋予默认值。


~~~


## rest操作符

~~~
 rest 操作符可以用于创建有一个变量来接受多个参数的函数。 这些参数被储存在一个可以在函数内部读取的数组中。

请看以下代码：

function howMany(...args) {  #此时args自动变成数组
  return "You have passed " + args.length + " arguments.";
}

console.log(howMany(0, 1, 2));
console.log(howMany("string", null, [1, 2, 3], { }));
控制台将显示字符串 You have passed 3 arguments. 和 You have passed 4 arguments.。

rest 参数使我们不需要使用 arguments 对象，允许我们对传递给函数 howMany 的参数数组使用数组方法。
~~~

## 使用 spread 运算符展开数组项
~~~
下面的 ES5 代码使用了 apply() 来计算数组的最大值：

var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr);
maximus 的值为 89。

我们必须使用 Math.max.apply(null, arr)，因为 Math.max(arr) 返回 NaN。 Math.max() 函数中需要传入的是一系列由逗号分隔的参数，而不是一个数组。 展开操作符可以提升代码的可读性，使代码易于维护。

const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr);
maximus 的值应该是 89。

...arr 返回一个解压缩的数组。 换句话说，它展开了数组。 然而，展开操作符只能够在函数的参数中或者数组中使用。 例如：

const spreaded = [...arr];
下面的代码将不能运行：

const spreaded = ...arr;


使用展开操作符将 arr1 中的全部内容复制到另一个数组 arr2 中。

const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;

arr2 = [...arr1];  


~~~

## 使用解构赋值来获取对象的值

~~~
解构赋值是 ES6 引入的新语法，用来从数组和对象中提取值，并优雅地对变量进行赋值。

有如下 ES5 代码：

const user = { name: 'John Doe', age: 34 };

const name = user.name;
const age = user.age;
name 的值应该是字符串 John Doe， age 的值应该是数字 34。

下面是使用 ES6 解构赋值语句，实现相同效果：

const { name, age } = user;
同样，name 的值应该是字符串 John Doe， age 的值应该是数字 34。

在这里，自动创建 name 和 age 变量，并将 user 对象相应属性的值赋值给它们。 这个方法简洁多了。

你可以从对象中提取尽可能多或很少的值。


把两个赋值语句替换成效果相同的解构赋值语句。 today 和 tomorrow 的值应该还是 HIGH_TEMPERATURES 对象中 today 和 tomorrow 属性的值。

const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};
/*修改前
const today = HIGH_TEMPERATURES.today;
const tomorrow = HIGH_TEMPERATURES.tomorrow;
*/
//修改后
const {today,tomorrow} = HIGH_TEMPERATURES;
~~~

## 使用解构赋值从对象中分配变量
~~~
可以给解构的值赋予一个新的变量名， 通过在赋值的时候将新的变量名放在冒号后面来实现。

还是以上个例子的对象来举例：

const user = { name: 'John Doe', age: 34 };
这是指定新的变量名的例子：

const { name: userName, age: userAge } = user;
你可以这么理解这段代码：获取 user.name 的值，将它赋给一个新的变量 userName，等等。 userName 的值将是字符串 John Doe，userAge 的值将是数字 34。


####################


使用解构赋值语句替换两个赋值语句。 将 HIGH_TEMPERATURES 的 today 和 tomorrow 的值赋值给 highToday 和 highTomorrow。
const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};

//修改这一行下面的代码

const highToday = HIGH_TEMPERATURES.today;
const highTomorrow = HIGH_TEMPERATURES.tomorrow; 
//修改后
const {today:highToday,tomorrow:highTomorrow}= HIGH_TEMPERATURES;

/***********************/
大概结构：const {原对象元素1:你想赋值的变量名1，原对象元素2:你想赋值的变量名2，......}=原对象名字   

而且这种结构可以用于嵌套对象中
/***********************/
~~~

~~~
/************************/
数组例子：


与数组解构不同，数组的扩展运算会将数组里的所有内容分解成一个由逗号分隔的列表。 所以，你不能选择哪个元素来给变量赋值。

而对数组进行解构却可以让我们做到这一点：

const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b);
控制台将显示 a 和 b 的值为 1, 2。

数组的第一个值被赋值给变量 a，数组的第二个值被赋值给变量 b。 我们甚至能在数组解构中使用逗号分隔符，来获取任意一个想要的值：

const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);
控制台将显示 a、b 和 c 的值为 1, 2, 5。

##################

使用数组解构来交换变量 a 与 b 的值，使 a 接收 b 的值，而 b 接收 a 的值。
let a = 8, b = 6;

[a,b]=[b,a]
~~~

## 通过 rest 参数解构
在解构数组的某些情况下，我们可能希望将剩下的元素放进另一个数组里面。

以下代码的结果与使用 Array.prototype.slice() 类似：
~~~
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);
console.log(arr);
控制台将显示 1, 2 和 [3, 4, 5, 7]。

变量 a 和 b 分别接收数组的第一个和第二个值。 之后，因为 rest 语法，arr 以数组形式接收了剩余的值。 rest 参数只能对数组列表最后的元素起作用。 这意味着你不能使用 rest 语法来省略原数组最后一个元素、截取中间的元素作为子数组。

#####################

使用一个带有 rest 语法的解构赋值来模拟 Array.prototype.slice() 的行为。 removeFirstTwo() 应该返回原始数组 list 的子数组，前两个元素被省略。
function removeFirstTwo(list) {
  let [,,...arr]=list;
  return arr;
}

const source = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const sourceWithoutFirstTwo = removeFirstTwo(source);
~~~

## 使用解构赋值将对象作为函数的参数传递
~~~
在某些情况下，你可以在函数的参数里直接解构对象。

请看以下代码：

const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;

}
上面的操作解构了传给函数的对象。 这样的操作也可以直接在参数里完成：

const profileUpdate = ({ name, age, nationality, location }) => {

}
当 profileData 被传递到上面的函数时，从函数参数中解构出值以在函数内使用。

######################################
对 half 的参数进行解构赋值，仅将 max 与 min 的值传进函数。

const stats = {
  max: 56.78,
  standard_deviation: 4.34,
  median: 34.54,
  mode: 23.87,
  min: -0.75,
  average: 35.85
};

// 只修改这一行下面的代码
const half = (stats) => (stats.max + stats.min) / 2.0; 
// 只修改这一行上面的代码

const half = ({min ,max}) => (min+max)/ 2.0; 

~~~

## 使用模板字面量创建字符串
模板字符串是 ES6 的另外一项新的功能。 这是一种可以轻松构建复杂字符串的方法。

模板字符串可以使用多行字符串和字符串插值功能。
# *记得用tmd反引号 ```````````*
请看以下代码：
~~~
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);


~~~

## 使用简单字段编写简洁的对象字面量声明

请看以下代码：
~~~
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
getMousePosition 简单的函数，返回拥有两个属性的对象。 ES6 提供了一个语法糖，消除了类似 x: x 这种冗余的写法。 你可以只写一次 x，解释器会自动将其转换成 x: x（或效果相同的内容）。 下面是使用这种语法重写的同样的函数：

const getMousePosition = (x, y) => ({ x, y });

请使用简单属性对象的语法来创建并返回一个具有 name、age 和 gender 属性的对象。
const createPerson = (name, age, gender) => {
  // 只修改这一行下面的代码
   return {
    name: name,
    age: age,
    gender: gender
  };
  ////////////////////////////
  //修改后
const createPerson = (name, age, gender) => ({name,age,gender})
  
~~~

## 简洁函数声明

~~~
在 ES5 中，当我们需要在对象中定义一个函数的时候，必须像这样使用 function 关键字：

const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
用 ES6 的语法在对象中定义函数的时候，可以删除 function 关键词和冒号。 请看以下例子：

const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};

##########################

使用以上这种简短的语法，重构在 bicycle 对象中的 setGear 函数。
// 只修改这一行下面的代码
const bicycle = {
  gear: 2,
  setGear: function(newGear) {
    this.gear = newGear;
  }
};
// 只修改这一行上面的代码
bicycle.setGear(3);
console.log(bicycle.gear);
/////////////////////修改后

// 只修改这一行下面的代码
const bicycle = {
  gear: 2,
  setGear(newGear) {  ###########只是删了冒号和function
    this.gear = newGear;
  }
};
// 只修改这一行上面的代码
bicycle.setGear(3);
console.log(bicycle.gear);
~~~


## 用 export 来重用代码块
假设有一个文件 math_functions.js，该文件包含了数学运算相关的一些函数。 其中一个存储在变量 add 里，该函数接受两个数字作为参数返回它们的和。 你想在几个不同的 JavaScript 文件中使用这个函数。 要实现这个目的，就需要 export 它。

~~~
export const add = (x, y) => {
  return x + y;
}
上面是导出单个函数常用方法，还可以这样导出：

const add = (x, y) => {
  return x + y;
}

export { add };
导出变量和函数后，就可以在其它文件里导入使用从而避免了代码冗余。 重复第一个例子的代码可以导出多个对象或函数，在第二个例子里面的导出语句中添加更多值也可以导出多项，例子如下：

export { add, 其他函数（比如add2....）};

~~~

### 通过 import 复用 JavaScript 代码

import 可以导入文件或模块的一部分。 在之前的课程里，例子从 math_functions.js 文件里导出了 add。 下面看一下如何在其它文件导入它：

~~~
import { add } from './math_functions.js';
在这里，import 会在 math_functions.js 里找到 add，只导入这个函数，忽略剩余的部分。 ./ 告诉程序在当前文件的相同目录寻找 math_functions.js 文件。 用这种方式导入时，相对路径（./）和文件扩展名（.js）都是必需的。

通过在 import 语句里添加项目，可以从文件里导入多个项目，如下：

import { add, subtract } from './math_functions.js';

~~~

### 用 * 从文件中导入所有内容
假设你有一个文件，你希望将其所有内容导入到当前文件中。 可以用 import * as 语法来实现。 下面是一个从同目录下的 math_functions.js 文件中导入所有内容的例子：
~~~
import * as myMathModule from "./math_functions.js";
~~~

上面的 import 语句会创建一个叫作 myMathModule 的对象。 这只是一个变量名，可以随便命名。 对象包含 math_functions.js 文件里的所有导出，可以像访问对象的属性那样访问里面的函数。 下面是使用导入的 add 和 subtract 函数的例子：
~~~
myMathModule.add(2,3);
myMathModule.subtract(5,3);
~~~

### 用 export default 创建一个默认导出
在 export 的课程中，你学习了命名导出语法， 这可以在其他文件中引用一些函数或者变量。

还需要了解另外一种被称为默认导出的 export 的语法。 在文件中只有一个值需要导出的时候，通常会使用这种语法。 它也常常用于给文件或者模块创建返回值。

下面是使用 export default 的例子：
```
export default function add(x, y) {
  return x + y;
}

export default function(x, y) {
  return x + y;
}
第一个是命名函数，第二个是匿名函数。

export default 用于为模块或文件声明一个返回值，在每个文件或者模块中应当只默认导出一个值。 此外，你不能将 export default 与 var、let 或 const 同时使用。
```

### 导入一个默认的导出
学习了 export default 的用法。 还需要一种 import 的语法来导入默认的导出。 在下面的例子里，add 是 math_functions.js 文件的默认导出。 以下是如何导入它：

```
import add from "./math_functions.js";
这个语法有一处特别的地方， 被导入的 add 值没有被花括号（{}）所包围。 add 只是一个变量的名字，对应 math_functions.js 文件的任何默认导出值。 在导入默认导出时，可以使用任何名字。
```

## 创建一个 JavaScript Promise
Promise 是异步编程的一种解决方案 - 它在未来的某时会生成一个值。 任务完成，分执行成功和执行失败两种情况。 Promise 是构造器函数，需要通过 new 关键字来创建。 构造器参数是一个函数，该函数有两个参数 - resolve 和 reject。 通过它们来判断 promise 的执行结果。 用法如下：
```
const myPromise = new Promise((resolve, reject) => {

});
```

### 通过 resolve 和 reject 完成 Promise
Promise 有三个状态：pending、fulfilled 和 rejected。 上一个挑战里创建的 promise 一直阻塞在 pending 状态里，因为没有调用 promise 的完成方法。 Promise 提供的 resolve 和 reject 参数就是用来结束 promise 的。 Promise 成功时调用 resolve，promise 执行失败时调用 reject， 如下文所述，这些方法需要有一个参数。
```
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```

上面的示例使用字符串作为这些函数的参数，但参数实际上可以是任何格式。 通常，它可能是一个包含数据的对象，你可以将它放在网站或其他地方。

## 用 then 处理 Promise 完成的情况
当程序需要花费未知的时间才能完成时（比如一些异步操作），一般是服务器请求，promise 很有用。 服务器请求会花费一些时间，当结束时，需要根据服务器的响应执行一些操作。 这可以用 then 方法来实现，

~~~
Promise.prototype.then(onFulfilled, onRejected)
~~~
then方法调度回调函数，以便最终完成Promise——要么实现，要么拒绝。将执行oncompleted和onRejected处理程序之一来处理当前承诺的完成或拒绝。当promise被resolve完成时，onfulfillment处理程序被调用。

~~~
myPromise.then(result => {

});
result 即传入 resolve 方法的参数。



给 promise 添加 then 方法。 用 result 做为回调函数的参数并将 result 打印在控制台。

const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer 设置为 true，表示从服务器获得有效响应
  let responseFromServer = true;
  makeServerRequest.then(result=>{});
  console.log(result);
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});
~~~

### 使用 catch 处理 Promise 失败的情况
当 promise 失败时会调用 catch 方法。 当 promise 的 reject 方法执行时会直接调用。 用法如下：

myPromise.catch(error => {

});
error 是传入 reject 方法的参数。

```
给 promise 添加 catch 方法。 用 error 作为回调函数的参数，并把 error 打印到控制台。

const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer 设置为 false，表示从服务器获得无效响应
  let responseFromServer = false;
  makeServerRequest.catch(error=>{});
  console.log(error);
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {
  console.log(result);
});

```


# 总结
ES6中的多个新特性，主要包括箭头函数、解构赋值、模板字符串、Promise等。以下是这些特性的总结：

### 箭头函数
- **语法简洁**：使用`=>`符号定义，比传统的`function`关键字更简洁。
- **自动绑定`this`**：箭头函数不会创建自己的`this`上下文，而是继承父执行上下文中的`this`值。
- **无参数或单个参数**：可以省略小括号，当函数体只有一行时，可以省略`return`和大括号。

### 解构赋值
- **数组解构**：可以从数组中提取数据到不同的变量中。
- **对象解构**：可以从对象中提取数据到不同的变量中，甚至可以重命名变量。
- **用途广泛**：用于交换变量值、从函数返回多个值等场景。

### 模板字符串
- **使用反引号**：用反引号`` ` ``包围的字符串，可以嵌入表达式。
- **多行字符串**：支持跨越多行的字符串。
- **表达式插值**：通过`${}`插入变量或表达式的结果。

### Promise
- **异步编程**：用于处理异步操作，如网络请求。
- **三种状态**：pending（进行中）、fulfilled（已成功）、rejected（已失败）。
- **方法**：
  - `resolve()`：将Promise对象的状态从“pending”变为“fulfilled”。
  - `reject()`：将Promise对象的状态从“pending”变为“rejected”。
  - `then()`：处理Promise成功的情况。
  - `catch()`：处理Promise失败的情况。

### rest参数和spread运算符
- **rest参数**：用`...`表示，用于将不定数量的参数表示为一个数组。
- **spread运算符**：用`...`表示，用于在函数调用或数组字面量扩展数组元素。

### 默认参数
- **语法**：在函数参数列表中，可以指定默认值，如果调用函数时未提供该参数，则使用默认值。

### 简洁的对象字面量声明
- **ES6允许**：在对象字面量中直接使用变量名作为属性名，而不需要显式指定键名。

### 模块
- **export**：用于导出模块中的函数、对象或原始值，以便其他JavaScript文件通过import语句使用。
- **import**：用于导入模块中导出的内容。可以使用`import * as`导入模块中的所有导出内容，或使用`import { export1, export2 }`导入特定的导出内容。
