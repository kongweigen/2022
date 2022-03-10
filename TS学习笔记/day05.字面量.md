### 字面量类型

ts 支持三种字面量类型，字符串字面量类型，数字字面量，布尔值字面量类型，对应的字面量类型和值的类型一致

```ts
let str04: 'this is str' = 'this is str'
let num07: 1 = 1
let boolean01: true = true
let str05: string = 'hello'
// str04 = '12' // Type '"12"' is not assignable to type '"this is str"'.
// str04 = str05 // error
str05 = str04
// 'this is str' 属于 string 的子类型
```

> 实际上，定义单个的字面量类型并没有太大的用处，它真正的应用场景是可以把多个字面量类型组合成一个联合类型，用来描述拥有明确成员的实用的集合。如下

```ts
type Direction = 'up' | 'down'
function move(dir: Direction) {
  console.log(dir)
}
move('up')
// move('right'); // ts(2345) Argument of type '"right"' is not assignable to parameter of type 'Direction'

interface Config {
  size: 'small' | 'big'
  margin: 10 | 20
  isEnable: true | false
}

let c: Config = {
  size: 'small',
  margin: 20,
  isEnable: false
}
```
let const 的类型
> const 定义的不可变的常量，缺省类型注释的情况下，类型由赋值的字面量类型决定

> let 正常执行类型推断
```ts
{
  const str = 'this is str' // str: 'this is str'
  const num = 1 //num: 1
  const bool = true // bool: boolean
}

{
  let str = 'this is str' // str: string
  let num = 1 // num: number
  let bool = true // bool: boolean
}
```