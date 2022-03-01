函数

- 声明定义

```ts
// 函数声明
function sum(a: number, b: number): number {
 return a + b;
}

// 函数表达式
let sum1 = (a: number, b: number): number => a + b;
console.log(sum1(1, 3));

let mySum: (x: number, y: number) => number = function (x, y) {
 return x + y;
};
mySum(1, 2);

// 接口定义函数类型
interface myFunc {
 (x: number, y: string): string;
}
let myFunc01: myFunc = (x, y) => x + y;
myFunc01(1, "2");
```

> 通过函数表达式定义、接口定义函数的方式时，对等号两侧左侧的类型进行限制，保证其类型的不可变。

- 参数

```ts
// 可选参数
let func01 = (x: number, y: number, z?: number): number => {
 if (typeof z === "number") {
  return x + y + z;
 } else {
  return x + y;
 }
};
console.log(func01(1, 2, 3)); // 6
console.log(func01(1, 2)); // 3

// 参数默认值
var func02 = function (x, y) {
 if (y === void 0) {
  y = 1;
 }
 return x + y;
};
console.log(func02(1, 2)); // 3
console.log(func02(1)); // 2

// 剩余参数
let func03 = (
 arr: Array<number>,
 ...items: Array<string>
): Array<number | string> => {
 if (Array.isArray(items)) {
  Array.prototype.push.apply(arr, items);
 }
 return arr;
};
// items [2, 4, 6, "tom"]
func03([1], 2, 4, 6, "tom");
```

函数重载

```ts
// 重载，函数名称相同，参数不同返回，不同的返回
type Types = string | number;
// 类型定义
function add(a: number, b: number): number;
function add(a: string, b: number): string;
function add(a: number, b: string): string;
function add(a: string, b: string): string;
// 函数定义
function add(a: Types, b: Types): Types {
 if (typeof a === "string" || typeof b === "string") {
  return a.toString() + b.toString();
 }
 return a + b;
}
// 没有覆盖当前参数类型，则 split 的调用就会报错，需要单独对返回值进行判断
add("1", "2").split(",");
```