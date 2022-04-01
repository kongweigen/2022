## 响应式

### ref

类型申明响应式对象，通过 .value 来访问，模板中可以直接访问

```ts
let name:Ref<string> = ref("")
let name = ref<string>("")
```

### shallowRef

> 创建一个跟踪自身 .value 变化的 ref，但不会使其值也变成响应式的。  --官方文档

```ts
let shallowRefNum = shallowRef({ num: 1 })
let shallowRefNum2 = shallowRef(2)
let shallowName = shallowRef({ name: '孔维根' })

const changeShallowName = () => {
  shallowName.value.name = 'kwg' // 非响应式
}
const changeNum = () => {
  shallowRefNum.value.num++  // 非响应式
}
const changeNum = () => {
  shallowRefNum2.value = 999  // 响应式
}
const changeNum = () => {
  shallowRefNum.value.num++  // 响应式
  shallowRefNum2.value = 999
}
```

> 单独修改 shallowRef 定义的数据不会触发响应式（但是值已经修改了），现在触发其他响应式数据的修改，shallowRef 定义的数据会重新触发响应式  
> 具体原因可能要翻一下源码才知道了


### toRef

> 用来为源响应式对象的某一个 property 新建一个 ref。 然后 ref 可以被传递，他会保持对其源 property 的响应式连接

```ts
type Person = { name: string }
let obj = reactive<Person>({
  name: 'kwg'
})
let name: Ref<string> = toRef(obj, 'name')
const changeName = () => {
    name.value = "已修改"
}
```
5
### toRefs

> 将响应式对象转换成普通对象，其中的每个 property， 都指向原对象对应的 property
> 一般用于对象解构，保持响应式

```ts
// toRefs
let { name, age } = toRefs(obj)
console.log(name, age);
```

### toRaw

> 返回 reactive 或 readonly 代理的原始对象。这是一个“逃生舱”，可用于临时读取数据而无需承担代理访问/跟踪的开销，也可用于写入数据而避免触发更改。不建议保留对原始对象的持久引用。请谨慎使用。

```ts
let obj = reactive({
    name:"kwg",
    age:19
})
console.log(obj);
console.log('toRaw', toRaw(obj));
// Proxy {name: 'kwg', age: 19}
// ToRawDemo.vue:15 toRaw {name: 'kwg', age: 19}
```