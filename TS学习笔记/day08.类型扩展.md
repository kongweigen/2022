### 交叉类型
```ts
// 交叉类型
{
  type IntersectionType = { name: string } & { id: number }
  let obj: IntersectionType = {
    name: '',
    id: 1
  }

  // 同名属性，类型冲突
  type IntersectionTypeConfict = { id: string; name: string } & {
    id: number
    age: number
  }

  // let obj1:IntersectionTypeConfict = {
  //   name: "13",
  //   age:1,
  //   id:"" // 类型冲突导致直接报错
  // }

  // 同名属性，类型和子类型
  type IntersectionTypeConfict1 = { id: number; name: string } & {
    id: 1
    age: number
  }
  // 交叉的类型为子类型
  let obj2: IntersectionTypeConfict1 = {
    id: 1,
    name: '123',
    age: 30
  }

  // 同名类型，非基本类型
  // type A = {
  //   x: { a: true }
  // }
  // type B = {
  //   x: { b: string }
  // }
  // type C = {
  //   x: { c: number }
  // }

  interface A {
    x: { a: true }
  }
  interface B {
    x: { b: string }
  }
  interface C {
    x: { c: number }
  }

  type ABC = A & B & C
  let abc: ABC = {
    x: {
      a: true,
      b: '',
      c: 1
    }
  }
}
// type: 类型别名，类型别名会给一个类型起个新名字。
// 类型别名有时和接口很像，但是可以作用于原始值，联合类型，元组以及其它任何你需要手写的类型。

// 接口
{
  interface Person {
    name: string
    age: number
  }
  // 定义的变量属性需要与类型保持一致
  let tom: Person = {
    name: '',
    age: 30
  }

  // 可选和只读属性
  interface Person1 {
    name: string
    age: number
    sex?: string // 可选属性
    readonly isAdmin: boolean // 只读属性
  }

  let p1: Person1 = {
    name: '孔维根',
    age: 29,
    isAdmin: false
  }
  // p1.isAdmin = true // 只读属性不可修改

  // 任意类型
  // 当可选属性和任意属性并存，则任意属性的类型需要包含可选属性的类型
  interface Person2 {
    name: string
    age?: number
    [propName: string]: string | number | undefined
  }
}

// 接口与类型别名
// 都可以描述对象和函数，语法不同
{
  interface Point {
    x: number
    y: number
  }
  interface SetPoint {
    (x: number, y: number): void
  }

  type Point1 = {
    x: number
    y: number
  }
  type SetPoint2 = (x: number, y: number) => void
}
// interface 支持接口重复定义，自动合并
{
  interface p1 {
    x: number
  }
  interface p1 {
    y: number
  }
  let p: p1 = { x: 1, y: 2 }
}

// 扩展，接口扩展通过 extends 扩展，类型别名通过 & 来实现
{
  interface PointX {
    x: number
  }

  interface Point extends PointX {
    y: number
  }
  let p: Point = { x: 1, y: 2 }
}

```