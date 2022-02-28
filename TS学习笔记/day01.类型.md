### TypeScript 初始化

```ts
npm i -g typescript // ts 安装
npm i -g ts-node // ts-node 安装
tsc --init // 生成 tsconfig.json 文件
ts-node index.ts // 创建 index.ts，并通过命令进行监听
tsc index.ts // ts 文件编译成 js
```

#### 内置的八种类型

```ts
let str: string = "孔维根";
let len: number = 6;
let flag: boolean = false;
let u: undefined = undefined;
let n: null = null;
let obj: object = { name: "kwg" };
// TODO 需要修改 tsconfig.json
// let big: bigint = 100n;
// let sym: symbol = Symbol("1")

// unll/undefined 赋值给其他类型
str = null; // Type 'null' is not assignable to type 'string'.ts(2322)

// 通过联合类型实现
let str1: string | null | undefined = "tom";
str1 = undefined;
str1 = null;
```

> undefined 和 null 是任意类型的子类型，当 strictNullChecks: false 时候，str = null 是成立的，否则会有错误提示

TypeScript 中的严格模式跟 JavaScript 中说的严格模式（即 use strict）不是一个概念，它表示是否开启下面一系列的类型检查规则：

```ts
{
  "noImplicitAny": true,
  "strictNullChecks": true,
  "strictFunctionTypes": true,
  "strictBindCallApply": true,
  "strictPropertyInitialization": true,
  "noImplicitThis": true,
  "alwaysStrict": true
}
```

- 如果你设置 strict 为 true 的话，那么上面所有的配置默认全是 true
- 如果你设置 strict 为 false 的话，那么上面的所有配置默认全是 false
- 你如果既设置了 strict 又单独设置了其中的部分配置，那么以单独设置的配置为准

---

#### 其他类型

数组定义

```ts
let arr01: string[] = ["1", "2", "3", "4", "5"];
let arr02: Array<string> = ["4", "5", "6"];
// 联合类型
let arr03: Array<string | number | boolean> = ["1", 2, true, "2"];
// 对象数组
interface Person {
  name: string;
  age: number;
}
let arrObj01: Array<Person> = [{ name: "12", age: 12 }];
```
