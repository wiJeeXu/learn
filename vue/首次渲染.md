首次渲染
createApp(App).mount('#app')
App.vue

1. 普通标签

```html
<div>hello vue</div>
```

mount -> createVNode -> render -> patch

createVNode

1. ShapeFlags 类型
2. 生成 vnode

render

1. 如果 vnode 为 null 并且 div#app 存在\_vnode,执行 unmount 卸载函数
2. vnode 存在则执行 patch 函数

patch

n1: 老的 vnode
n2: 新的 vnode

1. 如果 n1 === n2,直接 return
2. 如果 n1 n2 不是一个标签类型,直接 unmout 卸载 n1,并把 n1 = null
3. 判断 type

- case Text 文本类型 执行 processText
- case Comment 注释类型 执行 processCommentNode
- case Static 未知类型 如果 n1 === null 执行 mountStaticNode, 否则是开发环境执行 patchStaticNode
- case Fragment 片段类型 多个跟节点 执行 processFragment
- case default ELEMENT 执行 processElement | COMPONENT 执行 processComponent | TELEPORT 执行 type.process | SUSPENSE 执 type.process

createApp(App) App.vue 组件

processComponent 解析

1. n1 == null, 如果 n2.shapeFlags === COMPONENT_KEPT_ALIVE,执行 parentComponent.ctx.activate,否则执行 mountComponent
2. n1 不为 null,执行 updateComponent

App.vue 初次渲染 n1 = null 并且 n2.shapeFlags != COMPONENT_KEPT_ALIVE,执行 mountComponent

mountComponent 解析

1. instance = compatMountInstance || initialVNode.component = createComponentInstance(initialVNode,
   parentComponent,
   parentSuspense)
2. setupComponent()

- initProps
- initSlots

3. setupRenderEffect()

- 注册 const componentUpdateFn = () => {}
- const effect = new ReactiveEffect(componentUpdateFn, () => queueJob(instance.update), instance.scope)
- const update = instance.update = effect.run.bind(effect)
- update()
