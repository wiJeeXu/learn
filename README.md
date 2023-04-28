```
createApp(App).mount('#app')
```

1. 执行 runtime-dom 模块里的 createApp 函数
2. 执行 const app = ensureRenderer().createApp(...args) args:
3. createRenderer(options) options: node 节点的操作方法
4. 实际调用 baseCreateRenderer(options, undefined) 注册 patch、render 等函数,并返回{
   render,
   hydrate,
   createApp: createAppAPI(render, hydrate)
   }
5. ensureRenderer().createApp 执行实际执行的是 createAppAPI 返回的 createApp(rootComponent, rootProps = null) 函数
6. 执行 createApp(rootComponent, rootProps = null) 构造 app 对象并返回给第 2 步骤的 app,app 对象注册了 use、mixin、component、directive、mount、unmount、provide 函数,
7. 取出 app.mount 保存 const { mount } = app
8. 重构 app.mount 函数, 返回 app
9. app.mount('#app') 执行重构 app.mount 的函数
10. 执行 normalizeContainer('#app'), 返回 document.querySelector('#app')
11. container.innerHTML = '', 挂载之前清空
12. 执行保存的 mount 函数, mount(container, false, container instanceof SVGElement)
13. createVNode(rootComponent, rootProps), rootComponent 根组件的对象,rootProps = null
14. 实际执行的是\_createVNode, 返回 vnode
15. 执行 render 函数
16. 执行 patch 函数, patch(null, vnode, container, null, null, null, isSVG)
17. 执行 mountComponent
