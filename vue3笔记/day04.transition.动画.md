## Transition

> 单个动画， import 'animate.css' 结合 animate.css 使用

1. 直接定义 appear-active-class

```html
<h2>单个动画</h2>
<button @click="flag = !flag">切换</button>
<transition appear appear-active-class="animate__animated animate__bounceIn" enter-active-class="animate__animated animate__zoomIn" leave-active-class="animate__animated animate__hinge">
    <div v-if="flag" class="box"></div>
</transition>
```

2. 定义 transition 名称，按照名称写 class

```html
<transition name="fade">
    <div v-if="flag" class="box"></div>
</transition>
<style>
    /* 进入开始状态 */
    .fade-enter-from {
        width: 0;
        height: 0;
    }

    /* 动画时间 */
    .fade-enter-active {
        transition: all 0.5s ease
    }

    /* 动画结束 */
    .fade-enter-to {
        width: 100px;
        height: 100px;
    }
</style>
```

> 列表动画

```html
<template>
    <div>
        <h1>Transition 案例</h1>
        <h2>单个动画</h2>
        <button @click="flag = !flag">切换</button>
        <transition appear appear-active-class="animate__animated animate__bounceIn" enter-active-class="animate__animated animate__zoomIn" leave-active-class="animate__animated animate__hinge">
            <div v-if="flag" class="box"></div>
        </transition>

        <transition name="fade">
            <div v-if="flag" class="box"></div>
        </transition>

        <div></div>
        <h2>列表动画</h2>
        <button @click="addItem">增加</button>
        <button @click="removeItem">删除</button>
        <transition-group enter-active-class="animate__animated animate__bounceIn" leave-active-class="animate__animated animate__hinge">
            <div class="li" v-for="(item, index) in list" :key="index">
                {{ item }}
            </div>
        </transition-group>

        <div style="height: 200px"></div>
    </div>
</template>

<script setup lang="ts">
    import 'animate.css'
    import {
        reactive,
        ref
    } from 'vue'
    let flag = ref < boolean > (true)
    let flag1 = ref < boolean > (true)

    let list = reactive < number[] > ([1, 2, 3, 4, 5, 6])

    const addItem = () => {
        list.push(33)
    }
    const removeItem = () => {
        list.pop()
    }
</script>
<style scoped>
    .box {
        width: 200px;
        height: 200px;
        background-color: #6f6f6f;
    }

    .li {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px;
        margin: 5px;
        width: 150px;
        border: 1px solid;
        border-radius: 5px;
    }
</style>
```
