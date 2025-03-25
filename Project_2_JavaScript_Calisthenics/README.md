# CS142 Project 2: JavaScript Calisthenics

## Setup

虽然这个项目需要在浏览器中运行代码，但您需要在系统上安装 Node.js 来运行代码质量检查器。如果您尚未安装 Node.js 和 npm 包管理器，请现在按照[安装说明](https://web.stanford.edu/class/cs142/install.html)进行安装。

安装好 Node.js 后，创建一个名为 `project2` 的目录，并将[此 zip 文件](https://web.stanford.edu/class/cs142/downloads/project2.zip)的文件内容提取到该目录中。该 zip 文件包含 `cs142-test-project2.html` 和 `cs142-test-project2.js` 文件，它们作为本项目中编写代码的测试框架。

您可以在 `project2` 目录下运行以下命令来获取代码质量工具（也称为“linter”）[ESLint](https://eslint.org/)：

```
npm install eslint
```

这会将 ESLint 获取到 `node_modules` 子目录中。您可以通过运行以下命令在 `project2` 目录中的所有 JavaScript 文件上运行 ESLint：

```
npm run lint
```

您提交的代码应在每个 JavaScript 文件中以 `"use strict";` 开头，并且使用上述命令运行 ESLint 不应输出任何错误或警告。任何错误或警告都将用于扣除风格分。

要运行该作业，您有两种选择：

1. **通过浏览器**：在浏览器中打开文件 `cs142-test-project2.html` 。网页将加载您编写的 JavaScript 代码并运行一些测试。

2. **通过 Node.js** ：您也可以使用以下命令在没有浏览器的情况下运行测试
    ```
    npm test
    ```

我们建议使用浏览器进行开发，因为调试环境要好得多。但是，我们将使用 Node.js 进行评分。

**注意：**这些测试并不涵盖所有边缘情况。它们旨在帮助您指导，并让您知道何时具备基本功能。处理以下规格中未在提供的测试文件中明确测试的所有内容，这是您的责任。

在这个项目中，我们要求您编写或修改一些 JavaScript 函数。这个作业中的问题具有实际性质，您开发的功能将在完成后续课程项目时非常有用。鉴于 JavaScript 库可以解决或帮助解决几乎所有分配给您的 JavaScript 任务，您很可能只需几行代码调用库例程即可解决这些问题。由于项目的目标是学习 JavaScript，**我们禁止您在解决方案中使用任何 JavaScript 库**。JavaScript 内置的函数，如数组和日期对象，是可以接受的。

## Problem 1: Generate a Multi Filter Function (10 points)
> 问题 1：生成多过滤函数（10 分）

在您的 project2 目录下，创建一个名为 `cs142-make-multi-filter.js` 的新文件。您的多过滤函数的代码将放在这个文件中。

声明一个名为 `cs142MakeMultiFilter` 的全局函数，该函数接受一个数组（ `originalArray` ）作为参数，并返回一个可以用来过滤数组元素的函数。返回的函数（ `arrayFilterer` ）内部处理一个 `currentArray`。最初， `currentArray` 设置为与 `originalArray` 相同。 `arrayFilterer` 函数接受两个函数作为参数。它们是：

1. `filterCriteria` - 一个接受数组元素作为参数并返回布尔值的函数。
    这个函数会在 `currentArray` 的每个元素上调用，并且 `currentArray` 会根据 `filterCriteria` 函数的结果进行更新。如果 `filterCriteria` 函数对一个元素返回 `false` ，则该元素应从 `currentArray` 中移除。否则，它将被保留在 `currentArray` 中。如果 `filterCriteria` 不是一个函数，则返回的函数（ `arrayFilterer` ）应立即返回 `currentArray` 的值，不执行任何过滤。
2. `callback` - 当过滤完成时将被调用的函数。 `callback` 接收 `currentArray` 的值作为参数。在 `callback` 函数内部访问 `this` 应引用 `originalArray` 的值。如果 `callback` 不是一个函数，则应忽略它。 `callback` 没有返回值。
该 `arrayFilterer` 函数应返回自身，除非未指定 `filterCriteria` 参数，此时应返回 `currentArray` 。必须能够同时运行多个 `arrayFilterer` 函数。
以下代码展示了如何使用您在本问题中定义的函数：

```js
// Invoking cs142MakeMultiFilter() with originalArray = [1, 2, 3] returns a
// function, saved in the variable arrayFilterer1, that can be used to
// repeatedly filter the input array
var arrayFilterer1 = cs142MakeMultiFilter([1, 2, 3]);

// Call arrayFilterer1 (with a callback function) to filter out all the numbers
// not equal to 2.
arrayFilterer1(function (elem) {
  return elem !== 2; // check if element is not equal to 2
}, function (currentArray) {
  // 'this' within the callback function should refer to originalArray which is [1, 2, 3]
  console.log(this); // prints [1, 2, 3]
  console.log(currentArray); // prints [1, 3]
});

// Call arrayFilterer1 (without a callback function) to filter out all the
// elements not equal to 3.
arrayFilterer1(function (elem) {
  return elem !== 3; // check if element is not equal to 3
});

// Calling arrayFilterer1 with no filterCriteria should return the currentArray.
var currentArray = arrayFilterer1();
console.log("currentArray", currentArray); // prints [1] since we filtered out 2 and 3

// Since arrayFilterer returns itself, calls can be chained
function filterTwos(elem) { return elem !== 2; }
function filterThrees(elem) { return elem !== 3; }
var arrayFilterer2 = cs142MakeMultiFilter([1, 2, 3]);
var currentArray2 = arrayFilterer2(filterTwos)(filterThrees)();
console.log("currentArray2", currentArray2); // prints [1] since we filtered out 2 and 3

// Multiple active filters at the same time
var arrayFilterer3 = cs142MakeMultiFilter([1, 2, 3]);
var arrayFilterer4 = cs142MakeMultiFilter([4, 5, 6]);
console.log(arrayFilterer3(filterTwos)()); // prints [1, 3]
console.log(arrayFilterer4(filterThrees)()); // prints [4, 5, 6]
```

## Problem 2: Template Processor (5 points)
> 问题 2：模板处理器（5 分）

在您的 project2 目录下，创建一个名为 `cs142-template-processor.js` 的新文件。您的模板处理器代码将放在这个文件中。

创建一个模板处理器类（ `Cs142TemplateProcessor` ），该类通过一个字符串参数（ `template` ）进行构造，并具有一个方法（ `fillIn` ）。当使用一个对象（ `dictionary`）的参数调用时， `fillIn` 将返回一个填充了字典对象中值的字符串。 `Cs142TemplateProcessor` 应使用标准的 JavaScript 构造函数和原型结构编写。

`fillIn` 方法返回替换了任何形式为 `{{property}}` 的文本的 `template` 字符串，该文本与传入函数的对象的 `property` 对应。

如果模板指定了字典对象中未定义的属性，则该属性应替换为空字符串。如果属性位于两个单词之间，您会发现将属性替换为空字符串会导致出现两个连续的空格。例如： `"This {{undefinedProperty}} is cool"` -> `"This  is cool"` 。这是可以的。您不必担心去除额外的空格。

您的系统只需处理格式正确的属性。在以下情况下，其行为可以是未定义的，因为我们不会明确检查它们。

- 嵌套属性 - `{{foo {{bar}}}}` 或 `{{{{bar}}}}` 或 `{{{bar}}}`
- 不平衡的括号 - `{{bar}}}`
- 任何属性字符串中的游离括号 - `da{y` 或 `da}y`

以下代码展示了如何使用您在本问题中定义的函数：

```js
var template = "My favorite month is {{month}} but not the day {{day}} or the year {{year}}";
var dateTemplate = new Cs142TemplateProcessor(template);

var dictionary = {month: "July", day: "1", year: "2016"};
var str = dateTemplate.fillIn(dictionary);

assert(str === "My favorite month is July but not the day 1 or the year 2016");

// Case: property doesn't exist in dictionary
var dictionary2 = {day: "1", year: "2016"};
var str = dateTemplate.fillIn(dictionary2);

assert(str === "My favorite month is  but not the day 1 or the year 2016");
```

## Problem 3: Fix `cs142-test-project2.js` to not pollute the global namespace (5 points)
> 问题 3：修复 `cs142-test-project2.js` 以避免污染全局命名空间（5 分）

我们提供的测试 JavaScript 文件（ `cs142-test-project2.js` ）在全局 JavaScript 命名空间中声明了多个符号。例如，在脚本加载后，符号 `p1Message` 出现在全局命名空间中。另一个 JavaScript 文件随后可以访问并更改 `p1Message` 。将 cs142-test-project2.js 修改为使用标准的 JavaScript 模块模式，通过**匿名函数**隐藏符号以避免污染全局命名空间，同时保持相同的检查功能。

## Style Points (5 points)

这些分数将在您的上述解答 JavaScript 代码整洁、易读且无 ESLint 警告时获得。

## Useful Hint

- 在 JavaScript 中，检查相等/不等式的约定是 `===` 和 `!==` ，而不是 `==` 和 `!=` 。
- 运行 ESLint 时，请确保存在 `.eslintrc.json` （隐藏文件），否则 ESLint 会抛出错误。您可以使用命令 `ls -a` （Windows 命令行中的 `dir /a` ）查看您当前目录下的所有文件，包括隐藏文件。
- 如果 ESLint 输出显示大量样式问题，您可以通过运行 `npm run lint -- --fix` 让 ESLint 为您修复其中许多问题。
- 在移动文件时，请确保使用命令行进行操作。拖放文件通常不会移动隐藏文件，这是学生遗漏 `.eslintrc.json` 文件的一个常见原因，该文件包含在您开始提取的 zip 文件中。
- 要求您的 Problem 1 解决方案支持 `cs142MakeMultiFilter` 的多个同时使用，这意味着您不应该使用全局变量来存储 `currentArray` 状态。
- 在问题 3 中，您只需要处理测试文件创建的符号。同时，您需要将变量 `cs142Project2Results` 保留为全局的（即 window 对象的属性），以便您可以使用 `run-tests-using-node.js` 脚本来继续运行测试。

## Deliverables

请使用 standard class [submission mechanism](https://web.stanford.edu/class/cs142/submit.html) 提交 project2 目录。此目录应包括我们提供的启动文件以及您为问题创建或修改的代码文件，包括 `cs142-make-multi-filter.js` 、 `cs142-template-processor.js` 、 `cs142-test-project2.js` 和 `cs142-test-project2.html` 。请确保您的提交在运行 `npm run lint` 和 `npm test` 时没有错误或警告。