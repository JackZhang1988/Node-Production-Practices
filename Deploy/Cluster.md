
###Cluster 集群

>`Node comes with a concept of clustering built into the core.`  
Node的核心库中内置了clustering(集群)的概念。  
>`When using the cluster module in your application, your application is free to spin up as many workers as necessary to accommodate the load your application will receive.`  
当你在应用中使用cluster(集群)模块时,你的应用可以根据实际的负载需求来自由的增加节点的数量。  
>`Though generally it is suggested to match the number of workers to the number of threads or logical cores your environment has available to it.`  
不过通常建议集群的节点数与你服务器提供的线程数或逻辑核心数一致。  


>`The logic that encompasses your master process can be as simple or as complex as you want it to be, at the very least it will need to be able to spin up your workers when needed. It is ideal to make sure yourmaster is keeping track if workers exit and if it's necessary to create new workers.`  
你可以尽可能简单或复杂的组织master进程的逻辑,至少当有需要时能够增加集群的节点数。比较理想的情况是确保能跟踪节点的状态，当节点退出及必要时可以创建新的集群节点。  


>`The logic that makes up a worker is dependent on your application, but any socket opened in a worker will be shared among all workers in the pool.`  
集群节点的逻辑构成依赖于你的应用程序，不过一个节点打开的任何一个socket连接会被集群中所有节点共享。  
>`The design is such that you can write your logic once and spin up as many workers without having to worry about the synchronization of sockets on your own.`  
这种设计能够使你写一次逻辑、开启任意多的节点，且不用去担心socket连接间的同步问题。  
>`If a worker close()'s a listening socket, that only indicates to the pool to stop delivering new requests to that worker, not that all workers will cease to receive new requests from that socket.`  
如果一个节点调用close() 方法关闭一个socket的监听，这只会导致集群停止向此节点发送新的请求，而不是所有的节点都停止从这个socket接受新请求。  



