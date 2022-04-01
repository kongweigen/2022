## 响应式Demo

> 通过 proxy effect 实现页面响应式

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>数据响应式</title>
</head>

<body>
    <div id="app">
        <h1>响应式练习</h1>
        <input type="text" id="ipx" />
        <p id="msg"></p>
    </div>
    <script>
        let activeEffect
        let weakMap = new WeakMap()
        let obj = {
            ok: true,
            name: '孔维根',
            age: 30
        }
        let data = new Proxy(obj, {
            get(target, key) {
                track(target, key)
                return target[key]
            },
            set(target, key, nv) {
                if (target[key] !== nv) {
                    target[key] = nv
                }
                trigger(target, key, nv)
            }
        })

        function track(target, key) {
            if (!activeEffect) return
            let depMap = weakMap.get(target)
            if (!depMap) {
                weakMap.set(target, (depMap = new Map()))
            }
            let deps = depMap.get(key)
            if (!deps) {
                depMap.set(key, (deps = new Set()))
            }
            if (!deps.has(activeEffect)) {
                deps.add(activeEffect)
            }
            activeEffect.deps.push(deps)
        }

        function trigger(target, key, nv) {
            let depMap = weakMap.get(target)
            let deps = depMap.get(key)
            // 防止死循环，track 里面在 add，trigger里面在 delete
            const depsFn = new Set(deps)
            depsFn &&
                depsFn.forEach((dep) => {
                    console.log('nv', nv)
                    dep()
                })
        }

        function effect(fn) {
            const _effect = () => {
                // 清除依赖副作用
                clearFn(_effect)
                activeEffect = _effect
                fn()
            }
            _effect.deps = []
            _effect()
            return _effect
        }

        // 清除 track 中 deps 关联的副作用函数，effect 执行的时候会重新进行依赖收集
        function clearFn(effectFn) {
            for (let i = 0; i < effectFn.deps.length; i++) {
                let deps = effectFn.deps[i]
                deps.delete(effectFn)
            }
            effectFn.deps.length = 0
        }

        effect(() => {
            document.getElementById('msg').innerText = data.ok ? data.name : 'not'
        })

        setTimeout(() => {
            data.name = 'hello'
        }, 1000)

        setTimeout(() => {
            data.name1 = 'hello1'
        }, 2000)
        setTimeout(() => {
            data.name = '培根666'
            data.ok = false
        }, 3000)
        setTimeout(() => {
            data.name = '不应该生效'
        }, 4000)
    </script>
</body>

</html>
```
