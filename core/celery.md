# Celery

## Install
```bash
pip install celery[redis] flower
```

## Commands

| 命令 | 作用说明 |
|---|---|
|redis://:password@localhost:6379/0 | 连接 redis |
| celery -A app.core.celery.celery worker | 启动 Worker |
| celery -A app.core.celery.celery worker --loglevel=info | 启动 Worker（info 日志） |
| celery -A app.core.celery.celery worker --loglevel=debug | 启动 Worker（debug 日志） |
| celery -A app.core.celery.celery worker -c 4 | 启动 Worker 并设置 4 并发 |
| celery -A app.core.celery.celery worker -n worker1@%h | 给 Worker 起名字 |
| celery -A app.core.celery.celery worker -Q email | 只监听 email 队列 |
| celery -A app.core.celery.celery worker -Q email,ai | 同时监听多个队列 |
| celery -A app.core.celery.celery worker -n email_worker@%h -Q email | email 专属 Worker |
| celery -A app.core.celery.celery worker -n ai_worker@%h -Q ai | ai 专属 Worker |
| celery -A app.core.celery.celery inspect registered | 查看已注册 task |
| celery -A app.core.celery.celery inspect active | 查看正在执行任务 |
| celery -A app.core.celery.celery inspect scheduled | 查看定时任务 |
| celery -A app.core.celery.celery inspect reserved | 查看等待中的任务 |
| celery -A app.core.celery.celery inspect active_queues | 查看 Worker 正在监听的队列 |
| celery -A app.core.celery.celery inspect stats | 查看 Worker 状态信息 |
| celery -A app.core.celery.celery inspect ping | 检查 Worker 是否在线 |
| celery -A app.core.celery.celery status | 查看所有在线 Worker |
| celery -A app.core.celery.celery purge | 清空等待中的任务队列 |
| celery -A app.core.celery.celery beat | 启动定时任务服务 |
| celery -A app.core.celery.celery report | 查看 Celery 环境报告 |
| celery -A app.core.celery.celery flower | 启动 Flower |
| celery -A app.core.celery.celery flower --port=8888 | Flower 指定端口 |
| celery -A app.core.celery.celery flower --broker=redis://:123456@localhost:6379/0 | Flower 指定 Redis |
| pkill -f 'celery worker' | 关闭所有 Worker |
| ps aux \| grep celery | 查看 Celery 进程 |
| kill -9 PID | 强制关闭指定 Worker |
| http://localhost:5555 | Flower 默认地址 |
| redis-cli | 打开 Redis CLI |
| redis-cli -a 密码 | 使用密码连接 Redis |