# JS 的执行过程

接下来我们要讲解 ESM 的模块导入，为了方便理解 ESM 的模块导入，这里需要补充一个知识点 —— **JavaScript 的执行过程**。

JavaScript 执行过程分为两个阶段:

- 编译阶段
- 执行阶段

## 编译阶段

在编译阶段 JS 引擎主要做了三件事：

- 词法分析
- 语法分析
- 字节码生成

这里不详情讲这三件事的具体细节，感兴趣的读者可以阅读 [the-super-tiny-compiler](https://github.com/jamiebuilds/the-super-tiny-compiler) 这个仓库，它通过几百行的代码实现了一个微形编译器，并详细讲了这三个过程的具体细节。

## 执行阶段

在执行阶段，会分情况创建各种类型的执行上下文，例如：**全局执行上下文** (只有一个)、**函数执行上下文**。而执行上下文的创建分为两个阶段：

- 创建阶段
- 执行阶段

在创建阶段会做如下事情：

- 绑定 this
- 为函数和变量分配内存空间
- 初始化相关变量为 undefined

我们日常提到的 变量提升 和 函数提升 就是在 **创建阶段** 做的，所以下面的写法并不会报错：

```js
console.log(msg);
add(1,2)

var msg = 'hello'
functionadd(a,b){
  return a + b;
}
```

因为在执行之前的创建阶段，已经分配好了 `msg` 和 `add` 的内存空间。
