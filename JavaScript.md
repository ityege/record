# 集合

JavaScript中没有list和map,但是有array和对象;

JavaScript的array是可以动态扩容的，相当于list;

JavaScript的对象就相当于map。

# 遍历

~~~js
// for in 遍历是对象的key
const obj = { a: 1, b: 2, c: 3 };
console.log("=========================1");
for (const key in obj) {
    console.log("key:", key, "value:", obj[key]);
}
console.log("=========================2");
//for of 遍历的对象需要实现Symbol.iterator()
// 如下代码错误
// for (const item of obj) {
//     console.log("item:", item);
// }
console.log("=========================3");
for (const key of Object.keys(obj)) {
    console.log("key:", key, "value:", obj[key]);
}
console.log("=========================4");
for (const value of Object.values(obj)) {
    console.log("value:", value);
}
console.log("=========================5");
for (const [key, value] of Object.entries(obj)) {
    console.log("key:", key, "value:", value);
}
console.log("=========================6");
Object.entries(obj).forEach(([key, value]) => {
    console.log("key:", key, "value:", value);
});
~~~

# 导包

在Node.js中，import 和 require 是两种用于导入模块（即引入其他JavaScript文件或库）的机制。它们之间有几个关键的不同点，主要源于它们分别属于ECMAScript模块（ESM）和CommonJS模块系统。 

1. 语法差异
  require（CommonJS）:
  const module = require('module-name');
  或者对于本地文件：
  const myModule = require('./myModule');
  import（ECMAScript模块，简称ESM）:
  import module from 'module-name';
  或者导入特定的导出：
  import { export1, export2 } from 'module-name';
  对于本地文件，路径可以是相对或绝对的，但通常使用相对路径：
  import myModule from './myModule.js';

2. 动态导入require 不支持动态导入（即运行时决定要导入哪个模块）。虽然可以通过一些技巧实现类似的功能，但这不是其原生支持的特性。import()（作为import的语法糖，用于动态导入）：
  import('module-name').then(module => {  // 使用 module.default 或 module.namedExport }).catch(err => {  // 处理错误 });

  这允许你在需要时异步地加载模块。

3. 导入时的行为require 是同步的（尽管在内部，Node.js可能会异步地处理模块加载，但这对调用者来说是隐藏的）。如果模块尚未被加载，require 会阻塞后续代码的执行，直到模块被加载和解析。import 是异步的（对于静态导入，这主要影响模块的加载顺序，因为顶层await允许你在模块顶层等待异步操作完成）。然而，对于动态导入（import()），它明确是异步的，并返回一个Promise。

4. 导出机制CommonJS 使用 module.exports 或 exports 对象来导出模块。ECMAScript模块 使用 export 关键字来导出模块。可以导出单个值、多个值或整个模块。

5. 兼容性require 是Node.js自诞生以来就支持的特性，因此它在所有版本的Node.js中都是可用的。import/export 是在较新的Node.js版本中通过引入对ECMAScript模块的支持而添加的。为了使用它们，你可能需要在package.json中设置"type": "module"，或者将文件扩展名更改为.mjs。

6. 缓存require 会缓存模块，这意味着如果多次调用require来加载同一个模块，它将返回相同的模块实例。import 同样会缓存模块，但行为上与require相似，因为两者都遵循Node.js的模块缓存机制。结论选择import还是require主要取决于你的项目需求、Node.js版本以及你希望遵循的模块系统（ESM或CommonJS）。随着Node.js对ESM的支持越来越完善，越来越多的项目开始迁移到ESM，但require在现有项目中仍然非常普遍。
