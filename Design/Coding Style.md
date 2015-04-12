>##Coding Style
Coding style is notoriously contentious because much of it is arbitrary. It's important to follow a style that is comfortable for you and your team. That being said, there are some conventions that can be used to make your life developing with Node easier.


##代码风格
代码应该遵守什么样的风格很难界定，因为大部分的规定都是片面的。遵守一个能让你自己和你的团队感到舒服的代码风格很重要。而按很多人总结的，有一些规范能帮你在开发node应用时更轻松。


>###Name your functions
Consider naming all functions, even small closures you wouldn't think merit a name. While V8 will try its best to identify by script name and function location the source of an error, it can be difficult to differentiate functions at a glance that way. The last thing you want to do when debugging is to waste time fixing the wrong function.

###为你的函数起名
尝试为所有函数命名，即使是小的你不认为值得命名的闭包函数。然而V8引擎会尽最大努力使用脚本名和函数来制定错误的位置。如果这样的话，未命名的函数将很难第一眼区分不同的函数。而最后你所做的只是不断浪费时间在调试错误的函数。

>###Avoid closures
Similarly, consider moving function definitions outside of other functions. This changes your thinking from closure-based to stack-based. This small switch in logic can help eliminate many unintended memory leaks that closures can bring with them.

###避免闭包
同样的，考虑把函数的定义从其他函数内部移出来。这会改变你的思考方式从闭包式的到堆栈式的。这种逻辑上小的改变可以帮助你排除很多由闭包引起的无意识的内存泄露问题。

>###More and smaller functions
The V8 JIT is a powerful engine and can optimize a lot of patterns, but the smaller and more concise you are with your functions the more likely the JIT will be able to inline those functions. On the upside, if your function is small (no more than a 100 or so lines of code for instance) it's likely to increase the readability and understandability of your codebase, which should decrease the amount of effort spent trying to maintain your application.

###使用更小的函数
V8运行时是一个很强大的引擎，它可以优化很多的模式，但更小更简洁的函数能让V8运行时更好的内联函数。好的一点是，如果你的函数很小（代码或者实例代码行数不到100），它更能提高代码的可读性和可理解性，从而减少很多维护应用的工作。

>###Check style programmatically
Use a consistent style, and have a checking tool that enforces it. We use jsstyle, which is a somewhat unusual style for JavaScript, but at least the tool enforces it. Errors from the style checker are just like syntax errors or unit test failures: the build is considered broken and must be fixed immediately.

###检查编程风格
使用一致的编程风格，并且使用代码审查工具来进一步保持这种风格。我们使用**jsstyle**，一种针对Javascript不同寻常的风格，但是至少这个工具能保证维持这种风格。来自代码风格检查工具的错误提示就像语法错误或单元测试错误一样：构建是被认为是失败的并且需要马上修复。
