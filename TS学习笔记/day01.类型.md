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

#### 基本类型和包装类型

```ts
// 原始类型兼容包装类
let num01: number = 1;
let Num01: Number = 1;
// num01 = Num01;
Num01 = num01;
```

#### object、Object 和 {}

```ts
let lowerCaseObject: object;
lowerCaseObject = 1; // ts(2322)
lowerCaseObject = "a"; // ts(2322)
lowerCaseObject = true; // ts(2322)
lowerCaseObject = null; // ts(2322)
lowerCaseObject = undefined; // ts(2322)
lowerCaseObject = {}; // ok
```

{} 等价于 Object

```ts
let upperCaseObject: Object;
upperCaseObject = 1; // ok
upperCaseObject = "a"; // ok
upperCaseObject = true; // ok
upperCaseObject = null; // ts(2322)
upperCaseObject = undefined; // ts(2322)
upperCaseObject = {}; // ok
```

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


元祖

> 能够保存不同类型，同是限制数量的集合叫元祖。数量和类型都不确定的情况直接直接使用 any[]

```ts
let x: [string, number];
x = ["孔维根", 30]; // OK
// x = ["1", "2"]; // ERROR
// x = [1, 1]; // ERROR

// 解构
let [name, age] = x;

// 参数可选
type Point = [number, number?, number?];
let x: Point = [10];
let xy: Point = [10, 20];
let xyz: Point = [10, 20, 30];

// 只读元祖，通过 readonly 配置元祖的只读，不可单项修改，不过可以重新赋值
let readonlyTuple1: readonly [number, string];
readonlyTuple1 = [1, "2"];
readonlyTuple1 = [1, "3"];
// readonlyTuple1[1] = "3" // ERROR
```