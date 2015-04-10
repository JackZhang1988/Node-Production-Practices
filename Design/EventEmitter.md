>Node.js is JavaScript, so everything you already know about JavaScript applies to your Node application as well. The patterns you use to write your front-end client code can be used when writing your server-side application logic. Node does not use any JavaScript language extensions or modifications to accomplish its goal of server side JavaScript.

###Node.js使用Javascript语言，所以一切你知道的有关Javascript的都同样应用于Nodejs。你再编写前端代码使用的模式同样试用与编写server端应用逻辑。Node并不适用Javascript语言的扩展或修改版来完成其server端的功能。

>There are, however, patterns used throughout Node and Joyent that are helpful to know and can be useful while designing your application.

因此，了解在Joyent的node应用中使用的设计模式会对你设计应用时很有帮助并且很有用。




>##EventEmitter

>The first pattern to be aware of is the EventEmitter pattern, which allows implementors to emit an event and consumers to subscribe to the events they are interested in. You can think of this as an extension to the pattern of passing a callback to an asynchronous function that the function invokes upon completion. EventEmitters are useful when one callback isn't enough, usually because there's more than one event that might be interesting to the caller.

#事件分发器


第一个要知道的设计模式是[事件分发](https://nodejs.org/api/events.html#events_class_events_eventemitter)模式，它允许功能实现者分发一个事件，而功能消费者可以订阅他们感兴趣的事件。你可以认为这是函数执行完成后就将回调传递给异步函数的设计模式的一个扩展。对当一个回调不能够满足需求时，事件分发模式很有用，因为通常我们的执行函数要订阅多个事件。

>For example, a caller might make a request to "list files" on a remote server. You may want to stream results back as they come, invoking a callback for each one. The EventEmitter pattern lets you emit "file" on each one, and "end" when the whole operation is done.

举例来说，一个执行函数可能要发出一个展示远程server端文件的请求。你可能期望以流的形式传回结果，当每个文件传回时执行一次回调。事件分发模式使你在每次得到一个文件时分发“file”事件，然后再你完成所有操作后分发“end”事件。

>When implementing an EventEmitter, you simply need to emit the event and the arguments associated with that event.

当我们实现一个事件分发器，你仅仅只需要**分发**这个事件，然后把相应参数传递过去就行。

```
var EventEmitter = require('events').EventEmitter;
var util = require('util');

function MyClass() {
  if (!(this instanceof MyClass)) return new MyClass();

  EventEmitter.call(this);

  var self = this;
  setTimeout(function timeoutCb() {
    self.emit('myEvent', 'hello world', 42);
  }, 1000);
}
util.inherits(MyClass, EventEmitter);
```

>The constructor for MyClass creates a timer that will fire in 1 second, when that timer fires it emits the event myEvent with the string 'hello world' and the number 42. To consume that event you need to use the on() method which was added to the prototype of your class when you inherited it from EventEmitter:

MyClass的构造函数创建了一个每秒触发一次的计时器，每次计时器触发时，计时器都会分发**myEvent**事件，并传递参数**'hello world'**和数字**42**。监听这个事件你需要使用**on()**方法，这个方法已经在它继承自**EventEmitter**时添加到它的原型里了。

```
var myObj = new MyClass();
var start = Date.now();
myObj.on('myEvent', function myEventCb(str, num) {
  console.log('myEvent triggered', str, num, Date.now() - start);
});
```
>It's important to note that you subscribe EventEmitter events to be notified of asynchronous events, but the execution of the listeners themselves is synchronous when that event actually happens. So if the myEvent event has 10 listeners subscribed, all 10 listeners will be called sequentially without deferring to the event loop. With that synchronicity in mind it's important for event emitters to defer emission of events so that consumers can subscribe to multiple events in the same turn of the event loop and have confidence that the callback will be fired sometime in the future.

很重要的一点是，你订阅的EventEmitter事件会异步地通知到你，但监听它们的执行函数是在事件触发时同步执行的。所以如果myEvent事件有10个监听者，所有10个监听者都会顺序地调用而不会推迟事件轮询。要意识到同步性对于事件分发器推迟事件的发放以便让功能订阅者在同一次事件轮询中订阅多个事件，同时保证回调函数会在未来准确无误地触发非常重要。

>##verror
verror extends the base Error class, and allows you to define your messages using printf string formatting. The logic for your application is often a composition of asynchronous methods, and when adding error handling you may want to bubble that information up through your system. verror has VError and WError which allow you to accumulate multiple levels of errors through a chain, and either see the combination of errors in the message (as in VError) or have a final message in WError but programmatically be able to access the previous errors in the chain.

git 
>##verror
## ## ## >[verror](https://npmjs.org/package/verror)扩展了Error基类，它允许你以**printf**的形式输出消息。你的应用通常是一些异步方法的组合，并且处理错误时，你可能想将这个错误信息以冒泡的形式传播到你的系统里。**verror**拥有**VError**和**WError**，它们允许你通过链式结构汇集多层错误，并且同样能看到在信息中错误的组合（以**VError**的形式），或者在**WError**中有一个最终的消息，但是能用程序访问在链式结构中之前的错误。

