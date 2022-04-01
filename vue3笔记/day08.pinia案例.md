## Pinia 的使用

1. 安装

```sh
yarn add pinia
# 使用npm
npm i pinia
# 使用 pnpm
pnpm i pinia
```

2. 创建一个 Pinia
根目录新建一个 store 文件夹
src/store/index.ts

```ts
import { createPinia } from 'pinia'
const store = createPinia()
export default store
```

/src/main.ts

```ts
import store from '@/store'
app.use(store)
```

3. 使用 Pinia
写法一

```ts
import { defineStore } from 'pinia'
interface Person {
  name: string
  age: number
  address: Address
}
interface Address {
  id: string
  addressName: string
}

export const useUserStore = defineStore({
  id: 'user',
  state: () => {
    return {
      name: '孔维根',
      age: 30,
      address: {
        id: '1',
        addressName: '玻纤院'
      }
    }
  },
  actions: {
    updateUser: function (data: Person) {
      this.name = data.name
      this.age = data.age
      this.address = { ...data.address }
    }
  }
})
```

写法二 setup 写法

```ts
import {reactive} from 'vue'
const useUserStore = defineStore(() => {
  const user = reactive({
    {
      name: '孔维根',
      age: 30,
      address: {
        id: '1',
        addressName: '玻纤院'
      }
    }
  })
  function updateUser () {
    // TODO
  }

  return { user, updateUser }
})
```