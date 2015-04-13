##Linting

##代码分析

Lint tools analyze your code statically (without running it) to identify potential bugs or dangerous patterns, like use of undeclared variables or "case" statements inside a switch without a "break" statement. Good linters can be a little aggressive (e.g., sometimes it's desirable to have a "case" statement without a "break"), but you can override them on a per-line basis. Such overrides should not be used just to silence the linter, but rather because the code as written is much clearer than rewriting it to avoid the warning. The override also clarifies the potentially confusing code for readers.

代码分析工具可以静态分析你的代码（而不需要运行它）来制定代码中潜在的bug或危险的设计模式，比如使用未声明的变量或者在switch中“case”声明内没有使用“break”。好的代码分析工具可能会更激进些（比如，有些情况我们是故意要设计成case语句后没有break的），但是你可以用一行代码重写他们的分析规则。这种重写并不能仅仅为了不让代码分析工具不报错而做，而是因为取消代码警报后我们的代码能变得更整洁。这种重新同样能为读者澄清代码中不太好理解的地方。


If you lint your code, be serious about it. Run lint checks as part of the build, alongside unit tests, and reject code that doesn't pass all checks. (Remember, you can override individual checks as needed, but the point is that doing so makes it clear that the programmer has seen that check and decided the code is correct.)

如果你开始分析你的代码，请认真对待这项工作。把代码分析作为和单元测试一样的构建应用的一部分，而且重新改下那些没有通过审查的代码。（记住，你可以在需要时重写单独的检查方法，但这么做的目的应该是能让程序员更清楚意识到所检查的和所写的代码是正确的。）

Lint is not the same thing as style checking. Style checking is useful too (see above), but linting generally refers to objectively dangerous patterns, rather than arbitrary style choices. (Admittedly, there's a gray area between these, as when considering whether it's okay to use "==" instead of "===" in some cases.)

代码分析和代码风格检查不一样。风格检查同样很有用（可以看之前的文章），但是代码分析通常应用于客观的危险模式，而不是抽象的风格选择。
（无可否认地，在这两者之间还存在模糊的地方，就像考虑在某些情况下是否使用“==”替代“===”一样。）

There are many different linters. Find one that fits your needs. We use javascriptlint because it has a good number of checks and it's configurable both on a by-project basis (each project can specify which checks it wants to enforce) as well as on a by-line basis (so that a programmer can indicate when a check is being explicitly bypassed).

有许多种的代码分析工具。找到一个适合你的工具。我们使用**javascriptlint**，因为它有足够数量的代码检查类型，并且它既可以基于项目（每个项目可以指定哪种检查类型需要加强）同时可以基于单行代码（这样程序员可以指定在什么时候需要显示的忽略审查）配置审查规则。

Also, strongly consider enabling strict mode on your codebase with 'use strict';, as this can help your code fail fast if the JavaScript parser can identify a leaked global or similar bad behavior.

同样，强烈建议你考虑在你的代码中使用'use strict'打开严格模式,因为这样可以让你代码的错误进口抛出来，以便Javascript处理器可以定位一个全局的漏洞或者相似的严重错误。

>译者注：lint 是最著名的C语言工具之一，是由贝尔实验室SteveJohnson于1979在PCC(PortableC Compiler)基础上开发的静态代码分析，一般由UNIX系统提供。与大多数C语言编译器相比，lint可以对程序进行更加广泛的错误分析，是一种更加严密的编译工具。最初，lint这个工具用来扫描C源文件并对源程序中不可移植的代码提出警告。但是现在大多数lint实用程序已经变得更加严密，它不但可以检查出可移植性问题，而且可以检查出那些虽然可移植并且完全合乎语法但却很可能是错误的特性。
