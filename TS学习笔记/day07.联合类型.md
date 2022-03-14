### 联合类型

联合类型表示取值可以取多种类型中的一种，使用 `|` 分割每个类型

```ts
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven'; // OK
myFavoriteNumber = 7; // OK

let sayHelle = (name: string | null | undefined) => {
    /***/
}
```
### 类型别名
给类型起一个新名字，类型别名一般用于联合类型，当前操作并没创建新的类型
```ts
type Message = string | number;
let str: Message = '123'
str = 123
```

### 交叉类型
交叉类型试讲多种类型叠加一起，成为一种新的类型，通过 & 定义交叉类型；
一般用于多个接口和合并成一个类型
```ts
// 很明显，基本类型的交叉类型毫无意义，不存在同时满足的类型
type Useless = string & number

// 对象合并
type IntersectionType = { name:string,age:number } & {sex:string}
let mixed: IntersectionType = {
    name:"123",
    age:123,
    sex:'男'
}
```

