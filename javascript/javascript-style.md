## Javascript 代码风格指南

> 本文档部分内容摘录自百度、airbnb

### 目录

- [命名](#命名)
- [注释](#注释)
- [变量](#变量)
- [对象](#对象)
- [函数](#函数)
- [字符串](#字符串)
- [比较](#比较)
- [控制语句](#控制语句)
- [空白](#空白)
   + [空格](#空格)
   + [空行](#空行)

## 命名

- 命名空间 、变量、函数、参数、方法、属性使用 `Camel` 命名。

- 常量使用全部字母大写，单词间 `_` 分隔的命名法。

- 不使用拼音或拼音简写命名。

  ```javascript
  
  // bad
  // 公积金额度
  var gjjAmout;
  
  // 法人姓名
  var frName;
  
  // 格式化
  function geShiHua() {  }
  
  ```

- 缩略词应全部大写或小写。

  > 名字是用来阅读的，不能让步给计算机算法。
  
  ```javascript
  
  // bad
  import SmsContainer from './containers/SmsContainer';
  
  const HttpRequests = [
    // ...
  ];
  
  // good
  import SMSContainer from './containers/SMSContainer';
  
  const HTTPRequests = [
    // ...
  ];
  
  ```

- 不使用下划线开头或结尾。  

  > 原因：JavaScript对于属性和方法并没有隐私的概念.尽管下划线开头通常意味着'private', 事实上这些属性是完全公开的，是公开API的一部分. 这种风格可能导致开发者错误地认为这不重要或者测试也不必要. 也就是说: 如果你想让其 “private”, 必须使其不可见.

  ```javascript
  
  // bad
  this.__firstName__ = 'Panda';
  this.firstName_ = 'Panda';
  this._firstName = 'Panda';
  
  ```

- 构造函数或类使用 `Pascal` 命名。  

  ```javascript
  
  // bad
  function user(options) {
    this.name = options.name;
  }
  
  const bad = new user({
    name: 'nope'
  });
  
  // good
  class User {
    constructor(options) {
      this.name = options.name;
    }
  }
  
  const good = new User({
    name: 'yup'
  });
  
  ```
  
- 模块文件名应该和默认 `export` 的名字相同。  

- 当默认导出一个函数时使用 `Camel` 风格。  

  ```javascript
  
  function makeStyleGuide() {  }
  
  export default makeStyleGuide;
  
  ```
  
- 当导出构造函数、类、单例、函数库、对象时使用 `Pascal` 风格。

  ```javascript
  
  const AirbnbStyleGuide = {
    es6: {}
  };
  
  export default AirbnbStyleGuide;
  
  ```

- 函数名使用动宾短语。

  ```javascript
  
  // bad
  function productDetail() {  }
  
  // good
  function getProductDetail() {  }
  
  ```
  
- `boolean` 类型的变量使用 `is` 或 `has` 开头。

  ```javascript
  
  var isReady = false;
  
  var hasMoreCommands = false;
  
  ```

- `Promise` 对象用动宾短语的进行时表达。

  ```javascript  
  
  var loadingData = ajax.get('url');
  
  loadingData.then(callback);
  
  ```

### 注释

- 注释缩进与被注释代码保持一致。

  ```javascript
  
  // bad
  // is current tab
  var active = true;
  
  // bad
  // 输出标题
  document.getElementById("myH1").innerHTML="欢迎来到我的主页";
  
  ```

- 所有注释都要以空格开头便于阅读。

  ```javascript
  
  // bad
  //is current tab
  const active = true;
  
  // good
  // is current tab
  const active = true;
  
  // bad
  /**
   *make() returns a new element
   *based on the passed-in tag name
   */
  function make(tag) {
  
    // ...
    
    return element;
  }
  
  // good
  /**
   * make() returns a new element
   * based on the passed-in tag name
   */
  function make(tag) {
  
    // ...
    
    return element;
  }
  
  ```
  
- 单行注释独占一行，如果不是放置在块的第一行则在注释前留一个空行。

  ```javascript
  
  // bad
  const active = true;  // is current tab
  
  // good
  // is current tab
  const active = true;
  
  // bad
  function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this._type || 'no type';
    
    return type;
  }
  
  // good
  function getType() {
    console.log('fetching type...');
    
    // set the default type to 'no type'
    const type = this._type || 'no type';
    
    return type;
  }
  
  // also good
  function getType() {
    // set the default type to 'no type'
    const type = this._type || 'no type';
    
    return type;
  }
  
  ```

- 多行注释使用文档注释`/** ... */`，而避免使用`/* ... */`。

  ```javascript
  
  // bad
  // 函数名
  // 描述
  // 参数
  // 返回值
  function make(tag) {
  
    // ...
    
    return 1;
  }
  
  // bad
  /*
  函数名
  描述
  参数
  返回值
  */
  function make(tag) {
  
    // ...
    
    return 1;
  }

  // good
  /**
   * make() returns a new element
   * based on the passed in tag name
   */
  function make(tag) {
  
    // ...
    
    return element;
  }
  
  ```

- <font color=#1986db size=5>[建议]</font>为了便于代码阅读和自文档化，以下内容必须包含以 `/**...*/` 形式的块注释中。
   + 文件
   + namespace
   + 类
   + 函数或方法
   + 类属性
   + 事件
   + 全局变量
   + 常量
   + AMD模块

### 变量

- 不要重复声明变量。

- 每个 `var` 只声明一个变量。

  ```javascript
  
  // bad
  var a, b, c;
  
  // good
  var a = 1;
  var b = 2;
  var c = 3;
  
  ```

- 在需要的地方变量声明，但位置要合理。

  > 变量声明与使用的距离越远，出现的跨度越大，代码的阅读与维护成本越高。虽然JavaScript的变量是函数作用域，还是应该根据编程中的意图，缩小变量出现的距离空间。
  
  ```javascript
  
  // bad - unnecessary function call
  function checkName(hasName) {
    var name = getName();
    
    if (hasName === 'test') {
      return false;
    }
    
    if (name === 'test') {
      this.setName('');
      return false;
    }
    
    return name;
  }
    
  // good
  function checkName(hasName) {
    if (hasName === 'test') {
      return false;
    }
    
    var name = getName();
    
    if (name === 'test') {
      this.setName('');
      
      return false;
    }
    
    return name;
  }
  
  ```

- 变量不要进行链式赋值。

  > 变量链式赋值会创建隐藏的全局变量。
  
  ```javascript
  
  // bad
  var a = b = c = 1
  
  // good
  var a = 1;
  var b = 2;
  var c = 3;
  
  ```

- 如果要保存对上下文 `this` 的引用，请使用 `self` 来命名。

  ```javascript
  
  // bad
  var _this = this;
  var This = this;
  
  // good
  var self = this;
  
  ```

- 使用浏览器全局变量时加上 `window.` 前缀，`document`、`console`、`navigator`除外。

### 对象

- 创建对象时，不要给属性添加引号，除非属性是非法标识符。

  ```javascript
  
  // bad
  var bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5
  };
  
  // good
  var good = {
    foo: 3,
    bar: 4,
    'data-blah': 5
  };
  
  ```

- 对象属性换行时注意统一代码风格。
  
  ```javascript
  
  // bad
  var bad = {
    foo: 3, bar: 4,
    baz: 5
  }
  
  // good
  var good = {
    foo: 3,
    bar: 4,
    baz: 5
  }
  
  ```

### 函数

- 不要在控制语句的代码块中定义函数。
  
  ```javascript
  
  // bad
  if (flag) {
    function Foo() {  }
  }
  
  while (flag) {
    function Foo() {  }
  }
  
  ```

- 不要改变参数。

  ```javascript
  
  // bad
  function foo(n) {
    n = n * 100;
    return n;
  }
  
  function bar(option) {
    option.key = 1;
  }
  
  // good
  function foo(n) {
    var result = n;
    result = result * 100;
    return result;
  }
  
  function bar(option) {
    var key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
  }
  
  ``` 

- 命名`函数`或`方法`的常用动词。
  
  | A | B |
  | ---- | ---- |
  | get 获取 | set 设置 |
  | add 添加 | remove 移除 |
  | create 创建 | destory 销毁 |
  | start 启动 | stop 停止 |
  | open 打开 | close 关闭 |
  | read 读取 | write 写入 |
  | load 载入 | save 保存 |
  | begin 开始 | end 结束 |
  | backup 添加 | restore 恢复 |
  | import 导入 | export 导出 |
  | split 分割 | merge 合并 |
  | inject 注入 | extract 提取 |

### 字符串

- 字符串使用单引号`'`。

  > 输入单引号方便输入，这对创建HTML字符串非常有好处。

  ```javascript
  
  // bad
  const name = "Capt. Janeway";
  
  // bad - template literals should contain interpolation or newlines
  const name = `Capt. Janeway`;
  
  // good
  const name = 'Capt. Janeway';
  
  ```

### 比较

- 使用`===`而非`==`。

  > 例外：`obj == null`可以用来检查`null || undefined`。  
  
  > 使用`===`可以避免等于判断中隐式的类型转换。

### 控制语句

- 把 `else` 放到和 `if` 块的闭合括号同一行。

  ```javascript
  
  // bad
  if (test) {
    thing1();
    thing2();
  }
  else {
    thing3();
  }

  // good
  if (test) {
    thing1();
    thing2();
  } else {
    thing3();
  }
  
  ```

- `if`条件控制，即使代码只有一行，也不要省略大括号。

  ```javascript
  
  // bad
  if (isTrue) doSomeThing();
  
  // good
  if (isTrue) {
    doSomeThing();
  }
  
  ```

- 一旦你的控制语句 (`if`, `while` 等。) 太长或者超出行宽最大长度，每一个(组)条件要被放到新行。逻辑运算符应该在写在行的开头。
    
  > 原因：行开头有运算符可以使运算符有像链式方法一样的形式。这对于追踪复杂逻辑能够提高可读性。

  ```javascript
  
  // bad
  if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
    thing1();
  }
    
  // bad
  if (foo === 123 &&
    bar === 'abc') {
    thing1();
  }
    
  // bad
  if (foo === 123
    && bar === 'abc') {
    thing1();
  }
    
  // bad
  if (
    foo === 123 &&
    bar === 'abc'
  ) {
    thing1();
  }
    
  // good
  if (
    foo === 123
    && bar === 'abc'
  ) {
    thing1();
  }
  
  // good
  if (
    (foo === 123 || bar === "abc")
    && doesItLookGoodWhenItBecomesThatLong()
    && isThisReallyHappening()
  ) {
    thing1();
  }
  
  // good
  if (foo === 123 && bar === 'abc') {
    thing1();
  }
    
  ```

- 用`switch`做条件控制时，要使用`break` 来将条件分支正常中断。
  
  ```javascript
  
  //bad
  switch (filter) {
    case 1:
      doSomething1();
    case 2:
      doSomething2();
    case 3:
      doSomething3();
  }
  
  //good
  switch (filter) {
    case 1:
      doSomething1();
      break;
    case 2:
      doSomething2();
      break;
    case 3:
      doSomething3();
  }
  
  ```

- 避免使用`Yoda`表示法。

  ```JavaScript
  
  // bad
  if('blue' === theSky) {  }
  
  // good
  if(theSky === 'blue) {  }
  
  ```

### 空白

#### 空格

- 将软tab设置为两个空格。  

  ```javascript
  
  // bad
  function foo() {
  ∙∙∙∙const name;
  }
  
  // bad
  function bar() {
  ∙const name;
  }
  
  // good
  function baz() {
  ∙∙const name;
  }
  
  ```

- 在起始花括号前加一个空格。
  
  ```javascript
  
  // bad
  function test(){
    console.log('test');
  }
  
  // good
  function test() {
    console.log('test');
  }
  
  // bad
  dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog',
  });
  
  // good
  dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog',
  });
  
  ```

- 在控制语句的圆括号前加一个空格 (if，while 等)。 在函数调用和声明中在参数列表和函数名间不要放置空格。

  ```javascript
  
  // bad
  if(isJedi) {
    fight ();
  }
  
  // good
  if (isJedi) {
    fight();
  }
  
  // bad
  function fight () {
    console.log ('Swooosh!');
  }
  
  // good
  function fight() {
    console.log('Swooosh!');
  }
  
  ```

- 二元运算符两边放置空格。

  ```javascript
  
  // bad
  const x=y+5;
  
  // good
  const x = y + 5;
  
  ```
    
- 圆括号中不要添加空格。

  ```javascript
  
  // bad
  function bar( foo ) {
    return foo;
  }
  
  // good
  function bar(foo) {
    return foo;
  }
  
  // bad
  if ( foo ) {
    console.log(foo);
  }
  
  // good
  if (foo) {
    console.log(foo);
  }
  
  ```

- 不要在方括号内添加空格

  ```javascript
  
  // bad
  const foo = [ 1, 2, 3 ];
  console.log(foo[ 0 ]);
  
  // good
  const foo = [1, 2, 3];
  console.log(foo[0]);
  
  ```

- 在花括号中添加空格。

  ```javascript
  
  // bad
  const foo = {a: 1}
  function foo () {return true} 
  
  // good
  const foo = { a: 1 }
  function foo () { return true } 
  
  ```

- 逗号前不要加空格，逗号后要加空格。

  ```javascript
  
  // bad
  var foo = 1,bar = 2
  var arr = [1 , 2]
  var bar = { a: 1,b: 2 }

  // good
  var foo = 1, bar = 2
  var arr = [1, 2]
  var bar = { a: 1, b: 2 }
  
  ```

- 对象字面量属性中的 : 之后必须有空格，: 之前不允许有空格。

  ```javascript
  
  // bad
  var obj = { a : 42 };
  var obj2 = { a:42 };

  // good
  var obj = { a: 42 };
  
  ```

- 行尾不得有多余的空格。
  
  ```javascript
  
  // bad
  var obj = { a: 1 }∙∙
  
  // good
  var obj = { a: 1 }
  
  ```

#### 空行

- 用空行结束文件。
    
- 在代码块结束和下一个声明前留一个空行。
  
  ```javascript
  
  // bad
  if (foo) {
    return bar;
  }
  return baz;

  // good
  if (foo) {
    return bar;
  }

  return baz;

  // bad
  const obj = {
    foo() {},
    bar() {},
  };
  return obj;

  // good
  const obj = {
    foo() {
    },
    
    bar() {
    },
  };
  
  return obj;
  
  // bad
  const arr = [
    function foo() {},
    function bar() {},
  ];
  return arr;

  // good
  const arr = [
    function foo() {},

    function bar() {},
  ];
  
  return arr;
  
  ```

- 清除代码中的冗余空行。

  ```javascript
  
  // bad
  function bar() {
  
    console.log(foo);
  
  }
  
  // also bad
  if (baz) {
  
    console.log(qux);
  } else {
    console.log(foo);
    
  }
  
  // good
  function bar() {
    console.log(foo);
  }
  
  // good
  if (baz) {
    console.log(qux);
  } else {
    console.log(foo);
  }
  
  ```
  
