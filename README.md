

## prompt 和 confirm

### [prompt](https://zh.javascript.info/alert-prompt-confirm#prompt)

`prompt` 函数接收两个参数：

```javascript
result = prompt(title, [default]);
```

浏览器会显示一个带有文本消息的模态窗口，还有 input 框和确定/取消按钮。

- `title`

  显示给用户的文本

- `default`

  可选的第二个参数，指定 input 框的初始值。

### [confirm](https://zh.javascript.info/alert-prompt-confirm#confirm)

语法：

```javascript
result = confirm(question); //返回值为boolean
```

`confirm` 函数显示一个带有 `question` 以及确定和取消两个按钮的模态窗口。

点击确定返回 `true`，点击取消返回 `false`。

## for循环

**标签** 是在循环之前带有冒号的标识符：

```javascript
labelName: for (...) {
  ...
}
```

```js
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    let input = prompt(`Value at coords (${i},${j})`, "");

    // 如果是空字符串或被取消，则中断并跳出这两个循环。
    if (!input) break outer; // (*)

    // 用得到的值做些事……
  }
}
alert("Done!");
```

上述代码中，`break outer` 向上寻找名为 `outer` 的标签并跳出当前循环。

我们还可以将标签移至单独一行：

```javascript
outer:
for (let i = 0; i < 3; i++) { ... }
```

`continue` 指令也可以与标签一起使用。在这种情况下，执行跳转到标记循环的下一次迭代。

**标签并不允许“跳到”所有位置**

标签不允许我们跳到代码的任意位置。

例如，这样做是不可能的：

```javascript
break label;  // 跳转至下面的 label 处（无效）

label: for (...)
```

`break` 指令必须在代码块内。从技术上讲，任何被标记的代码块都有效，例如：

```javascript
label: {
  // ...
  break label; // 有效
  // ...
}
```

……尽管 99.9% 的情况下 `break` 都被用在循环内，就像在上面那些例子中我们看到的那样。

`continue` 只有在循环内部才可行。

## switch

### case分组

共享同一段代码的几个 `case` 分支可以被分为一组：

比如，如果我们想让 `case 3` 和 `case 5` 执行同样的代码：

```javascript
let a = 3;

switch (a) {
  case 4:
    alert('Right!');
    break;

  case 3: // (*) 下面这两个 case 被分在一组
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;

  default:
    alert('The result is strange. Really.');
}
```

现在 `3` 和 `5` 都显示相同的信息。

## 函数默认参数

定义：函数默认参数也可为函数

```js
function a(num,fun = b()){
  console.log(num,fun)
}
function b(){
  return 2
}
a(1) //打印1,2
```

## Debugger

我们也可以使用 `debugger` 命令来暂停代码，像这样：

```javascript
function hello(name) {
  let phrase = `Hello, ${name}!`;

  debugger;  // <-- 调试器会在这停止

  say(phrase);
}
```

当我们在一个代码编辑器中并且不想切换到浏览器在开发者工具中查找脚本来设置断点时，这真的是非常方便。

## 函数注释

记录函数的参数和用法

有一个专门用于记录函数的语法 [JSDoc](http://en.wikipedia.org/wiki/JSDoc)：用法、参数和返回值。

现代 JSDoc 中使用的一些比较流行的注解标签是：

|      标签      |                       描述                       |
| :------------: | :----------------------------------------------: |
|   `@author`    |                    开发商名称                    |
| `@constructor` |               将函数标记为构造函数               |
| `@deprecated`  |                将方法标记为已弃用                |
|  `@exception`  |                 同义词 `@throws`                 |
|   `@exports`   |               标识由模块导出的成员               |
|    `@param`    | 记录方法参数；可以在花括号之间添加数据类型指示符 |
|   `@private`   |                 表示成员是私有的                 |
|   `@returns`   |                    记录返回值                    |
|   `@return`    |                同义词 `@returns`                 |
|     `@see`     |              记录与另一个对象的关联              |
|    `@todo`     |               记录丢失/打开的东西                |
|    `@this`     |    指定关键字`this`在函数中引用的对象的类型。    |
|   `@throws`    |                记录方法抛出的异常                |
|   `@version`   |                  提供库的版本号                  |

```js
/**
 * 返回 x 的 n 次幂的值。
 *
 * @param {number} x为number类型, 表示要改变的值。
 * @param {number} n幂数为number类型，表说必须是一个自然数。
 * @return {number} 返回值是 x 的 n 次幂的值。
 */
function pow(x, n) {
  ...
}
```

## 双括号函数

意想不到的是: 函数调用是可以**函数(值1)(值2)**调用函数，但第一个括号必须返回一个函数

例如：

```js
function sum(a) {
  return function(b) {
    return a + b; // 从外部词法环境获得 "a"
  };
}

alert( sum(1)(2) ); // 3
alert( sum(5)(-1) ); // 4
```

## 字符串

### str.charAt

定义：和str[pos]类似,获取某个字符

区别：

```js
let str = `Hello`;

alert( str[1000] ); // undefined
alert( str.charAt(1000) ); // ''（空字符串）
```

### 遍历字符串

我们也可以使用 `for..of` 遍历字符：

```javascript
for (let char of "Hello") {
  alert(char); // H,e,l,l,o（char 变为 "H"，然后是 "e"，然后是 "l" 等）
}
```

```js
for (let char in "Hello") {
  console.log(char); // 0,1,2,3,4（char 变为 "0"，然后是 "1"，然后是 "2" 等）
}
```

### 字符串元素不可改变

解决办法：只能赋值给新的变量咯~

```js
let str = 'Hi';
str[0] = 'h'; // error
alert( str[0] ); // 无法运行

#解决办法
let str = 'Hi';
str = 'h' + str[1];  // 替换字符串
alert( str ); // hi
```

### 使一个字符变成大小写

```js
alert( 'Interface'[0].toLowerCase() ); // 'i'
alert( 'interface'[0].toUpperCase() ); // 'I'
```

### 查找字符串(indexOf)

定义：不仅可以查找是否存在，也可查找字符位置，还可以设置起始位置查找

```js
let str = 'Widget with id';
#第一个值为目标字符，第二个为起始索引
alert( str.indexOf('id', 2) ) // 从第二个找,12
```

**`str.lastIndexOf(substr, pos)`**

还有一个类似的方法 [str.lastIndexOf(substr, position)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf)，它从字符串的末尾开始搜索到开头。

它会以相反的顺序列出这些事件。

### [按位（bitwise）NOT 技巧](https://zh.javascript.info/string#an-wei-bitwisenot-ji-qiao)

定义：它将数字转换为 32-bit 整数（如果存在小数部分，则删除小数部分），然后对其二进制表示形式中的所有位均取反，

实际上，这意味着一件很简单的事儿：对于 32-bit 整数，`~n` 等于 `-(n+1)`。

例如：

```javascript
alert( ~2 ); // -3，和 -(2+1) 相同
alert( ~1 ); // -2，和 -(1+1) 相同
alert( ~0 ); // -1，和 -(0+1) 相同
alert( ~-1 ); // 0，和 -(-1+1) 相同
```

人们用它来简写 `indexOf` 检查：

```javascript
let str = "Widget";
//也可使用!str.indexOf("Widget")
if (~str.indexOf("Widget")) {
  alert( 'Found it!' ); // 正常运行
}
```

### 截取字符串

**三种：**

| 方法                    | 选择方式……                                            | 负值参数            |
| :---------------------- | :---------------------------------------------------- | :------------------ |
| `slice(start, end)`     | 从 `start` 到 `end`（不含 `end`）                     | 允许                |
| `substring(start, end)` | `start` 与 `end` 之间（包括 `start`，但不包括 `end`） | 负值代表 `0`        |
| `substr(start, length)` | 从 `start` 开始获取长为 `length` 的字符串             | 允许 `start` 为负数 |

### 字符串互转数字

`str.codePointAt(pos)`：返回在 `pos` 位置的字符代码 :

```javascript
// 不同的字母有不同的代码
alert( "z".codePointAt(0) ); // 122
alert( "Z".codePointAt(0) ); // 90
```

`String.fromCodePoint(code)`：通过数字 `code` 创建字符

```javascript
alert( String.fromCodePoint(90) ); // Z
```

### 字符串转数组

#### split

**意想不到**：split('分隔符', **分隔的数组长度**)

```js
var str ="1=3=4=5"
console.log(str.split('='));//输出['1','3']
console.log(str.split('=',3)) //输出['1','3','4']
```

#### Array.from和[...str]

意想不到的是：这样也可以字符转数组

```js
#1
let str = '123';
// 将 str 拆分为字符数组
let chars = Array.from(str); //[1,2,3]

#2
let str = '123';
// 将 str 拆分为字符数组
let chars = [...str]; //[1,2,3]
```



## 数组

### 数组截肢

定义：通过控制数length属性，来截肢数组，本人称他为截肢

```js
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // 截断到只剩 2 个元素
alert( arr ); // [1, 2]

arr.length = 5; // 又把 length 加回来
alert( arr[3] ); // undefined：被截断的那些数值并没有回来
```

所以，清空数组最简单的方法就是：`arr.length = 0;`。

### new Array()

`new Array(数字)` 创建的数组的所有元素都是 `undefined`。

```js
let arr = new Array(2); // 会创建一个 [2] 的数组吗？

alert( arr[0] ); // undefined！没有元素。

alert( arr.length ); // length 2
```

### 数组转字符串

定义：数组转字符串，会返回以逗号隔开的元素列表, 注：`alert`会把任何东西转字符串

```js
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true

alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
#上面的步骤就和下面一样
alert( "" + 1 ); // "1"
alert( "1" + 1 ); // "11"
alert( "1,2" + 1 ); // "1,21"
```

### 数组查找

- `arr.indexOf(item, from)` 从索引 `from` 开始搜索 `item`，如果找到则返回索引，否则返回 `-1`。
- `arr.lastIndexOf(item, from)` —— 和上面相同，只是从右向左搜索。
- `arr.includes(item, from)` —— 从索引 `from` 开始搜索 `item`，如果找到则返回 `true`（译注：如果没找到，则返回 `false`）。

### arr.sort()原理

```js
let arr = [1, 3, 2];
function compareNumeric(a, b) {
  if (a > b) return 1; //返回1则 a在b后
  if (a == b) return 0; //返回0  a和b位置不动
  if (a < b) return -1; //返回-1  a在b前
  #以上判断可简写为
  return a - b //从小到大 反之大到小
}

arr.sort(compareNumeric);
console.log(arr); //[1,2,3]

```

意想不到的用法：

```js
let john = { name: "John", age: 25 };
let pete = { name: "Pete", age: 30 };
let mary = { name: "Mary", age: 28 };

let arr = [ pete, john, mary ];

function sortByAge(arr) {
  arr.sort((a, b) => a.age - b.age); //以年龄大小排序
}
sortByAge(arr);

// 排序后的数组为：[john, mary, pete]
alert(arr[0].name); // John
alert(arr[1].name); // Mary
alert(arr[2].name); // Pete
```

### Array.from

定义：可以将伪数组转为真数组

值得注意的是：它有三个参数：

`Array.from(arr,fun(每个元素),this)`

- `arr:`数组
- `fun:`添加到数组前调用函数，参数为每个元素
- `this:`可以改变数组this指向

```js
// 求每个数的平方
let arr = Array.from(range, num => num * num);

alert(arr); // 1,4,9,16,25
```

### 数组解构

```js
// 我们有一个存放了名字和姓氏的数组
let arr = ["Ilya", "Kantor"]

// 解构赋值
// sets firstName = arr[0]
// and surname = arr[1]
let [firstName, surname] = arr;

alert(firstName); // Ilya
alert(surname);  // Kantor

#如果我们想要一个“默认”值给未赋值的变量，我们可以使用 = 来提供：

// 默认值
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

alert(name);    // Julius（来自数组的值）
alert(surname); // Anonymous（默认值被使用了）

# 默认值也可以是函数
let [name = prompt('name?'), surname = prompt('surname?')] = ["Julius"];

alert(name);    // Julius（来自数组）
alert(surname); // 你输入的值
```

#### 忽略使用逗号的元素

数组中不想要的元素也可以通过添加额外的逗号来把它丢弃：

```javascript
// 不需要第二个元素
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert( title ); // Consul
```

在上面的代码中，数组的第二个元素被跳过了，第三个元素被赋值给了 `title` 变量，数组中剩下的元素也都被跳过了（因为在这没有对应给它们的变量）。

#### 等号右侧可以是任何可迭代对象

……实际上，我们可以将其与任何可迭代对象一起使用，而不仅限于数组：

```javascript
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```

#### 与 .entries() 方法进行循环操作

```js
let user = {
  name: "John",
  age: 30
};

// 循环遍历键—值对
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, then age:30
}
```



## 对象

### delete

我们可以用 `delete` 操作符移除属性：

```javascript
delete user.age;
```

### [计算属性](https://zh.javascript.info/object#ji-suan-shu-xing)

当创建一个对象时，我们可以在对象字面量中使用方括号。这叫做 **计算属性**。

例如：

```javascript
let fruit = 'apple'

let bag = {
  [fruit]: 5, // 属性名是从 fruit 变量中得到的 变为apple:5
};

alert( bag.apple ); // 5 当然，如果 fruit="apple"
```

我们可以在方括号中使用更复杂的表达式：

```javascript
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

### [“in” 操作符](https://zh.javascript.info/object#shu-xing-cun-zai-xing-ce-shi-in-cao-zuo-fu)

`in` 的左边必须是 **属性名**。通常是一个带引号的字符串。

如果我们省略引号，就意味着左边是一个变量，它应该包含要判断的实际属性名。例如：

```javascript
let user = { age: 30 };

let key = "age";
alert( key in user ); // true，属性 "age" 存在
```

### 整数属性

因为这些电话号码是整数，所以它们以升序排列。所以我们看到的是 `1, 41, 44, 49`。

```javascript
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```

### [通过引用来比较](https://zh.javascript.info/object-copy#tong-guo-yin-yong-lai-bi-jiao)

仅当两个对象为同一对象时，两者才相等。

例如，这里 `a` 和 `b` 两个变量都引用同一个对象，所以它们相等：

```javascript
let a = {};
let b = a; // 复制引用

alert( a == b ); // true，都引用同一对象
alert( a === b ); // true
```

而这里两个独立的对象则并不相等，即使它们看起来很像（都为空）：

```javascript
let a = {};
let b = {}; // 两个独立的对象

alert( a == b ); // false
```

### [克隆与合并](https://zh.javascript.info/object-copy#cloning-and-merging-object-assign)

如果被拷贝的属性的属性名已经存在，那么它会被后面覆盖

**法一：Object.assign**

浅克隆：

第一个参数 `dest` 是指目标对象。

```javascript
Object.assign(dest, [src1, src2...]) // dest:{0:{...src1},1:{...src2}}
```

```js
Object.assign(dest, src1,src2) // dest:{...src1,...src2}
```

`dest` 为空对象则返回新的对象

```js
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user); // clone = {name: "John",age: 30}
```

深克隆：例如 [lodash](https://lodash.com/) 库的 [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep)。

**法二：for循环**

```js
let user = {
  name: "John",
  age: 30
};

let clone = {}; // 新的空对象

// 将 user 中所有的属性拷贝到其中
for (let key in user) {
  clone[key] = user[key];
}

// 现在 clone 是带有相同内容的完全独立的对象
clone.name = "Pete"; // 改变了其中的数据

alert( user.name ); // 原来的对象中的 name 属性依然是 John
```

**法三：展开运算符**

```js
let user = {
name: "John",
age: 30
};

let clone = { ...obj };
```

### 原始值转换

定义：对象类型因无法被其他类型准确的进行转换，也无法和其他类型进行准确比较，所以Javascript通过**三种办法**，判断当对象类型被转换为`string、number、default`(其他类型)类型时，根据类型检测返回的`hint`，返回的相应类型的值

注：**不会判断boolean值**：`Boolean(obj)`永远为`true`

**法一：[Symbol.toPrimitive](https://zh.javascript.info/object-toprimitive#symboltoprimitive)**

```js
let user = {
  name: "John",
  money: 1000,
	//类型检测，判断当前user类型,根据hint值，输出指定内容
  [Symbol.toPrimitive](hint) {
    console.log(hint);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// 转换演示：
alert(user); // 对象类型：返回对象 user
alert(+user); // 数字类型：返回数值 1000
alert(user + 500); // 其他类型: 返回数值 1500
```

**法二：**[toString/valueOf](https://zh.javascript.info/object-toprimitive#tostringvalueof)

```js
let user = {
  name: "John",
  money: 1000,

  // 对于 hint="string"
  toString() {
    return `{name: "${this.name}"}`;
  },

  // 对于 hint="number" 或 "default"
  valueOf() {
    return this.money;
  }

};

alert(user); // 对象类型：返回对象 user
alert(+user); // 数字类型：返回数值 1000
alert(user + 500); // 其他类型: 返回数值 1500
```

**法三：**如果没有 `Symbol.toPrimitive` 和 `valueOf`，则`toString` 将处理所有原始转换。

```js
let user = {
  name: "John",
	//toString处理所有类型
  toString() {
    return 2;
  }
};

console.log(user); // 对象类型：返回对象 user
console.log(+user) // 数字类型：返回 数字2
console.log(String(user))//字符类型：返回 字符2
console.log(user + 500); // 其他类型: 返回数字 502
```

### 对象包装器(了解)

定义：包装原始类型，使得原始类型可以临时存储多个数据，当这些数据被调用完毕时，会立即销毁对象

原始类型：在 JavaScript 中有 7 种原始类型：`string`，`number`，`bigint`，`boolean`，`symbol`，`null` 和 `undefined`

```js
let str = "Hello";
str.toUpperCase()
console.log( str ); // Hello

#上面实际操作,当str调用方法时
//将str字符类型包装成一个对象
str = {
  value:'Hello'
  toUpperCase:()=>{}
}
//toUpperCase方法执行完毕时，对象包装器会立即删除
str.toUpperCase()
str = 'Hello'
//包装器被删除，返回的仍是原始值
console.log(str)
```

总结: 实际上我们调用原始类型的方法，就是对象包装器临时创建的对象，该对象存储了一些方法

### 可迭代对象

详情：https://zh.javascript.info/iterable

### Object.keys，values，entries

- [Object.keys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) —— 返回一个包含该对象所有的键的数组。
- [Object.values(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/values) —— 返回一个包含该对象所有的值的数组。
- [Object.entries(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) —— 返回一个包含该对象所有 [key, value] 键值对的数组.

**[Object.keys/values/entries](http://object.keys/values/entries) 会忽略 symbol 属性**

就像 `for..in` 循环一样，这些方法会忽略使用 `Symbol(...)` 作为键的属性。

 [Object.getOwnPropertySymbols(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols)，它会返回一个只包含 Symbol 类型的键的数组。

 [Reflect.ownKeys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys)，它会返回 **所有** 键。

### 对象解构

默认值可以是任意表达式甚至可以是函数调用

```js
let options = {...};
let {width: w = 100, height: h = 200, title} = options;
let {width = prompt("width?"), title = prompt("title?")} = options;
```

也可以只取其中的某一些属性，然后`rest`把“剩余的”赋值到其他地方

```js
let {title, ...rest} = options; //rest不需要在对象声明就可使用的
```

**嵌套解构**

```js
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true
};
let {
  size: { // 把 size 赋值到这里
    width,
    height
  },
  items: [item1, item2], // 把 items 赋值到这里
  title = "Menu" // 在对象中不存在（使用默认值）
} = options;
```

**图解：**

![image-20220127143536502](C:\Users\16274\AppData\Roaming\Typora\typora-user-images\image-20220127143536502.png)

## 构造器和操作符 "new"

### [构造函数](https://zh.javascript.info/constructor-new#gou-zao-han-shu)

定义：任何函数（除了箭头函数，它没有自己的 `this`）都可以用作构造器。即可以通过 `new` 来运行，它会执行上面的算法。“首字母大写”是一个共同的约定，以明确表示一个函数将被使用 `new` 来运行

注：如果没有参数，我们可以省略 `new` 后的括号

```js
let user = new User; // <-- 没有参数
// 等同于
let user = new User();
```

构造函数在技术上是常规函数。不过有两个约定：

1. 它们的命名以大写字母开头。
2. 它们只能由 `"new"` 操作符来执行。

```javascript
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("Jack");

alert(user.name); // Jack
alert(user.isAdmin); // false
```

当一个函数被使用 `new` 操作符执行时，它按照以下步骤：

换句话说，`new User(...)` 做的就是类似的事情：

```javascript
#四个步骤
function User(name) {
  //1. this = {};（隐式创建）
	//2. this.__proto__ = User.prototype;
  //3. 添加属性到 this
  this.name = name;
  this.isAdmin = false;

  //4. return this;（隐式返回）
}
```

**new function() { … }**

如果我们有许多行用于创建单个复杂对象的代码，我们可以将它们封装在一个立即调用的构造函数中，像这样：

```javascript
// 创建一个函数并立即使用 new 调用它
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // ……用于用户创建的其他代码
  // 也许是复杂的逻辑和语句
  // 局部变量等
};
```

这个构造函数不能被再次调用，因为它不保存在任何地方，只是被创建和调用。因此，这个技巧旨在封装构建单个对象的代码，而无需将来重用。

### [构造器模式测试：new.target](https://zh.javascript.info/constructor-new#gou-zao-qi-mo-shi-ce-shi-newtarget)

在一个函数内部，我们可以使用 `new.target` 属性来检查它是否被使用 `new` 进行调用了。

对于常规调用，它为 `undefined`，对于使用 `new` 的调用，则等于该函数：

```javascript
function User() {
  alert(new.target);
}

// 不带 "new"：
User(); // undefined

// 带 "new"：
new User(); // function User { ... }
```

### [构造器的 return](https://zh.javascript.info/constructor-new#gou-zao-qi-de-return)

通常，构造器没有 `return` 语句。

但是，如果这有一个 `return` 语句，那么规则就简单了：

- 如果 `return` 返回的是一个对象，则返回这个对象，而不是 `this`。
- 如果 `return` 返回的是一个原始类型，则忽略。

```javascript
function BigUser() {

  this.name = "John";

  return { name: "Godzilla" };  // <-- 返回这个对象
}

alert( new BigUser().name );  // Godzilla，得到了那个对象
```

这里有一个 `return` 为空的例子（或者我们可以在它之后放置一个原始类型，没有什么影响）：

```javascript
function SmallUser() {

  this.name = "John";

  return; // <-- 返回 this
}

alert( new SmallUser().name );  // John
```

## 垃圾回收算法

### [内部算法](https://zh.javascript.info/garbage-collection#nei-bu-suan-fa)

**找到垃圾**

垃圾回收的基本算法被称为 “mark-and-sweep”。

定期执行以下“垃圾回收”步骤：

- 垃圾收集器找到所有的根，并“标记”（记住）它们。
- 然后它遍历并“标记”来自它们的所有引用。
- 然后它遍历标记的对象并标记 **它们的** 引用。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象。
- ……如此操作，直到所有可达的（从根部）引用都被访问到。
- 没有被标记的对象都会被删除。

详情请点击[内部算法](https://zh.javascript.info/garbage-collection#nei-bu-suan-fa)结合图片查看，当然，**不是下面这张图片**，下面这张图是对整个回收机制的总结

![缩略图](https://uploads.disquscdn.com/images/29b10afdc3306b3b094312d2afeabbcc405d9942d5b0c605a030a567e7905a20.png?w=800&h=325)

## 数字类型方法

### Math

**常用方法**

| 方法                                | 描述                                                         |
| :---------------------------------- | :----------------------------------------------------------- |
| `ceil(x)`                           | 对x进行上舍入。                                              |
| `floor(x)`                          | 对 x 进行下舍入。                                            |
| `max(x,y,z,...,n)`                  | 返回 x,y,z,...,n 中的最高值。                                |
| `min(x,y,z,...,n)`                  | 返回 x,y,z,...,n中的最低值。                                 |
| `pow(x,y)`                          | 返回 x 的 y 次幂。                                           |
| `sqrt(x)`                           | 返回根号 x 值                                                |
| `Math.random() * (max - min) + min` | 返回 min ~ (max-min) 之间的随机数。<br />radom()默认 0~1     |
| `round(x)`                          | 四舍五入。                                                   |
| `abs(x)`                            | 获取x绝对值                                                  |
| `trunc(x)`                          | 将 x 的小数部分去掉，只保留整数部分。                        |
| `sign(x)`                           | x : 正数返回 `1` , 0返回 `0` , -0返回 `-0` , 负数返回 `-1`<br />非数字字符和空返回`NaN` |
| `Math.imul(x,y)`                    | 返回x * y的乘法结果.                                         |

### toFixed()

定义：保留小数点位数

toFixed()会舍四进五，类似于 `Math.round`

```js
let num1 = 12.34;
alert( num1.toFixed(1) ); // "12.3"

let num2 = 12.36;
alert( num2.toFixed(1) ); // "12.4"
```

注意 `toFixed` 的结果是一个字符串。如果小数部分比所需要的短，则在结尾添加零

```js
let num = 12.34;
alert( num.toFixed(5) ); // "12.34000"，在结尾添加了 0，以达到小数点后五位
#将其转换为数字：+num.toFixed(5)
```

### isFinite()

`isFinite(value)` 将其参数转换为数字，如果是常规数字，则返回 `true`，而不是 `NaN/Infinity/-Infinity`：

```javascript
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false，因为是一个特殊的值：NaN
alert( isFinite(Infinity) ); // false，因为是一个特殊的值：Infinity
```

### parseInt和parseFloat

它们可以从字符串中“读取”数字，直到无法读取为止。如果发生 error，则返回收集到的数字。函数 `parseInt` 返回一个整数，而 `parseFloat` 返回一个浮点数

```js
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12，只有整数部分被返回了
alert( parseFloat('12.3.4') ); // 12.3，在第二个点出停止了读取
alert( parseFloat('a123')) // NaN 未找到第一个数字
```

### Map

详情查看[Map方法](https://cloud.tencent.com/developer/chapter/13610)，这里主要说几个不常用的

#### new Map()

众所周知的是：map存入的key和值，都是以**数组形式**储存

定义：`new Map`的同时在括号里定义**二维数组**，则相当于一次性使用了多个`map.set()`

```js
let map1 = new Map([['x',1],['y',2],['z',3]])
let map2 = new Map()
map.set('x',1).set('y',2).set('z',3)

console.log(map) //{'x' => 1, 'y' => 2, 'z' => 3} 
console.log(map.keys()) // {'x', 'y', 'z'}
console.log(map.values()) // {1, 2, 3}
//实际上还是数组
for(let key of map1){
  consoel.log(key) // ['x',1] ['y',2] ['z',3]
}
for(let key of map2){
  consoel.log(key) // ['x',1] ['y',2] ['z',3] 一样
}
```

#### Object.entries

定义：将对象转化为二维数组

```js
let obj = {
  x:1,
  y:2,
  z:3
}
let arr = Object.entries(obj)
console.log(arr) //[ ['x', 1],['y', 2],['z', 3] ]
```

#### Object.fromEntries

定义：将二维数组转对象

```js
let arr = [
  ['banana', 1],
  ['orange', 2],
  ['meat', 4]
]
let obj = Object.fromEntries(arr)
console.log(obj) // { banana: 1, orange: 2, meat: 4 }
```

#### entries()

作用：为所有数组添加一个**迭代器**，可通过`next().value`的方式访问迭代值(数组)

注：`recipeMap[Symbol.iterator]()`和`recipeMap.entries()`具有相同的作用

```js
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',50]
]);
let newMap = recipeMap.entries() // 可替换为recipeMap[Symbol.iterator]()
console.log(newMap.next().value) //['cucumber', 500]
console.log(newMap.next().value) //['tomatoes', 350]
console.log(newMap.next().value) //['onion',50]
```

#### map.forEach()

实际上：map拥有自己的forEach()

格式:`forEach(value,key,map)=>{}`

```js
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);
// 对每个键值对 (key, value) 运行 forEach 函数
recipeMap.forEach( (value, key, map) => {
  alert(`${key}: ${value}`); // cucumber: 500 以此类推
});
```

### Set

详情查看[Set方法](https://cloud.tencent.com/developer/section/1192061)

众所周知的是：Set和Map方法大同小异，只是有些地方略有不同

#### set.forEach()

格式：`forEach((value, valueAgain, set)`

有趣的是：forEach第一个参数可第二个参数是一样的，但这是为了与 `Map` 兼容

```js
et set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// visits，一些访客来访好几次
set.add(john);
set.add(pete);
set.add(mary);

set.forEach((value, valueAg) => {
  console.log(value)
  /* 
  每个对象打印了2次
  {name: 'John'}
  {name: 'John'}
  {name: 'Pete'}
  {name: 'Pete'}
  {name: 'Mary'}
  {name: 'Mary'}
  */
});
```

### WeakMap和WeakSet

与**Map/Set不同点**：

- `WeakMap` 的key必须是对象
- `WeakMap`的key所引用的对象都是弱引用,只要对象的其他引用被删除，垃圾回收机制就会释放该对象占用的内存，从而避免内存泄漏,而`map`不是，即使引用删除，内存也不会释放

```js
# Map
let john = { name: "John" };
let map = new Map();
map.set(john, "...");
john = null; // 覆盖引用
// john 被存储在了 map 中，
// 我们可以使用 map.keys() 来获取它

# WeakMap
let john = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(john, "...");
john = null; // 覆盖引用
// john 被从内存中删除了！
// consoel.log(weakMap)值依然存在，可能内存被删除了吧，但我不知道诶...
```

注意：**WeakMap/WeakSet无法获取key**

详情查看[WeakMap各种方法](https://cloud.tencent.com/developer/chapter/13627) 和 [WeakSet各种方法](https://cloud.tencent.com/developer/section/1192265)

### Date(日期)

时间戳：传入的整数参数代表的是自 1970-01-01 00:00:00 以来经过的**毫秒数**，该整数被称为 **时间戳**

### JSON

#### JSON.stringify

格式：**JSON.stringify(值, 函数或数组,缩进字符)**

JSON 支持以下数据类型：

- Objects `{ ... }`，Arrays `[ ... ]`，原始类型：strings，numbers，boolean： `true/false`，null。

一些特定于 JavaScript 的对象属性会被 `JSON.stringify` 跳过。

```js
let user = {
  sayHi() { // 被忽略:对象方法
    alert("Hello");
  },
  [Symbol("id")]: 123, // 被忽略：symbol属性
  something: undefined // 被忽略：undefined属性
};

alert( JSON.stringify(user) ); // {}（空对象）
```

值得注意的是：如果两对象循环引用，则JSON.stringify会报错

```js
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: ["john", "ann"]
};

meetup.place = room;       // meetup 引用了 room
room.occupiedBy = meetup; // room 引用了 meetup

JSON.stringify(meetup); // Error: Converting circular structure to JSON
```

##### replacer

定义：JSON.stringify的第二个参数: 可以自定义选择需要的值，和自定义改变值

```js
let mySelf = {
  myName: "张三",
  age: 18,
  friend:[{name: "John"}, {name: "Alice"}],
  nickName:'zs'
};
#数组格式
//例如 张三不喜欢外号(nickName)zs,那我们就不添加
 #结果是，缺少nickName属性，同时friend:[{},{}]，因为stringify数组没有name属性
console.log(JSON.stringify(mySelf,['myNname','age','friend']))

#函数格式
//为解决上述问题，采用函数形式，遍历每个key，然后返回key值，必须有返回值
#需要注意的是(return value)之上的代码都处于 循环体中
console.log(JSON.stringify(mySelf,(key,value)=>{
  console.log(1)//打印好几遍
  if(key === 'nickName') return #如果key为nickName 则不添加
  return value //返回所有最终结果，只打印一遍
}))
```

##### space

定义：定义字符串化后缩进字符，对所有可字符串化数据**都有效**

```js
let user = {
  name: "John",
  age: 25,
  roles: {
    isAdmin: false,
    isEditor: true
  }
};
console.log(JSON.stringify(user, null, 2)); //缩进2个
console.log(JSON.stringify(user, null, 4)); //缩进4个
```

##### toJSON

定义：对象中可以内建一个toJSON()方法，其作用：当对象被转化时调用该方法

```js
let room = {
  number: 23,
  toJSON() {
    return this.number; //返回23
  }
};
let meetup = {
  title: "Conference",
  room
};
console.log( JSON.stringify(room) ); // 23
console.log( JSON.stringify(meetup) );// {"title":"Conference","room":23}
```

值得注意的是：new Date()**自带JSON属性**，返回的是new Date好的数据

```js
let meetup = {
  date: new Date(Date.UTC(2022, 1, 27)),
};
//是{"date":"2022-02-27T00:00:00.000Z"}
//而不是{"date": "new Date(Date.UTC(2022, 1, 27)")}
console.log(JSON.stringify(meetup))
```

#### JSON.prase

##### **reviver**

定义：JSON.prase第二个参数,是一个函数，用于获取数据前设置数据的

格式：JSON.parse(str, [reviver])

```js
let schedule = `{
  "meetups": [
    {"title":"Conference","date":"2017-11-30T12:00:00.000Z"},
    {"title":"Birthday","date":"2017-04-18T12:00:00.000Z"}
  ]
}`;

schedule = JSON.parse(schedule, function(key, value) {
  if (key == 'date') return new Date(value); //遍历所有叫date的key,并为其包装一个Date
  return value;
});
console.log( schedule.meetups[1].date.getDate() )
```

## [词法环境](https://zh.javascript.info/closure#ci-fa-huan-jing)

详情点击[词法环境](https://zh.javascript.info/closure#ci-fa-huan-jing)

> 词法环境必须掌握的概念!

1. 每个运行的[函数、代码块{}、整个脚本]()都有一个 **词法环境**对象

2. 词法环境对象由**两部分组成**：

- **环境记录**：**一个**存储所有局部变量和参数作为其属性的**对象**

- **外部词法环境**：存储外部词法环境，也可以看成对象

3. 创建全局词法环境和声明变量的过程：

   - 当脚本开始运行时，全局词法环境预先填充了所有声明的**全局变量**

     **全局词法环境仅仅存储变量，变量声明并未开始**。几乎就像变量不存在一样

   - let声明变量出现，未赋值，值为`undefined`

   - 最后赋予值

4. 需要注意的是：**函数声明的初始化会被立即完成**，也就是说创建函数的同时，就被声明

   - **得出结论**：函数声明比变量声明要更**早**

5. 函数在运行调用时，内部自动创建一个新的**词法环境**以存储这个调用的局部变量和参数

6. 当代码要访问一个变量时 —— [首先会搜索内部词法环境，然后搜索外部环境，然后搜索更外部的环境]()，以此类推，**直到全局词法环境**，所以，非严格模式下，为了向下兼容，给未定义的变量赋值会创建一个全局变量

7. 所有函数都有名为 `[[Environment]]` 的隐藏属性，该属性保存了对创建该函数的词法环境的引用

8. 当变量被修改时,**会在变量所在的词法环境中更新变量**

9. 两个变量通过同一个函数创建的变量函数，它们都有独立的外部词法环境

[词法环境概念代码:]()

```js
#每个运行的函数、代码块{}、整个脚本，都有一个 词法环境对象
全局词法环境:{
  [[Environment]]:局部词法环境,
  环境记录:{
    全局变量,//并未声明
    全局函数，//已声明
  },
  外部词法环境:{
    null  #全局词法无外部词法环境
  }
}
let 全局变量 = 值
function 全局函数(){
  [[Environment]]:局部词法环境,
  局部词法环境:{
    环境记录:{
      局部变量,
      局部参数
    },
    外部词法环境引用:{
      函数本身,
      外部代码
    }
  }
}
```

## 垃圾收集

如果有一个嵌套的函数在函数结束后仍可达(占有内存)，则它将具有引用词法环境的 `[[Environment]]` 属性

在下面这个例子中，即使在函数执行完成后，词法环境仍然可达。因此，此嵌套函数仍然有效。

例如：

```javascript
function f() {
  let value = 123;

  return function() {
    alert(value);
  }
}

let g = f(); //占有内存,同时 g.[[Environment]] 存储了对相应 f() 调用的词法环境的引用
#正如我们所看到的，理论上当函数可达时，它外部的所有变量也都将存在。

#但在实际中，JavaScript 引擎会试图优化它。它们会分析变量的使用情况，如果从代码中可以明显看出有未使用的外部变量，那么就会将其删除。
```