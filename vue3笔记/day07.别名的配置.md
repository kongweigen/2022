## Vue3 别名配置

> vite.config.ts 增加别名配置项

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
// import path from "path" path 会直接报错 
// 尝试执行 npm install @types/node --save-dev 也无法解决
// 修改成 require 的方式引入
const path = require('path')
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  }
})
```

> ts 项目此时 @/router 还是会出现报错的情况， 需要重新配置 tsconfig.json，并不影响代码运行，是会影响 vscode 的编辑器
> 关键是 baseUrl 和 paths 的配置
```json
{
  "compilerOptions": {
    "target": "esnext",
    "useDefineForClassFields": true,
    "module": "esnext",
    "moduleResolution": "node",
    "strict": true,
    "jsx": "preserve",
    "sourceMap": true,
    "resolveJsonModule": true,
    "esModuleInterop": true,
    "lib": ["esnext", "dom"],
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```