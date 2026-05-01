# Frontend

## 基础

### HTML

| 模块       | 掌握内容                                    | 说明               |
| ---------- | ------------------------------------------- | ------------------ |
| 文档结构   | <!DOCTYPE>、html/head/body、meta、title     | 页面基础结构       |
| 文本标签   | h1~h6、p、span、strong、em、br              | 基础内容展示       |
| 链接媒体   | a、img、video、audio                        | 资源加载与跳转     |
| 列表       | ul / ol / li                                | 常用于菜单、列表   |
| 表格       | table / tr / td / th                        | 数据展示           |
| 表单       | form、input、textarea、select、button       | 前后端数据交互核心 |
| 表单属性   | name、value、placeholder、required          | 表单提交关键       |
| 语义化     | header、nav、main、article、section、footer | 提升结构语义、SEO  |
| 通用属性   | id、class、style、data-\*                   | 所有开发都会用     |
| 可访问性   | alt、label、aria-\*                         | 无障碍与规范化     |
| html5 能力 | video、audio、canvas、表单新类型            | 现代浏览器能力     |
| 性能       | script defer/async、图片懒加载              | 页面加载优化       |

### CSS

| 模块      | 掌握内容                                  | 说明           |
| --------- | ----------------------------------------- | -------------- |
| 基础语法  | 选择器、优先级、继承                      | CSS核心规则    |
| 盒模型    | content/padding/border/margin、box-sizing | 布局基础       |
| display   | block、inline、inline-block、none         | 元素显示方式   |
| Flex 布局 | 主轴/交叉轴、对齐、分布                   | 最常用布局方案 |
| Grid 布局 | 网格系统                                  | 复杂布局       |
| position  | relative/absolute/fixed/sticky            | 精准控制位置   |
| 响应式    | media query                               | 适配移动端     |
| 单位      | px、%、em、rem、vw/vh                     | 布局尺寸体系   |
| 动画      | transition、animation                     | 提升交互体验   |
| 变量      | CSS variables                             | 统一样式管理   |
| 预处理器  | Sass / Less                               | 提高开发效率   |
| 原子化    | Tailwind                                  | 现代开发趋势   |

### JavaScript

| 模块                        | 掌握内容                            | 说明                          |
| --------------------------- | ----------------------------------- | ----------------------------- |
| 基础语法                    | 变量、数据类型、运算符              | 基础                          |
| 作用域                      | 词法作用域（定义时决定）、let/const | `能访问谁`、制变量可见性      |
| this                        | 动态绑定（调用时决定）              | `当前是谁`、确定执行上下文    |
| 闭包                        | 函数 + 作用域绑定                   | `能记住谁`、状态管理（hooks） |
| 原型链                      | prototype、继承机制                 | `还能从谁那拿`、复用 / 继承   |
| 异步                        | Promise、async/await                | 处理异步操作                  |
| [事件循环](./event-loop.md) | event loop、宏任务/微任务           | 异步执行机制                  |
| DOM 操作                    | querySelector、节点操作             | 操控页面                      |
| 事件机制                    | 冒泡、捕获、事件委托                | 事件处理                      |
| ES6+                        | 解构、箭头函数、class、模块化       | 现代JS标准                    |
| 模块化                      | import/export                       | 工程化基础                    |
| 浏览器 API                  | localStorage、fetch                 | 常用能力                      |
| 错误处理                    | try/catch                           | 稳定性保障                    |
| 性能优化                    | 防抖、节流                          | 高频优化手段                  |
| TypeScript                  | 类型系统                            | 类型约束、泛型、接口设计      |

### Browser

| 模块                  | 掌握内容                                        | 说明                 |
| --------------------- | ----------------------------------------------- | -------------------- |
| 渲染机制              | DOM / CSSOM、Render Tree、布局与绘制            | 页面如何从代码变成UI |
| 重排重绘              | reflow / repaint                                | 性能优化关键点       |
| 缓存机制              | 强缓存、协商缓存（HTTP cache）                  | 提升加载性能         |
| 跨域                  | CORS、同源策略                                  | 前后端通信基础       |
| 存储                  | cookie、localStorage、sessionStorage、indexedDB | 本地数据存储         |
| requestAnimationFrame | 动画最佳实践                                    | 替代 setTimeout      |
| Web Worker            | 多线程计算                                      | 提升性能             |
| IntersectionObserver  | 懒加载/可视检测                                 | 替代滚动监听         |
| XSS                   | 注入攻击                                        | 必须防               |
| CSP                   | 内容安全策略                                    | 防攻击手段           |
| Service Worker        | 离线缓存、PWA                                   | 进阶应用             |
| CSRF                  | 跨站请求伪造                                    | 后端协作             |
| iframe 通信           | postMessage                                     | 嵌套页面通信         |

## 框架

### Vue / React 通用技术栈

| 模块            | 掌握内容                | 说明                |
| --------------- | ----------------------- | ------------------- |
| 核心思想        | 状态驱动视图            | UI = state 的映射   |
| 组件化          | 组件拆分、组合、复用    | 前端开发核心模式    |
| 状态管理        | 本地状态、全局状态设计  | 数据流设计能力      |
| 响应式/更新机制 | 状态变化 → 触发视图更新 | Vue自动 / React手动 |
| 生命周期        | 挂载、更新、卸载        | 组件运行过程        |
| 逻辑复用        | hooks / composable      | 抽离业务逻辑        |
| 事件系统        | 事件绑定、事件传递      | 用户交互            |
| 条件渲染        | 条件控制 UI 显示        | 控制视图            |
| 列表渲染        | 列表循环、key           | 性能优化关键        |
| 表单处理        | 输入绑定、校验          | 业务高频            |
| 路由            | 页面切换、嵌套路由      | SPA核心             |
| 全局状态        | store 设计、模块拆分    | 中大型项目          |
| 异步处理        | 请求、loading、错误处理 | 实战能力            |
| 副作用管理      | 数据请求、订阅、DOM操作 | 生命周期延伸        |
| 性能优化        | memo、缓存、懒加载      | 提升体验            |
| 代码拆分        | 动态加载、按需加载      | 减少首屏            |
| SSR             | 服务端渲染              | SEO / 性能          |
| 工程化          | 构建工具、目录设计      | 项目规范            |

### Vue vs React API 映射

| 能力              | Vue 3                | React                   | 本质说明       |
| ----------------- | -------------------- | ----------------------- | -------------- |
| 状态（响应式）    | ref / reactive       | useState                | 状态驱动UI     |
| 派生状态          | computed             | useMemo                 | 基于状态计算   |
| 监听变化          | watch                | useEffect               | 响应数据变化   |
| 生命周期（挂载）  | onMounted            | useEffect(() => {}, []) | 初次执行       |
| 生命周期（更新）  | onUpdated            | useEffect(() => {})     | 更新后执行     |
| 生命周期（卸载）  | onUnmounted          | useEffect return        | 清理副作用     |
| 逻辑复用          | composable           | custom hooks            | 抽离逻辑       |
| 组件通信（父→子） | props                | props                   | 数据传递       |
| 组件通信（子→父） | emit                 | 回调函数                | 事件上抛       |
| 跨组件通信        | provide/inject       | Context                 | 跨层级传值     |
| 双向绑定          | v-model              | value + onChange        | 语法糖 vs 手动 |
| 条件渲染          | v-if / v-show        | && / 三元表达式         | 控制显示       |
| 列表渲染          | v-for                | map                     | 循环渲染       |
| DOM 操作          | ref（DOM）           | useRef                  | 获取DOM        |
| 副作用            | watchEffect          | useEffect               | 自动 vs 手动   |
| 异步组件          | defineAsyncComponent | React.lazy              | 懒加载         |
| 全局状态          | Pinia                | Redux / Zustand         | 状态中心       |
| 路由              | Vue Router           | React Router            | 页面导航       |
| SSR               | Nuxt.js              | Next.js                 | 服务端渲染     |

#### Vue 写法（偏“声明式 + 自动”）

你声明关系，框架帮你追踪依赖；[simple.vue](https://github.com/angxuejian/simple.vue)

```js
const count = ref(0);

watch(count, () => {
  console.log("变化了");
});
```

#### React 写法（偏“函数式 + 手动控制”）

你自己声明什么时候执行

```js
const [count, setCount] = useState(0);

useEffect(() => {
  console.log("变化了");
}, [count]);
```

## 工程化

| 模块         | 掌握内容                                               | 说明                                                                                     |
| ------------ | ------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| 构建工具     | Vite / Webpack                                         | 开发服务器、打包、插件机制；[simple.bundle](https://github.com/angxuejian/simple.bundle) |
| 构建原理     | ESBuild（开发）+ Rollup（生产）、Rolldown（开发+生产） | Vite底层机制                                                                             |
| 模块化       | ESM / CommonJS / UMD                                   | JS模块体系                                                                               |
| 包管理       | pnpm / npm / yarn                                      | 依赖管理、lock机制                                                                       |
| Monorepo     | pnpm workspace                                         | 多包管理                                                                                 |
| 代码规范     | ESLint + Prettier                                      | 代码统一、团队协作                                                                       |
| Git Hooks    | husky + lint-staged                                    | 提交前校验                                                                               |
| 环境变量     | .env / import.meta.env                                 | 多环境配置                                                                               |
| 路径别名     | alias（@/xxx）                                         | 提升可读性                                                                               |
| 静态资源处理 | 图片/字体/压缩/哈希                                    | 构建优化                                                                                 |
| 依赖拆分     | vendor chunk（第三方库拆分）                           | 减少首屏体积、提升缓存利用                                                               |
| Tree Shaking | 删除未使用代码                                         | 减小包体积                                                                               |
| Source Map   | 调试源码映射                                           | 开发调试                                                                                 |
| 构建优化     | 压缩（terser）、gzip、brotli                           | 提升加载速度                                                                             |
| 依赖优化     | 预构建（pre-bundle）                                   | 提升 dev 启动速度                                                                        |
| 插件系统     | Vite 插件机制                                          | 扩展能力                                                                                 |
| 打包分析     | bundle analyzer                                        | 分析包体积                                                                               |
| 多环境构建   | dev / test / prod                                      | 不同环境打包                                                                             |
| CI/CD        | 自动构建、部署                                         | 工程自动化                                                                               |
| 部署         | Nginx / CDN                                            | 静态资源发布                                                                             |


## 网络层

| 模块       | 掌握内容                    | 说明                                        |
| ---------- | --------------------------- | ------------------------------------------- |
| HTTP       | 请求基础                    | RESTful、状态码、请求封装（axios/fetch）    |
| 长连接     | SSE                         | 服务端推送                                  |
| 实时通信   | WebSocket                   | 实时数据                                    |
| Beacon API | navigator.sendBeacon        | 页面关闭时发送请求                          |
| 请求封装   | axios / fetch 封装          | 统一接口调用、请求/响应拦截、token、错误    |
| 鉴权       | JWT / Token                 | 登录态管理、权限控制（路由守卫 / 按钮权限） |
| 跨域       | CORS                        | 前后端分离基础                              |
| Cookie     | sameSite / httpOnly         | 安全控制                                    |
| CSRF 防护  | token / sameSite            | 防攻击                                      |
| XSS 防护   | 输入过滤 / CSP              | 安全基础                                    |
| 请求优化   | 防抖 / 合并请求             | 减少请求次数                                |
| 缓存策略   | HTTP缓存（强缓存/协商缓存） | 提升性能                                    |
| 重试机制   | retry                       | 提高稳定性                                  |
| 超时控制   | timeout                     | 防止请求卡死                                |
| 取消请求   | AbortController             | 避免无效请求                                |
| 文件上传   | multipart/form-data         | 上传处理                                    |
| 文件下载   | blob / stream               | 下载处理                                    |

## 性能优化（运行时）

| 模块     | 掌握内容   | 说明                                   |
| -------- | ---------- | -------------------------------------- |
| 优化手段 | 前端性能   | 懒加载、代码分割、虚拟列表、防抖节流   |
| 首屏优化 | 首屏加载   | SSR、骨架屏、关键资源优先加载          |
| 资源加载 | 加载优化   | preload、prefetch、懒加载              |
| 渲染优化 | DOM性能    | 减少重排重绘、批量更新                 |
| 列表优化 | 大数据渲染 | 虚拟列表（virtual list）               |
| 事件优化 | 事件控制   | 防抖（debounce）、节流（throttle）     |
| 缓存策略 | 本地缓存   | HTTP缓存、localStorage、Service Worker |
| 图片优化 | 图片加载   | 懒加载、压缩、WebP、响应式图片         |
| JS优化   | 执行优化   | 减少主线程阻塞、Web Worker             |
| CSS优化  | 样式性能   | 减少复杂选择器、避免频繁重排           |
| 动画优化 | 动画性能   | requestAnimationFrame、GPU加速         |
| 网络优化 | 请求优化   | 减少请求数、合并请求、CDN              |
| 包体优化 | 资源体积   | Tree Shaking、按需加载                 |
| 指标监控 | 性能指标   | FCP、LCP、CLS                          |

## 测试

| 模块     | 掌握内容               | 说明             |
| -------- | ---------------------- | ---------------- |
| 单元测试 | Vitest                 | 组件/函数测试    |
| 组件测试 | Testing Library        | 用户视角测试组件 |
| E2E      | Playwright             | 模拟真实用户流程 |
| Mock     | 接口模拟（msw / mock） | 脱离后端测试     |
| 覆盖率   | coverage               | 测试质量评估     |
| CI 集成  | 自动化测试             | 提交/发布前校验  |


<!-- ## 作用域、闭包、this 与原型链

| 概念     | 人话理解       | 本质机制                     | 工程作用               |
|----------|----------------|------------------------------|------------------------|
| 作用域   | 能访问谁       | 词法作用域（定义时决定）     | 控制变量可见性         |
| 闭包     | 能记住谁       | 函数 + 作用域绑定            | 状态管理（hooks/composable） |
| this     | 当前是谁       | 动态绑定（调用时决定）       | 确定执行上下文         |
| 原型链   | 还能从谁那拿   | 对象委托（prototype chain）  | 复用 / 继承            | -->

<!-- | 层级 | 分类 | 技术 / 能力 | 核心内容 | 重要程度 |
|------|------|------------|----------|----------|
| 基础 | JavaScript | ES6+ | 闭包、作用域、this、原型链、Promise、async/await、事件循环 | ⭐⭐⭐⭐⭐ |
| 基础 | 浏览器原理 | 渲染机制 | DOM/CSSOM、重排重绘、缓存策略、CORS | ⭐⭐⭐⭐ |
| 框架 | Vue 3 | 核心能力 | 响应式（Proxy）、虚拟DOM、diff、Composition API | ⭐⭐⭐⭐⭐ |
| 框架 | 状态管理 | Pinia | 全局状态设计、模块拆分、持久化 | ⭐⭐⭐⭐ |
| 工程化 | 构建工具 | Vite | 开发服务器、打包、插件机制 | ⭐⭐⭐⭐⭐ |
| 工程化 | 包管理 | pnpm / npm | 依赖管理、lock机制 | ⭐⭐⭐⭐ |
| 工程化 | 代码规范 | ESLint + Prettier | 代码统一、团队协作 | ⭐⭐⭐ |
| 架构 | 前端分层 | 分层设计 | api / services / store / components / views | ⭐⭐⭐⭐⭐ |
| 架构 | BFF | Next.js | SSR、接口聚合、前后端中间层 | ⭐⭐⭐⭐ |
| 网络 | HTTP | 请求基础 | RESTful、状态码、请求封装（axios/fetch） | ⭐⭐⭐⭐⭐ |
| 网络 | 鉴权 | JWT / Token | 登录态管理、权限控制 | ⭐⭐⭐⭐ |
| UI | CSS | 布局 | Flex、Grid、响应式设计 | ⭐⭐⭐⭐⭐ |
| UI | 交互 | 动画 | 过渡动画、用户体验优化 | ⭐⭐⭐ |
| 性能 | 优化手段 | 前端性能 | 懒加载、代码分割、虚拟列表、防抖节流 | ⭐⭐⭐⭐ |
| 进阶 | TypeScript | 类型系统 | 类型约束、泛型、接口设计 | ⭐⭐⭐⭐⭐ |
| 进阶 | 全栈能力 | Vue + FastAPI | 前后端联动、接口设计、BFF | ⭐⭐⭐⭐ | -->
