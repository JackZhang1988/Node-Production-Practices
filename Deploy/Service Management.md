### Service Management服务管理

`Once your application is deployed on your server you will need a way to run it and to make sure it stays running.`
一旦你的应用部署到服务器，你会需要一种方式来运行应用服务，并且确保服务会一直运行。
`Enter the Service Management Facility: a framework for supervising your application.`
输入Service Management Facility: 一个监控你程序的框架。
`SMF is designed to ensure that your application is started only after other services that it depends on, and that if your application stops running it is immediately restarted.`
SMF被设计用来确保启动你的应用前先开启依赖服务，并且如果你的应用停止运行会立即重启。

`SMF is feature-rich, including safeguards against your application failing too quickly due to configuration problems or other failures that require operator intervention to fix.`
SMF功能丰富，拥有应用防护措施，能够预防程序因为配置问题或者需要运维人员介入的故障引起的的快速失败。
`Every SMF service has a log file that captures console.log and console.error output from your application, as well as the times of service failures and restarts.`
每个SMF服务都有一个log文件，它获取了你程序中console.log和console.error的输出，以及你的服务失败和重启次数。
`You can easily query the status of your service with a simple command-line tool, including a list of process IDs for your running node processes without needing to mess around with pid files.`
你可以用命令行工具便捷的查询服务状态，包括你正在运行node进程的进程ID列表 ，不需要直接处理pid文件。


`Services are defined and configured with a straightforward XML format; an example for use with your Node application can be found in this repository.`
服务使用了xml文件格式来定义和配置参数，一个Node应用的参考用例可以在这个工程中找到。
`There is also a simple, JSON-based SMF configuration tool called smfgen which will work with many Node applications, without the need to write or edit any XML.`
工程中还有一个基于JSON的SMF配置工具smfgen,它可以在许多Node 应用中使用，不需要直接去编辑修改XML。


`After you've modified the template to match your running user and the filesystem paths to point to where you've deployed your application, import the service into SMF: svccfg import nodeapp-manifest.xml.`
为适配当前用户、指向已部署应用的系统路径需要先修改模板配置，然后引入服务到SMF： svccfg import nodeapp-manifest.xml
`Once your manifest has been successfully imported, you can perform various actions:`
一旦你的manifest文件被成功引入，你可以进行一下操作：

   * Enable your application now, and at next reboot, with: svcadm enable nodeapp
     开启应用服务，在下次重启时使用命令：svcadm enable nodeapp
   * Disable your application with: svcadm disable nodeapp
     关闭应用服务使用命令： svcadm disable nodeapp
   * Query the current status of your application with: svcs nodeapp
     查询当前应用服务的状态，使用命令：svcs nodeapp
   * Find the SMF log file for your service with: svcs -L nodeapp
     查询你应用服务的SMF日志文件，使用命令： svcs -L nodeapp
   * List the process IDs of your running node processes: svcs -p nodded
     列出你当前运行的node进程的进程ID，使用命令： svcs -p nodded

`Read More about Service Management`
想要了解更多应用服务管理知识，请戳我!戳我!