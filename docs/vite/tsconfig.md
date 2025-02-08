# TSConfig

```js
{
  "files": [],
  "references": [
    {
      "path": "./tsconfig.node.json"
    },
    {
      "path": "./tsconfig.app.json"
    },
    {
      "path": "./tsconfig.vitest.json"
    }
  ],
  "extends": "@vue/tsconfig/tsconfig.dom.json",

  // 指定 TypeScript 需要处理的 .ts / .d.ts 文件路径
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue", "packages/src/**/*", "packages/src/**/*.vue"],

  // 排除 TypeScript 需要编译的文件或目录
  "exclude": ["src/**/__tests__/*", "packages/**/__tests__/*"],
  "compilerOptions": {
    "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo",


    // 编译时（TypeScript 类型检查和编译阶段） | 提供给 TypeScript 的路径别名，用于类型检查和 IntelliSense 提示，与 Vite 构建无直接关系。只在vite.config.ts的alias配置使用后，但tsconfig.json未配置，run build 时路径解析失败，因为 TypeScript 不知道别名。
    "paths": {
      "@/*": ["./src/*"],
      "@OarUI/*": ["./packages/src/*"]
    },
  }
}

```
