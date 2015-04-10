>##Control Flow
>Since JavaScript has the concept of functions as first class objects, and closures, it's easy to define the callback right where it is needed. This is convenient when prototyping your solution, as it allows you to consolidate the logic right where it's needed. However it can quickly lead to unwieldy sets of embedded functions, sometimes referred to as the christmas tree.

##流程控制

因为JavaScript有函数作为类对象已经闭包的概念，所以它很容易在需要的地方定义callback。这在你定义解决方案的原型十分有利，它允许你在正确的地方整合你的逻辑。
而且它可以像圣诞树一样将复杂的一系列方法整合起来。

>Consider that you want to read a series of files in succession, and perform a common task on the results of those tasks:

比如你想要连续地读取一系列文件，然后在这些任务中执行以下公用任务：

```
fs.readFile('firstFile', 'utf8', function firstCb(err, firstFile) {
  doSomething(firstFile);
  fs.readFile('secondFile', 'utf8', function secondCb(err, secondFile) {
    doSomething(secondFile);
    fs.readFile('thirdFile', 'utf8', function thirdCb(err, thirdFile) {
      doSomething(thirdFile);
    });
  });
});
```

>This doesn't appear too bad, but there are several downsides to the pattern:

这看起来不是很糟糕，但在设计模式上还是有一些不好的地方：

* If the logic around any of these pieces gets too complex, it can be difficult to understand the flow and order of operations.

* There's no error handling being done here, and by the time we're in the third level we've shadowed the first operation's error twice.

* The result from reading the first file will stay active in the eyes of the GC until the third operation completes. Closure memory leaks are very common in JavaScript applications, and often the most difficult to diagnose and detect.

* 如果这部分逻辑太过复杂，对于理解这段流程和操作的顺序都变得异常困难。
* 这里面没有任何的错误处理，当我们执行第三层调用时，我们已经将第一层的错误跟踪两次了。
* 在垃圾收集器只有在第三个操作完成时才会收集第一个文件读取的结果。闭包引起的内存泄露是JavaScript应用中常见的问题，而且通常难以诊断和检测。


>If you need to do a series of asynchronous operations on a set of input, it's good to find a control flow library that simplifies the process for you. We use vasync because it also makes it easy to inspect a pipeline from a debugger.

如果你像在一些输入程序中坐一些异步操作，找到一个好的流程控制库会简化你的操作。我们使用[vasync](https://npmjs.org/package/vasync)，因为他在使用debugger调试管道时十分方便。

>###vasync
>vasync is a control flow library, inspired by the patterns found in the async module. However vasync is designed specifically to enable a consumer to have visibility and observability into their progress for a given task. Such information is crucial when trying to determine how far along a task was before an error occurred.

>###vasync
>[vasync](https://npmjs.org/package/vasync)是一个流程控制库，它的设计灵感来自于[async](https://npmjs.org/package/async)模块。然而vasync被设计使得事件监控者对他们程序的运行的进度有足够的可见性和可观察性。这些信息对判断一个任务在什么时候出错十分重要。