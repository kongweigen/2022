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
