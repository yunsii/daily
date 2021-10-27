# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

**10.26** [你需要了解的六种渲染模式](https://segmentfault.com/a/1190000023469150)

<p align="center">
  <img src="./assets/images/渲染模式对比.png">
</p>
<p align="center">渲染模式对比</p>

<details>
<summary>阅读笔记</summary><br />

> - SSR (Server Side Rendering)，关联阅读 [彻底理解服务端渲染 - SSR 原理](https://github.com/yacan8/blog/issues/30)
> - SSG (Static Site Generation)
>   - 静态网站生成类似于服务器端渲染，不同之处在于您在构建时而不是在请求时渲染页面。
> - SSR With hydration -对曾经渲染过的 HTML 进行重新渲染的过程称为水合。
> - CSR with Pre-rendering
> - CSR (Client Side Rendering)
> - 三态渲染 (Trisomorphic Rendering)
>   - 如果你可以结合 Service-Worker, 则三态渲染模式也可能派上用场。

另外加一个 Modern.js 提到到 **SPR**，无服务预渲染（Serverless Pre-rendering）是一种通过预渲染与缓存的方式，为 SSR 页面提供静态 Web 响应性能的技术方案。理解下来好像跟三态渲染思路类似？页面直接可视范围内可以做到无感刷新。

</details>

**10.25** [解读新一代 Web 性能体验和质量指标](https://juejin.cn/post/6844904168591736846)

<details>
<summary>阅读笔记</summary><br />

> 网站开发者不应该为了理解他们交付给用户的体验的质量指标而成为性能专家。`Web Vitals` 计划的目的就是简化场景，降低学习成本，并帮助站点关注最重要的指标，即 `Core Web Vitals`。

> `Core Web Vitals` 是应用于所有 Web 页面的 `Web Vitals` 的子集，所有的站点开发者都应该关注一下，他们将在所有谷歌提供的性能测试工具中进行显示。每个 `Core Web Vitals` 代表用户体验的一个不同方面，在该领域是可衡量的，并反映了以用户为中心的关键结果的真实体验。

> 网页核心的性能指标应该是随着时间的推移而不断演变的。当前 2020 年主要关注用户体验的三个方面——加载、交互性和视觉稳定性：
>
> - `Largest Contentful Paint (LCP)`: 衡量加载体验：为了提供良好的用户体验， LCP 应该在页面首次开始加载后的 2.5 秒内发生。
> - `First Input Delay (FID)`: 衡量可交互性，为了提供良好的用户体验，页面的 FID 应当小于 100 毫秒。
> - `Cumulative Layout Shift (CLS)`:衡量视觉稳定性，为了提供良好的用户体验，页面的 CLS 应保持小于 0.1。

</details>

**10.23** [浏览器的重排和重绘](https://juejin.cn/post/6932734614440001549)

<p align="center">
  <img src="./assets/images/browser-components.png">
</p>
<p align="center">浏览器核心组件</p>

躺在收藏夹很久了，读了才发现概念混乱，还有错别字，不过[原文](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)看起来很专业。

**10.22** [关于 JS 隐式类型转换的完整总结](https://segmentfault.com/a/1190000040048164)

较为全面的总结了 JS 隐式类型转换的各种情况。

<details>
<summary>阅读笔记</summary><br />

- ToPrimitive - 内部方法
  - toPrimitive(input: any, preferedType?: 'string' |'number')
- ToNumber
- 加减法中隐式转换规则
  - 遇到对象先执行 ToPrimitive 转换为基本类型
    - 加法（+）运算，preferedType 是默认值
    - 减法（-）运算，preferedType 是 Number
  - 字符串 + 任意值，会被处理为字符串的拼接
  - 非字符串 + 非字符串，两边都会先 ToNumber
  - 任意值 - 任意值，一律执行 ToNumber，进行数字运算
  - - x 和 一元运算 +x 是等效的（以及- x)，都会强制 ToNumber
  - {} 在最前面时可能不再是对象
    - 代码块
    - 标签
  - Symbol 不能加减
- 宽松相等（==），相等于全等都需要对类型进行判断，当类型不一致时，宽松相等会触发隐式转换。
  - 对象 == 对象，类型一致则不做转换
  - 对象 == 基本值，对象先执行 ToPrimitive 转换为基本类型
  - 布尔值 == 非布尔值，布尔值先转换成数字，再按数字规则操作
  - 数字 == 字符串，字符串 ToNumber 转换成数字
  - null、undefined、symbol
    - null、undefined 与任何非自身的值对比结果都是 false，但是 null == undefined 是一个特例
- 对比（<>），对比不像相等，可以严格相等（===）防止类型转换，对比一定会存在隐式类型转换。
  - 对象总是先执行 ToPrimitive 为基本类型
  - 任何一边出现非字符串的值，则一律转换成数字做对比
- ToBoolean
  - if(...)
  - for(;...;)
  - while(...)
  - do while(...)
  - ... ? :
  - ||
  - &&
- 总结，对象都需要先 ToPrimitive 转成基本类型，除非是宽松相等（==）时两个对象做对比。
  - \+ 没有字符串就全转数字
  - \- 全转数字，preferedType = Number
  - == 同类型不转，数字优先，布尔全转数字，null、undefined、symbol 不转
  - <> 数字优先，除非两边都是字符串

字符串在进行大小比较时，会根据第一个不同的字符的 ASCII 码值进行比较，当数字与字符串比较大小时，会强制的将字符串转换成数字然后再进行比较

</details>

**10.21** [CSS 中重要的 BFC](https://segmentfault.com/a/1190000013023485)

CSS 基础有点薄弱，理解得不多……

**10.20** [如何推动前端团队的基础设施建设](https://juejin.cn/post/6844904093434019853)

全面的探讨了前端团队的基础设施建设的目的和方法。

<details>
<summary>阅读笔记</summary><br />

> “技术基建”，就是研发团队的技术基础设施建设，是一个团队通用的技术能力沉淀。

> 业务支撑 是 <ins>活在当下</ins><br/>
> 技术基建 是 <ins>活好未来</ins>

> **技术的价值在于解决业务问题**，“业务支撑” 和 “基础建设” 从来都是同一件事的两个面，这个 “同一件事”，就是帮助业务解决问题。任何脱离解决实际场景而发起的基建，都需要重新审视甚至不应被鼓励。

> 有时候阶段性的忙和加班是不可避免的……当这一阵过去后，团队一定要思考，怎么做能更高效。站在未来看今天，如果一年、两年后，业务量增长 N 倍，那时候该如何支持，现在的方式是否能满足？不可能靠堆人，只能靠技术建设去提效降成本，这就是基建最核心的价值：帮助业务更好的活在未来。

![](./assets/images/研发流程闭环.png)

<p align="center">研发流程闭环</p>

> **提效**、**体验**、**稳定性**，是基建要解决的最重要的目标，通用的公式是 标准化 + 规范化 + 工具化 + 自动化，能力完备后可以进一步提升到平台化 + 产品化。

后续详细介绍了**基建怎么搞**，甚至做了一个桌面客户端，基本所有的操作都能通过客户端实现，开发者只需要专注编码就行了，让我大受震撼，前端基建还能这么玩。

> 技术的价值，在于解决业务问题；人的身价，在于解决问题的能力。但解决问题，技术基建绝不是银弹，甚至在我来看，都不是排在前三位的。
>
> 业务架构 - 业务产品的抽象、设计、架构的合理性，是影响投入产出比的重要因素。<br />
> 业务支撑 - 研发团队的首要责任，是帮助业务活在当下，做好支撑。对于创业期团队尤是如此。<br />
> 流程制度 - 优异的治理结构（流程、制度）带来的正向影响，往往会出乎人们的认知。<br />
> 基础设施 - 技术的基础设施建设，是为了业务更好的活在未来，但基建并不是银弹。

> 最后，思考一个问题：因为你，什么会变得不一样？

</details>

**10.19** [Dan Abramov 访谈实录](https://mp.weixin.qq.com/s/SBVE34dW9g4BsabmLJV9wg)

重点介绍了 React 的设计思想和未来的发展方向。

<details>
<summary>阅读笔记</summary><br />

> 不应该去浮于表面地去讨论哪个库更好，而是去看你要处理的状态是什么种类，使用这些库的目的是什么，选用不同方案带来的差异是什么。

[TODO] 关于提及的 React Query，Apollo 和 React Relay 库，有空学习一下具体的 API 设计和代码实现。

> 关于 React 入门难的原因，其一是需要 JavaScript 编程基础，其二是开发环境，如果使用 Next.js 或 create-react-app 作为项目起点是一个不错的开始。

另外个人认为 UmiJS 对于国内玩家来说也是一个不错的开始。

> React 避坑，其一是不变性（immutability），其二理解 React 的渲染流程应当是纯粹的（Rendering is supposed to be pure），当组件进行渲染的时候，它就是在计算下一个 UI 应该长什么样子，你不应该在渲染流程中掺杂其他的操作。我认为理解 UI 是计算结果 （UI is a calculation）这个范式是非常重要的。

> 前端发展太快？如果你对已经存在的东西足够熟悉、理解足够深的话，你可能就不会对新出现的东西感到新奇了，因为它们某种程度上讲是同质化的东西。所以我觉得准备迎接新事物的最好方法就是去熟悉已有的东西，当你足够熟悉之后，你看到就只有相似性了。

> 如果要我讲 React 未来的样子的话，我希望它能够成为一个工具，一个帮助我写组件的工具，里面集成了 data-fetching，代码分割，动画渲染等等所有功能，而且这些功能都无缝地组合在一起。因为 React 的中心思想就是像乐高一样，将各部分功能组合起来，我们希望在未来能够支持这些功能。

> 我们对如何实现动画这个功能有自己的构想，这个构想会与 React 库深入结合，它会不同于我们现在看到的所有框架。

听起来就很让人期待了。

> 当我们提到 “Virtual-DOM” 这个词的时候，我们说的其实是一种 UI 在内存中的表现形式。这应该是你期望得到的东西，因为它为开发者提供了更多的选择。

关于 **React 的竞争力** 值得深入理解，感受到 React 还有无穷的创造力。

> **Server Component**，Client Component 和 Shared Component

> 对我来说，有一个能够无时无刻学习新事物的环境是最重要的。

</details>
