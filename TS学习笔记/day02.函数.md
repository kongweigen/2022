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
// let func01 = (x: number, y: number, z?: number): number => {
//  if (typeo
```