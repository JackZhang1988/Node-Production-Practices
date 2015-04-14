###Deploying New Versions  部署新版本

>`When it comes to deploying new versions of your application, avoid an in-process mechanism for reloading your code.`  

当要为你的程序部署新版本时，需避免使用进程内重新加载代码的机制。  
>`Such techniques are fraught with dangerous edge cases that can lead to memory and state corruption errors that are difficult to debug.`  

这类技术会让应用程序游走在充满危险情况的边缘，导致很难调试的内存和状态的崩溃错误。  
>`Reproducible deployment is critical in production systems, and is best accomplished by starting with a clean slate each time.`  

在生产系统中可再生的部署是至关重要的，并且最好每次能从干净的状态开启完成。  


>`If your application cannot sustain downtime for rolling out a new version of your software, use the cluster module to distribute the new versions to workers.`  

如果你的应用程序要求在更新版本时不能出现停机时间，可以使用cluster(集群)模块来分发新版本到节点。  

>`One possible solution would be for the master process to subscribe to the SIGHUP event.`  
一个可能的解决方案是master进程订阅SIGHUP事件。  
>`When the master receives the event, it should fork new workers that have the new application logic, and inform the existing workers to close their listeners.`  

当这个master进程接收到该事件，它将会fork出含有新程序逻辑的节点，并且通知目前的节点关闭监听。  
>`When the existing workers close their listeners, they simply stop accepting new connections, but allow any current operations run to completion.`  

当现有节点关闭监听服务后，它们将不再接收新的连接，但允许所有当前的操作运行完成。  
>`Once the existing operations have completed the worker is free to exit cleanly.`  

一旦现有的操作执行完成，节点将自由的退出干净。  
