# JavaScript in 1s

```js
// **动态类型**
    var i;
    typeof i == 'undefined' // true
    i = 32; // 现在 typeof i == 'number' 了
    i = true; // 'boolean'

// **变量作用域的问题**
// 作用域的边界惟以函数边界划分；
// 下面这两个函数是相同的，JavaScript 总是将所有的变量定义提到所在作用域的开头
    function foo() {
        var x;
        x = 2;
    }
    function foo2() {
        x = 2;
        var x;
    } 

// **let**
    // 这样是很confuse的
    console.log('Val is:', val);
    // ...
    for(var i = 0; i < 10; i++) {
        var val = "different string";
    }

    //这样引发Syntax errir
    console.log('Val is:', val);
    // ...
    for(var i = 0; i < 10; i++) {
        let val = "different string";
    }

// 数据类型 number
    MAX_INT = 2^53 - 1
    1/0 == Infinity
    Math.sqrt(-1) == NaN
    0.1 + 0.2 == 0.3 // false

// 数据类型 string
    let foo = 'This'
    foo.length // 4

    foo = foo + ' is'
    foo.toUpperCase() // This is

// 数据类型 boolean
    false //: 0, NaN, "", undefined, null
    true //: all objects, non-empty strings, non-zero/NaN numbers, functions

// 数据类型 undefined and null
    null == undefined
    null !== undefined

// 头等函数
    let aFuncVar = function(x) {
                        console.log("Func called with", x);
                        return x+1;
                    }
    myFunc(aFuncVar);
    function myFunc(routine) {
        console.log(routine.toString());
        // function(x) {
        //     console.log("Func called with", x);
        //     return x+1;
        // }
        console.log(routine(10));
        // Func called with 10
        // 11
    }

// 字典/Object
    let bar = {name: "Alice", "": "empty", "---": "dash"}
    bar.name;
    bar["name"];
    bar["---"];

    bar.new = "JS"; // 新增键值对
    delete bar.name; // 删除键值对
    Object.keys(bar) == ["", "---", "new"];

// 列表/Arrays
    let anArr = [1, 2, 3];
    typeof anArr == 'object';
    anArr[5] = 'FooBar'; // 这也是合法的 [1,2,3,,,'FooBar']
    anArr.length == 6;
    anArr.name = 'Foo' // 这也是合法的

// Dates
    let date = new Date();
    typeof date == 'object';
    date.valueOf() == 1452359316314;
    date.toISOString() == '2016-01-09T17:08:36.314Z';
    date.toLocaleString() == '1/9/2016, 9:08:36 AM';

// 正则表达式
    let re = /ab+c/;
    let re2 = new RegExp("ab+c");
    let re3 = /ab+c/i;
    re3.test(str); // 忽略大小写
    re.search(str); // 返回匹配子串首个字符的index
    let str = "This has 'quoted' words like 'this'";
    let re = /'[^']*'/g;
    str.match(re); // Returns ["'quoted'", "'this'"]
    str.replace(re, 'XXX');

// try | catch | throw | finally
```

最后：和html互动
- 外联形式
    ```html
    <script type="text/javascript" src="code.js"></script>
    ```
- 以及行内形式
    ```html
    <script type="text/javascript">
    //<![CDATA[
    Javascript goes here...
    //]]>
    </script>
    ```