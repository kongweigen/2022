#### 类型推断

类型推断，这种基础类型变量的定义，无需标明类型，内部会自己推断

```ts
let str02: string = "123";
let str03 = "123";
str02 = str03;

let num02: number = 1;
let num03 = 2;

// 推断出 add02 返回值为 number
function add02(a: number, b: number) {
 return a + b;
}

// 变量声明不赋值，默认类型为 any
let num04;
num04 = 45; // any 类型
```

---
### 类型断言

语法
```ts
let arrNum: number[] = [1, 3, 4, 6];
// 在确定类型的情况下，进行 as 语法断言
let num05: number = arrNum.find((n) => n > 2) as number;

let someValue: any = "this is a string";
let strLen: number = someValue.length;
```

非空断言

```ts
let stringNullUndefined: null | undefined | string
// stringNullUndefined.toString() // error
stringNullUndefined!.toString()
```

确定类型断言

```ts
// let num06: number // console 会直接报错，他不确定 setNumber 是否对 num06 进行赋值
let num06!: number
setNumber()
console.log('num06', num06)
function setNumber() {
  num06 = 7
}
```