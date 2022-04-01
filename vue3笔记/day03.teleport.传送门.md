# 全局组件注册

```ts
import Card from './common/Card.vue'
import Modal from './common/Modal.vue'
createApp(App).component('Card', Card).component('Modal', Modal).mount('#app')
```

## 组件传送门 teleport

> 模态框的实现

```html
  <teleport to="body">
      <div class="modal" v-if="show">
          <div class="mask" @click="close"></div>
          <div class="box">
              <div class="header">
                  <span>标题</span>
                  <span @click="close">X</span>
              </div>
              <div class="content">我是内容</div>
              <div class="footer">
                  <button>确定</button>
                  <button @click="close">取消</button>
              </div>
          </div>
      </div>
  </teleport>
```

```ts
defineProps<{
  show: boolean
}>()

let emit = defineEmits(['close'])
const close = () => {
  emit('close')
}
```
