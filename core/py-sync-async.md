# Py sync / async

| 调用关系                | 推荐写法                     | 是否阻塞线程 | 是否等待结果 | 备注         |
| ----------------------- | ---------------------------- | ------------ | ------------ | ------------ |
| 同步 → 同步             | 直接调用                     | ✅ 阻塞      | ✅           | 最基础       |
| -                       |                              |              |              |              |
| 同步 → 异步             | `asyncio.run()`              | ✅ 阻塞      | ✅           | 仅限普通脚本 |
| 同步 → 异步（框架）     | Django: `async_to_sync`      | ✅ 阻塞      | ✅           | 框架封装     |
| -                       |                              |              |              |              |
| 异步 → 异步（顺序）     | `await`                      | ❌ 不阻塞    | ✅           | ⭐最常用     |
| 异步 → 异步（并发）     | `asyncio.gather`             | ❌ 不阻塞    | ✅           | ⭐推荐       |
| 异步 → 异步（后台）     | `create_task`                | ❌ 不阻塞    | ❌           | ⚠️慎用       |
| -                       |                              |              |              |              |
| 异步 → 同步（IO）       | `asyncio.to_thread`          | ❌ 不阻塞    | ✅           | ⭐推荐       |
| 异步 → 同步（框架）     | FastAPI: `run_in_threadpool` | ❌ 不阻塞    | ✅           | 框架封装     |
| 异步 → 同步（快速计算） | 直接调用                     | ❌ 不阻塞    | ✅           | 很快时可用   |

## sync -> sync

```python
import time

def task(name):
    print(f"{name} 开始")
    time.sleep(1)  # 模拟耗时操作
    print(f"{name} 结束")

def main():
    start = time.time()

    task("任务1")
    task("任务2")
    task("任务3")

    print("总耗时:", time.time() - start)

if __name__ == "__main__":
    main()
```

## sync -> async

```python
import asyncio
import time

async def async_task(name):
    print(f"{name} 开始")
    await asyncio.sleep(1)
    print(f"{name} 结束")
    return name

def main():
    start = time.time()

    results = asyncio.run(run_tasks())

    print("结果:", results)
    print("总耗时:", time.time() - start)

async def run_tasks():
    tasks = [
        async_task("任务1"),
        async_task("任务2"),
        async_task("任务3"),
    ]

    # 并发执行所有任务，等待它们完成并收集结果
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    main()
```

## async -> async

```python
import asyncio
import time

async def task(name):
    await asyncio.sleep(1)
    print(f"{name} 结束")

async def main():
    start = time.time()

    # 顺序执行
    # print('开始执行任务...')
    # await task("任务1")
    # await task("任务2")
    # await task("任务3")

    # 并行执行
    # print('开始执行任务...')
    # await asyncio.gather(
    #     task("任务1"),
    #     task("任务2"),
    #     task("任务3")
    # )

    # 后台执行
    # asyncio.create_task(task("任务1"))
    # asyncio.create_task(task("任务2"))
    # asyncio.create_task(task("任务3"))
    # print('开始执行任务...')
    # await asyncio.sleep(2)  # 保证任务有时间执行

    print("总耗时:", time.time() - start)

asyncio.run(main())
```

## async -> sync

```python
import asyncio
import time

def sync_task(name, x: int):
    sum = 1 + x
    print(f"{name} 结果：{sum}")

def sync_task_io(name):
    time.sleep(1)
    print(f"{name} 结束")

async def main():
    start = time.time()

    # 同步函数为IO密集型任务
    # print('开始执行任务...')
    # await asyncio.gather(
    #     asyncio.to_thread(sync_task_io, "任务1"),
    #     asyncio.to_thread(sync_task_io, "任务2"),
    #     asyncio.to_thread(sync_task_io, "任务3"),
    # )

    # # 同步函数为轻量计算
    # sync_task("任务1", 1)
    # sync_task("任务2", 2)
    # sync_task("任务3", 3)

    print("总耗时:", time.time() - start)

asyncio.run(main())
```
