###Dependency Management 依赖管理

>It's important to consider your dependency tree when preparing to deploy your Node application.  

当准备部署Node应用时，很重要的一件事就是考虑你的依赖树结构。  
>NPM is a fast-paced and growing community.  

NPM是一个快节奏、成长型的社区。  

>Module authors are constantly improving their modules and publishing new versions, and their dependent modules are being updated just as quickly.  

模块的作者不断的改进模块功能、发布新的版本，同时它们所依赖的的模块也在迅速的更新。  

>This moving target can complicate your deployment if module versions and behaviors change subtlely between development and deployment, or even from one deploy to deploy in a scaled environment.    

如果模块的版本和功能在开发和部署间有微妙的变化，或者甚至在一个扩展了的环境中部署，这种变化会令部署变得更复杂.  

>While it's possible for you to cache your node_modules directory for reuse during deployment, it may not always be ideal.  

虽然你可以通过缓存node_modules文件夹在部署时重用，但并不总是name理想。    
>You may develop in a different environment from your deployment.  

你的开发环境可能与部署环境不同。

>If you are in a heterogenous environment any modules that depend on a binary dependency will likely break since those modules are platform-specific.  

如果处于不同运行环境中，任何有二进制依赖的模块都有可能出现异常，因为这些模块是基于特定平台的。  

>Also, depending on the size and kind of deployment it may not be feasible to store the various different combinations of modules required for your environments.   

另外，依据大小和部署类型，存储各种不同模块的组合也许并不可行。  


>To handle these scenarios during deployment, use npm shrinkwrap.  

要处理部署中这些问题可以使用命令： npm shrinkwrap.  
>Shrinkwrap makes sure to walk the dependency tree and, at each level, record the module, its version, the module's dependencies and their versions.  

Shrinkwrap命令会确保遍历依赖树，并且记录各层级的模块、版本、依赖模块以及依赖模块的版本。  
>The results are then written to npm-shrinkwrap.json which can safely be checked into your source control.  

结果会被写入到 npm-shrinkwrap.json文件中，它可以安全的加入到你的源码控制中。
>When you deploy your application with this file in the same directory as yourpackage.json, npm will then go and fetch the exact version requirements that were available at the time you created the shrinkwrap file.    

使用npm-shrinkwrap.json文件的部署和使用同目录的package.json部署方式一样，部署后npm将会精确获取所需的版本，这些都是在生产shrinkwrap文件时产生的。  


>Read More about Dependency Management  
想要了解更多应用依赖管理知识，请戳我!戳我!  
