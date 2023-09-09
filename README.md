# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

归档：[[2021](./2021.md)] [[2022](./2022.md)]

**09.09** HMR 初探

- [Webpack HMR 原理解析](https://zhuanlan.zhihu.com/p/30669007)
- [How should we set up apps for HMR now that Fast Refresh replaces react-hot-loader?](https://github.com/facebook/react/issues/16604#issuecomment-528663101)

结合这两个链接算是稍稍理解的 HMR 了，vite 插件实现看[这里](https://github.dev/vitejs/vite-plugin-react/blob/286360281992c425bf75cb0a18846f65fcdc5ef3/packages/plugin-react/src/index.ts)。HTML 和 CSS 的 HMR 实现相对于 JS 来说是最简单的，直接替换就好了，JS 特别是想 React 这样存在状态管理的框架的 HMR 看起来都需要官方支持才是最好的。

**08.04** [Idle Until Urgent](https://philipwalton.com/articles/idle-until-urgent/)

**06.06** [CRDT 简介](https://juejin.cn/post/7049939780477386759)

> CRDT (conflict-free replicated data type) 无冲突复制数据类型，是一种可以在网络中的多台计算机上复制的数据结构，副本可以独立和并行地更新，不需要在副本之间进行协调，并保证不会有冲突发生。

CRDT 有两种类型：Op-based CRDT 和 State-based CRDT，此文只介绍了 Op-based 的思路，State-based CRDT 看[这里](https://www.zxch3n.com/crdt-intro/design-crdt/)，又是大受震撼的一天。

**06.03** [为什么现在JSONP也不能进行跨域请求了？](https://segmentfault.com/q/1010000041163225)


因为这篇文章又学习了相关资源：

- [30 分钟理解 CORB 是什么](https://segmentfault.com/a/1190000016126079)
- [一篇文章彻底搞懂 JSONP](https://segmentfault.com/a/1190000038522212)
- [【计算机】15分钟读懂英特尔熔断幽灵漏洞-Emory](https://www.bilibili.com/video/av18144159)

又了解了个 CORB 的概念，另外是B站关于漏洞的介绍视频，真是让人大受震撼，漏洞总是能给人惊喜。

随便看看 [web 应用常见安全漏洞一览](https://segmentfault.com/a/1190000018004657)
