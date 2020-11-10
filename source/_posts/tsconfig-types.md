---
title: tsconfig
date: 2020-11-10 10:27:05
tags:
  - [typescript]
  - [tsconfig]
---

# tsconfig 中 typeRoots types @types 的区别和意义

   1. typeRoots 和 types 都是 tsconfig 中 compilerOptions 的配置项

   2. typeRoots 定义在哪些路径下查找ts定义模块，types 定义导入哪些定义模块

   3. @types 是由社区维护的第三方模块定义库，很多优秀的js模块都可以在这里找到定义库
   例如JQuery这种纯js库在ts中使用 可以直接 npm install -D @types/jquery 这样在import Jquery 时就会自动导入定义库了

### 示例代码
```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "strict": true,
    "jsx": "preserve",
    "importHelpers": true,
    "moduleResolution": "node",
    "experimentalDecorators": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "allowJs": true,
    "sourceMap": true,
    "baseUrl": ".",
    "typeRoots": ["./types", "./node_modules/@types"], // 只在列表中的路径下导入定义
    "types": ["webpack-env", "jest", "lodash", "moment"], // 只导入列表中的模块
    "paths": {
      "@/*": ["src/*"],
      "~/*": ["types/*"]
    },
    "lib": ["esnext", "dom", "dom.iterable", "scripthost"]
  },
  "include": ["types/*.ts", "src/**/*.ts", "src/**/*.tsx", "src/**/*.vue", "tests/**/*.ts", "tests/**/*.tsx"],
  "exclude": ["node_modules"]
}
```