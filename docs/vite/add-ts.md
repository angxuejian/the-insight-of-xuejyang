


# Add TS


## 模块路径

|配置文件 | 作用区域|	功能说明| 错误时机|
| ----- | ---- | ----| --- |
| vite.config.ts 的 alias | 运行时（Vite 构建和开发环境） | 解析模块路径，用于 Vite 在开发服务器和打包时找到正确的文件。| run dev 时路径解析正确，因为 Vite 知道别名的映射
| tsconfig.json 的 paths | 编译时（TypeScript 类型检查和编译阶段） | 提供给 TypeScript 的路径别名，用于类型检查和 IntelliSense 提示，与 Vite 构建无直接关系。| run build 时路径解析失败，因为 TypeScript 不知道别名。

### 1、.d.ts
.d.ts 文件用于定义模块的类型，解决模块缺少类型声明的问题。它告诉 TypeScript：

- 模块存在，并且有相应的类型。
- 如何为模块提供类型检查和 IDE 自动补全。


### 2、ts config

新增ts类型

#### 2.1、vue 默认配置
```json
// tsconfig.json

{
  "extends": "@vue/tsconfig/tsconfig.dom.json",
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue"],
  "exclude": ["src/**/__tests__/*"],
  "compilerOptions": {

    "paths": {
      "@/*": ["./src/*"],
    },
  }
}
```

```js
// vite.config.ts

import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'


// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url)),
    },
  },
})
```

只需要在`include`、`paths`、`alias`增加对应的文件即可



#### 2.2、新增配置

```json
// tsconfig.json

{
  "extends": "@vue/tsconfig/tsconfig.dom.json",
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue", "packages/src/**/*", "packages/src/**/*.vue"],
  "exclude": ["src/**/__tests__/*", "packages/**/__tests__/*"],
  "compilerOptions": {

    "paths": {
      "@/*": ["./src/*"],
      "@OarUI/*": ["./packages/src/*"]
    },
  }
}
```


```js
// vite.config.ts

import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url)),
      '@OarUI': fileURLToPath(new URL('./packages/src', import.meta.url))
    },
  },
})
```


