### Domains  域

>`Domain is a useful module built into the core of Node that allows developers to gracefully handle unexpected errors for asynchronous events.`  

Domain是Node核心库中内置的非常有用的模块，它允许开发者优雅的处理异步事件中意想不到的错误。  
>`That is to say, you can group related asynchronous IO operations together and if one of them errors in an unexpected way, that error won't necessarily disrupt other IO happening in the event queue.`    

这也就意味着，你可以将相关异步IO操作分组在一起，如果其中任一个出现异常报错，该错误不一定会破坏事件列表中其它IO操作。  


>`One of the primary use cases for domains is the scenario where you hit an unexpected error when handling an http request, however there are still other users that have requests being processed by your application.`    

Domain模块主要用例的一个使用场景是： 当你在处理http请求时遇到一个异常的错误，然而你的应用程序还有其它用户的请求正在处理。    
>`If you are in this scenario and have deployed with cluster you should immediately close()the listener in the worker, report the error, and let the other requests finish before exiting gracefully.`    

如果处于这种场景中并且使用了cluster(集群)模式部署，你应该立刻调用close()方法关闭节点中的监听器、上报错误，并且在优雅的退出前关闭其它的请求。  


>`Since the error you encountered was unexpected, it's not entirely clear just what might have happened to the rest of your state.`  

因为你遇到的错误是意想不到的，不完全清楚接下来的状态会受到什么影响。  
>`You could use the error handler to roll back transactions, and try to repair as much as possible, but it's unlikely that you can guarantee that the process is in a state where it's truly safe to continue.`  

你可以使用错误处理程序来回滚事务，尝试尽可能多的去修复，但是你不太可能保证这个过程处于一个可以继续执行的安全状态。  
>`Consider calling process.abort() instead to save a core file for later debugging, and allow the system to restart your process.`  

一种替代方案是可以考虑调用process.abort()方法 ，这能为后期的调试保存核心文件，并且允许系统重启你的进程。  
