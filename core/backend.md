# Backend

| 模块 | 掌握内容 | 说明 |
|--------|---------|------|
| API 服务 | RESTful API、HTTP协议、状态码、请求/响应、路由设计 | 理解客户端与服务端通信机制，能够设计规范的接口 |
| 数据持久化 | PostgreSQL/MySQL、数据建模、表设计、索引设计 | 数据存储基础，理解关系型数据库设计原则 |
| 数据库操作 | SQLAlchemy ORM、Session管理、CRUD、事务处理 | 实现数据库增删改查和事务控制 |
| 数据库迁移 | Alembic、Migration脚本、版本管理、数据初始化 | 管理数据库结构变更，支持团队协作和生产环境升级 |
| 参数校验/数据模型 | Pydantic、字段校验、序列化/反序列化、Schema设计 | 保证接口输入输出数据合法且规范 |
| 配置管理 | 环境变量、.env、Pydantic Settings、多环境配置 | 开发、测试、生产环境配置隔离 |
| 身份认证 | JWT、Access Token、Refresh Token、密码加密 | 实现用户登录和接口鉴权 |
| 权限控制 | RBAC、角色权限设计、资源授权 | 控制不同用户访问不同资源 |
| 日志系统 | logging、Loguru、日志分级、日志文件管理 | 记录系统运行状态，便于问题排查 |
| 异常处理 | 全局异常捕获、自定义异常、统一响应格式 | 提升系统稳定性和用户体验 |
| 中间件 | 请求日志、中间件机制、跨域(CORS)、限流 | 统一处理请求和响应流程 |
| 异步任务 | Celery、Redis、BackgroundTasks、定时任务 | 处理耗时任务，避免阻塞主线程 |
| 缓存 | Redis、缓存策略、缓存失效、分布式缓存 | 提升系统性能，减少数据库压力 |
| 文件存储 | 本地存储、OSS、MinIO、文件上传下载 | 实现文件管理能力 |
| 容器化部署 | Docker、Docker Compose、镜像构建、容器网络 | 实现环境一致性和快速部署 |
| 反向代理 | Nginx、负载均衡、静态资源代理、HTTPS | 对外提供统一访问入口 |
| 服务部署 | Gunicorn、Uvicorn、多进程部署 | 提高服务并发处理能力 |
| 消息队列 | RabbitMQ、Redis Stream、Kafka（了解） | 系统解耦和异步通信 |
| 测试 | Pytest、单元测试、集成测试、接口测试 | 保证代码质量和功能正确性 |
| 安全 | SQL注入防护、XSS、CSRF、密码加密、HTTPS | 提升系统安全性 |
| 监控运维 | Prometheus、Grafana、健康检查 | 监控服务状态和性能指标 |
| CI/CD | GitHub Actions、GitLab CI、自动部署 | 实现自动测试和持续交付 |

---

| 分类    | 通用概念               | Python            | Java              | Go             | Node.js          |
| ----- | ------------------ | ----------------- | ----------------- | -------------- | ---------------- |
| API服务 | HTTP、REST、路由       | FastAPI           | Spring Boot       | Gin/Fiber      | Express/NestJS   |
| 参数校验  | DTO、Schema         | Pydantic          | Bean Validation   | validator      | class-validator  |
| ORM   | ORM思想              | SQLAlchemy        | JPA/Hibernate     | GORM           | Prisma/TypeORM   |
| SQL   | SQL语法、索引、事务        | PostgreSQL        | PostgreSQL        | PostgreSQL     | PostgreSQL       |
| 数据迁移  | Migration          | Alembic           | Flyway            | golang-migrate | Prisma Migration |
| 认证    | JWT/OAuth2         | PyJWT             | Spring Security   | jwt-go         | jsonwebtoken     |
| 权限    | RBAC、ABAC          | Casbin            | Spring Security   | Casbin         | Casbin           |
| 缓存    | Redis              | redis-py          | Spring Data Redis | go-redis       | ioredis          |
| 异步任务  | MQ、Job             | Celery            | Quartz/RabbitMQ   | Asynq          | BullMQ           |
| 日志    | Structured Logging | Loguru            | Logback           | Zap            | Winston          |
| 配置    | ENV配置              | pydantic-settings | application.yml   | viper          | dotenv           |
| 容器化   | Docker             | Docker            | Docker            | Docker         | Docker           |
| 反向代理  | Nginx              | Nginx             | Nginx             | Nginx          | Nginx            |
| 消息队列  | RabbitMQ/Kafka     | pika/kafka-python | Spring Kafka      | sarama         | kafkajs          |
| 测试    | 单元测试               | pytest            | JUnit             | testing        | Jest             |
| 监控    | Metrics/Tracing    | Prometheus        | Prometheus        | Prometheus     | Prometheus       |
| CI/CD | 自动化部署              | GitHub Actions    | GitHub Actions    | GitHub Actions | GitHub Actions   |



<!-- | 能力模块            | 技术点                     | 作用说明                                              | 前端类比（帮助理解）              |
|---------------------|----------------------------|-------------------------------------------------------|----------------------------------|
| 分层设计            | Controller / Service       | 路由与业务逻辑解耦，结构清晰、易维护                  | Vue 组件 + composable 分层        |
| 依赖注入            | Depends                    | 解耦组件依赖，复用逻辑（鉴权、数据库连接等）          | Vue composable / hooks            |
| 中间件              | Middleware                 | 统一处理请求（日志、鉴权、限流等）                    | axios 拦截器                      |
| 全局异常处理        | Exception Handler          | 统一错误格式，避免接口返回混乱                        | 全局 error handler                |
| 异步并发            | async / await              | 提高并发能力，适合 IO 密集型（API 调用等）            | Promise / async await             |
| 内存缓存            | dict / TTL                 | 减少重复计算，提高性能（模拟 Redis）                  | 前端缓存 / memo / localStorage    |
| 请求限流            | 自定义 limiter             | 防止接口被刷，保护服务                                | 前端防抖 / 节流（throttle）       |
| 接口聚合（BFF）     | 多 service 组合            | 一个接口聚合多个数据源，减少前端请求次数              | 前端数据整合层（如页面级请求）     | -->


<!-- | 场景/问题                     | 是否需要引入 | 技术栈            | 作用说明                         | 什么时候用（判断标准）                         |
|------------------------------|--------------|-------------------|----------------------------------|-----------------------------------------------|
| 基础 API 服务                | ✅ 必须       | FastAPI           | 提供接口 / 路由                  | 只要做后端就需要                               |
| 数据持久化                   | ✅ 必须       | PostgreSQL        | 存储业务数据                     | 有结构化数据（用户、订单等）                   |
| 数据库操作                   | ✅ 必须       | SQLAlchemy        | ORM 操作数据库                   | 不想手写 SQL / 需要模型映射                    |
| 参数校验 / 数据模型          | ✅ 必须       | Pydantic          | 校验请求 & 定义返回结构          | 所有接口都建议用                               |
| 容器化部署                   | ✅ 强烈建议   | Docker            | 统一环境 / 一键部署              | 本地、测试、生产环境不一致时                   |
| 反向代理 / 网关              | ✅ 强烈建议   | Nginx             | 负载均衡 / HTTPS / 静态资源      | 上生产环境基本必备                             |
| 缓存热点数据                 | ⚠️ 按需       | Redis             | 提升性能 / 减少数据库压力        | 查询慢 / 高频访问 / QPS 上来                   |
| 用户登录认证                 | ⚠️ 按需       | JWT / OAuth2      | 用户身份验证                     | 有用户系统 / 登录功能                          |
| 异步任务（耗时操作）         | ⚠️ 按需       | Celery + Redis    | 后台执行任务                     | 发邮件 / AI处理 / 文件处理                     |
| 接口限流                     | ⚠️ 按需       | Redis / 中间件    | 防止接口被刷                     | 公网 API / 防攻击                              |
| 日志记录                     | ⚠️ 建议       | logging           | 记录运行信息                     | 任何项目都建议（排查问题）                     |
| 错误监控                     | ⚠️ 建议       | Sentry            | 捕获异常                         | 线上项目                                      |
| 实时通信                     | ⚠️ 按需       | WebSocket         | 实时数据推送                     | 聊天 / 实时状态更新                           |
| 全文搜索                     | ⚠️ 按需       | Elasticsearch     | 高效搜索                         | 搜索复杂（关键词 / 模糊搜索）                  |
| 消息队列（解耦系统）         | ⚠️ 进阶       | Kafka / RabbitMQ  | 服务解耦 / 高并发处理            | 高并发 / 多服务通信                           |
| AI / 语义搜索                | ⚠️ 按需       | LangChain / FAISS | LLM / 向量检索                   | AI项目（你现在就在用）                         |
| 微服务架构                   | ❌ 初期不要   | 多服务拆分        | 系统拆分                         | 单体撑不住（团队大 / 复杂度高）                | -->


<!-- | 前端概念       | 后端对应            |
| ---------- | --------------- |
| Vue 组件     | API 路由          |
| composable | service         |
| axios 拦截器  | middleware      |
| store      | fake_db / cache |
| props 校验   | Pydantic        |
| router     | FastAPI 路由      | -->
