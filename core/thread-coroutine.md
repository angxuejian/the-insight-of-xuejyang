# 单进程下：JS vs Python（线程 & 协程）

| 概念           | JS                  | Python                         | 说明                          |
| -------------- | ------------------- | ------------------------------ | ----------------------------- |
| 主线程         | Browser Main Thread | Main Thread                    | 默认执行代码的线程            |
| UI阻塞/API阻塞 | 死循环卡UI          | 同步阻塞卡API                  | 本质都是阻塞当前线程          |
| 协程语法       | `async/await`       | `async/await`                  | 两边思想几乎一致              |
| 协程对象       | Promise             | Coroutine                      | await 前不会完成              |
| 启动协程       | `asyncFunc()`       | `await coro` / `create_task()` | Python 不会自动执行 coroutine |
| 事件循环       | Event Loop          | asyncio Event Loop             | 负责协程调度                  |
| IO等待         | `await fetch()`     | `await httpx.get()`            | await期间不会阻塞线程         |
| 后台协程任务   | 不 await 的 async   | `asyncio.create_task()`        | fire-and-forget               |
| 真线程         | `Worker`            | `threading.Thread`             | 真正OS线程                    |
| 开线程目的     | 避免UI卡顿          | 隔离阻塞IO                     | 使用场景不同                  |
| 协程切换       | await时切换         | await时切换                    | 主动让出执行权                |
| 线程切换       | OS调度              | OS调度                         | 抢占式切换                    |
| 阻塞sleep      | 无真正同步sleep     | `time.sleep()`                 | 会卡线程                      |
| 非阻塞sleep    | `await delay()`     | `await asyncio.sleep()`        | 挂起协程                      |
| 同步HTTP       | `XMLHttpRequest`    | `requests.get()`               | 阻塞线程                      |
| 异步HTTP       | `fetch`             | `httpx.AsyncClient`            | async IO                      |
| 协程适用场景   | IO并发              | IO并发                         | 最适合网络等待                |
| 线程适用场景   | CPU计算/UI隔离      | 同步阻塞库                     | Python线程常用于兼容同步库    |
| CPU密集        | Worker              | Process                        | Python后面通常走多进程        |
| 单线程并发核心 | Promise/EventLoop   | asyncio/EventLoop              | 本质很像                      |
