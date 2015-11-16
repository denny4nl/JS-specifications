# JS-specifications
定义JS的书写规范
* ============================================ *
* 本文档主要目的用于规范在开发过程中对JS的使用 *
* 针对以下几个方面进行强制规定或者建议：       *
* ============================================ *

Reference
 - [原文](https://github.com/airbnb/javascript)
 - [参考1](https://github.com/adamlu/javascript-style-guide)
 - [参考2](https://github.com/fex-team/styleguide/blob/master/javascript.md)

## <a name='TOC'>内容</a>

1. [命名规则](#rules)
1. [文件命名](#file-naming)
1. [注释](#comments)
1. [命名约定](#naming-conventions)
1. [变量](#types)
1. [函数](#functions)
1. [块](#blocks)
1. [分号](#semicolons)
1. [空格](#space)
1. [比较操作](#conditionals)
1. [存取器](#accessors)
1. [构造器](#constructors)
1. [事件](#events)
1. [JQuery](#jquery)
1. [ES6](https://github.com/airbnb/javascript#ecmascript-6-styles)

## <a name='rules'>命名规则</a>
    + 驼峰式大小写（camel case）
        当变量和函数名称由两个或多个单词组成，利用“驼峰式大小写”来表示，可以
        增加变量和函数的可读性。
        小驼峰式命名法(lower camel case): 第一个单词以小写字母开始；第二个单词
        的首字母大写，例如：firstName, lastName
        大驼峰式命名法(upper camel case):每一个单词的首字母都采用大写字母，
        例如：FirstName, LastName, 也被称为Pascal命名法。
    + JQuery文件命名习惯：product-name.plugin-ver.filetype.js 
        例如：jquery-1.4.2.min.js, jquery.plugin-0.1.js
    + 普通的下划线法
    + 匈牙利命名法

## <a name='file-naming'>文件命名</a>
    - 如[命名规则](#file-naming)中提到的JQuery文件命名习惯，使用
    product-name.plugin-ver.filetype.js 这种方式。在项目中开发过程中由于文件
    变化频繁, 在发布成为正式可用版本前，ver处暂时不填写, 调试过程中暂时也不
    压缩js, 所以filetype暂时也为空。目前也暂时不会存在某个产品的plugin。
    直接使用product-name.js方式命名文件。
    - 在我们现有的产品开发过程中，由于list和CRUD（增删改查）比较多，可以使用
    以下方式：xxx-list.js, xxx-crud.js

## <a name='comments'>注释</a>
  - 使用 `/** ... */` 进行多行注释，包括描述，指定类型以及参数值和返回值

    ```javascript
    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - 使用 `//` 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.

    ```javascript
    // good
    // is current tab
    var active = true;

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

  - 如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话
    需要在你的注释前面加上 `FIXME` 或 `TODO` 帮助其他人迅速理解

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
  ```

    **[[⬆]](#TOC)**

## <a name='naming-conventions'>命名约定</a>
  - 避免单个字符名，让你的变量名有描述意义。

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - 当命名对象、函数和实例时使用驼峰命名规则

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    var this-is-my-object = {};
    function c() {};
    var u = new user({
      name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction() {};
    var user = new User({
      name: 'Bob Parr'
    });
    ```

  - 当命名构造函数或类时使用驼峰式大写

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    // good
    function User(options) {
      this.name = options.name;
    }

    var good = new User({
      name: 'yup'
    });
    ```

  - 命名私有属性时前面加个下划线 `_`

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - 当保存对 `this` 的引用时使用 `_this`.

    ```javascript
    // bad
    function() {
      var self = this;
      return function() {
        console.log(self);
      };
    }

    // bad
    function() {
      var that = this;
      return function() {
        console.log(that);
      };
    }

    // good
    function() {
      var _this = this;
      return function() {
        console.log(_this);
      };
    }
    ```

    **[[⬆]](#TOC)**

## <a name='types'>变量</a>
    首字母小写，接着每个单词首字母大写。变量名的第一个单词应当是一个名词
    (而非动词)。不要在变量命名中使用下划线。
    Promise对象 用 动宾短语的进行时 表达。
  - 使用字面值创建对象, 数组

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};

    // bad
    var items = new Array();

    // good
    var items = [];

    // good
    var loadingData = ajax.get('url');
    loadingData.then(callback);
    ```

  - 不要使用保留字 [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) 作为键

    ```javascript
    // bad
    var superman = {
      class: 'superhero',
      default: { clark: 'kent' },
      private: true
    };

    // good
    var superman = {
      klass: 'superhero',
      defaults: { clark: 'kent' },
      hidden: true
    };
    ```
  - 如果你不知道数组的长度，使用push

    ```javascript
    var someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```
  - 当你需要拷贝数组时使用slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length,
        itemsCopy = [],
        i;

    // bad
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

  - 使用slice将类数组的对象转成数组.

    ```javascript
    function trigger() {
      var args = Array.prototype.slice.call(arguments);
      ...
    }
    ```
 - 对字符串使用单引号 `''`

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```
 - 对字符串使用单引号 `''`

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

  - 超过80个字符的字符串应该使用字符串连接换行
  - 注: 如果过度使用，长字符串连接可能会对性能有影响. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
    was thrown because of Batman. \
    When you stop to think about \
    how Batman had anything to do \
    with this, you would get nowhere \
    fast.';


    // good
    var errorMessage = 'This is a super long error that ' +
      'was thrown because of Batman.' +
      'When you stop to think about ' +
      'how Batman had anything to do ' +
      'with this, you would get nowhere ' +
      'fast.';
    ```
    - 编程时使用join而不是字符串连接来构建字符串，特别是IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

    ```javascript
    var items,
        messages,
        length, i;

    messages = [{
        state: 'success',
        message: 'This one worked.'
    },{
        state: 'success',
        message: 'This one worked as well.'
    },{
        state: 'error',
        message: 'This one did not work.'
    }];

    length = messages.length;

    // bad
    function inbox(messages) {
      items = '<ul>';

      for (i = 0; i < length; i++) {
        items += '<li>' + messages[i].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = [];

      for (i = 0; i < length; i++) {
        items[i] = messages[i].message;
      }

      return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
    }
    ```
    **[[⬆]](#TOC)**

## <a name='functions'>函数</a>
    函数命名也应当采用驼峰命名格式。函数名的第一个单词应当是动词(而非名词)，
    最好不使用下划线。
    ```javascript
    function doSomething() {
    }
    ```
  - 函数表达式:

    ```javascript
    // 匿名函数表达式
    var anonymous = function() {
      return true;
    };

    // 有名函数表达式
    var named = function named() {
      return true;
    };

    // 立即调用函数表达式
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```
  - 绝对不要把参数命名为 `arguments`, 这将会逾越函数作用域内传过来的 `arguments` 对象.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```
    **[[⬆]](#TOC)**

## <a name='blocks'>块</a>

  - 给所有多行的块使用大括号

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }
    // bad
    function() { return false; }

    // good
    function() {
      return false;
    }
    ```
    **[[⬆]](#TOC)**

## <a name='semicolons'>分号</a>
    函数定义结束不允许添加分号。

  - 语句结束一定要加分号

    ```javascript
    // bad
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // good
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    // good
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();

    // 如果是函数表达式，分号是不允许省略的。
    var funcName = function () {
    };
    ```
    **[[⬆]](#TOC)**

## <a name='space'>空格</a>
  - 二元运算符两侧必须有一个空格，一元运算符与操作对象之间不允许有空格。
  - 用作代码块起始的左花括号 { 前必须有一个空格。
  - if / else / for / while / function / switch / do / try / catch / finally 
    关键字后，必须有一个空格。
  - 在对象创建时，属性中的 : 之后必须有空格，: 之前不允许有空格。
  - 函数声明、具名函数表达式、函数调用中，函数名和 ( 之间不允许有空格。
  - , 和 ; 前不允许有空格。
  - 在函数调用、函数声明、括号表达式、属性访问、if / for / while / switch 
    / catch 等语句中，() 和 [] 内紧贴括号部分不允许有空格。
  - 行尾不得有多余的空格。

## <a name='conditionals'>比较操作</a>
  在 Equality Expression 中使用类型严格的 ===。
  仅当判断 null 或 undefined 时，允许使用 == null。
  - 适当使用 `===` 和 `!==` 以及 `==` 和 `!=`.
  - 条件表达式的强制类型转换遵循以下规则：

    + **对象** 被计算为 **true**
    + **Undefined** 被计算为 **false**
    + **Null** 被计算为 **false**
    + **布尔值** 被计算为 **布尔的值**
    + **数字** 如果是 **+0, -0, or NaN** 被计算为 **false** , 否则为 **true**
    + **字符串** 如果是空字符串 `''` 则被计算为 **false**, 否则为 **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - 使用快捷方式.

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

## <a name='accessors'>存取器</a>

  - 属性的存取器函数不是必需的
  - 如果你确实有存取器函数的话使用getVal() 和 setVal('hello')

    ```javascript
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - 如果属性是布尔值，使用isVal() 或 hasVal()

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  - 可以创建get()和set()函数，但是要保持一致

    ```javascript
    function Jedi(options) {
      options || (options = {});
      var lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    Jedi.prototype.set = function(key, val) {
      this[key] = val;
    };

    Jedi.prototype.get = function(key) {
      return this[key];
    };
    ```

    **[[⬆]](#TOC)**


## <a name='constructors'>构造器</a>

  - 给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题。

    ```javascript
    function Jedi() {
      console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      fight: function fight() {
        console.log('fighting');
      },

      block: function block() {
        console.log('blocking');
      }
    };

    // good
    Jedi.prototype.fight = function fight() {
      console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      console.log('blocking');
    };
    ```
  **[[⬆]](#TOC)**
## <a name='events'>事件</a>

  - 当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里而不用找出并更新那个事件的事件处理器

    ```js
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId) {
      // do something with listingId
    });
    ```

    更好:

    ```js
    // good
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function(e, data) {
      // do something with data.listingId
    });
    ```

  **[[⬆]](#TOC)**
## <a name='jquery'>jQuery</a>

  - 缓存jQuery查询

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  - 对DOM查询使用级联的 `$('.sidebar ul')` 或 `$('.sidebar ul')`，[jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  - 对有作用域的jQuery对象查询使用 `find`

    ```javascript
    // bad
    $('.sidebar', 'ul').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good (slower)
    $sidebar.find('ul');

    // good (faster)
    $($sidebar[0]).find('ul');
    ```

    **[[⬆]](#TOC)**

