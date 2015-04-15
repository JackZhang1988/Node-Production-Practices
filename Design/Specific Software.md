##Specific Software

##特定的软件


>###restify
Restify is a module for creating and consuming REST endpoints. Designed specifically to increase the observability and debugability of your application, Restify comes with first class Bunyan support as well support for DTrace. With Bunyan and DTrace support, you're gaining the ability to see via the logs or at runtime routes and their latencies over requests.

[Restify](https://npmjs.org/package/restify)是一个构建和使用REST节点的模块。专门针对提高你的应用的可观察性和可调试性而设计，Restify内置支持Bunyan和DTrace。在Bunyan和DTrace的支持下，你可以获得通过log信息或者运行时路由和潜伏的请求查看调试信息的能力。


>###fast
Fast is a lightweight library for efficiently handling JSON messaging across a TCP channel. At its base it was created to enable message-based RPC, where the result for a given command may induce a series of related objects being streamed to the client. Designed with observability in mind, fast also comes with DTrace support, allowing you to quickly identify the performance characteristics of your server and clients.

[Fast](https://npmjs.org/package/fast)是一个高效地通过TCP通道处理JSON信息的轻量级库。在它的基础上可以传输基于远程过程调用协议的信息，这样可以使用指定的命令来将结果以流的形式将一系列相关对象传输给客户端。基于高可观测性的设计，fast同样支持DTrace，它同样允许你鉴定你的服务器和客户端的性能特征。

>###workflow
workflow built on top of restify, enables you to define orchestration among a series of remote services and their APIs. This allows you to decompose a complex series of operations down to a sequence of discreet tasks with a state machine. Workflow is more than a mechanism to allow you to define a sequence of tasks that are run in a specified order, it also enables you to handle failure states, describe timeouts and define retries, as well as identify stuck workflows.

[workflow](https://npmjs.org/package/node-workflow)是在`restify`基础上构建出来的，它可以使你通过一系列的远程服务和它的API定义合理的任务安排。这使得你可以将一系列的复杂操作解耦成一系列的使用状态机的谨慎的任务。Workflow不仅仅是一个允许你按指定顺序定义一系列任务的机制，它同样能让你处理失败的状态，描述超时和定义重连接，它同样能支出堆栈的工作流。