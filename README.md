# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

**12.12** [Developing in WSL](https://code.visualstudio.com/docs/remote/wsl)

<p align="center">
  <img src="./assets/images/architecture-wsl.png">
</p>
<p align="center">WSL 架构</p>

<details>
<summary>阅读笔记</summary><br />

> The Visual Studio Code Remote - WSL extension lets you use the Windows Subsystem for Linux (WSL) as your full-time development environment right from VS Code. You can develop in a Linux-based environment, use Linux-specific toolchains and utilities, and run and debug your Linux-based applications all from the comfort of Windows.

虽然用了 WSL + VS Code 很久了，这次来看看官方的操作手册。

> If you already have a folder open, you can also use the Remote-WSL: Reopen in WSL command. You will be prompted which distro to use.
>
> If you are in a WSL window and want to open the current input in a local window, use Remote-WSL: Reopen in Windows.

原来可以互操作，有点秀。此外还可以通过 Windows 的终端直接打开指定文件或目录，才想起来之前都是手动进入到 WSL 的终端打开的。

> If you install an extension from the Extensions view, it will automatically be installed in the correct location. Once installed, you can tell where an extension is installed based on the category grouping. There will be Local - Installed category and one for WSL.

> Local extensions that actually need to run remotely will appear dimmed and disabled in the Local - Installed category. Select Install to install an extension on your remote host.

扩展会自动安装到合适位置。

可通过 Remote-WSL: Show Log 查看 WSL 日志。

> If you are using WSL 2 and [Docker Desktop's WSL 2 back-end](https://docs.docker.com/docker-for-windows/wsl-tech-preview/), you can use the [Remote - Containers](https://code.visualstudio.com/docs/remote/containers) extension to work with source code stored inside WSL!

居然可以还可以在使用安装在 WSL 中的 Docker 容器 \_(:з」∠)\_

**我所关注的已知影响较大的限制：**

- [permission denied error trying to rename a folder in the open workspace in WSL 1](https://code.visualstudio.com/docs/remote/wsl#_i-see-eaccess-permission-denied-error-trying-to-rename-a-folder-in-the-open-workspace-in-wsl-1)
- [Webpack HMR not working](https://code.visualstudio.com/docs/remote/wsl#_nodejs-in-wsl-1)
- [Git limitations](https://code.visualstudio.com/docs/remote/wsl#_git-limitations)

</details>

**12.12** [What the heck are CJS, AMD, UMD, and ESM in Javascript?](https://dev.to/iggredible/what-the-heck-are-cjs-amd-umd-and-esm-ikm)

<details>
<summary>阅读笔记</summary><br />

**CJS**

CJS is short for CommonJS.

```js
//importing
const doSomething = require('./doSomething.js');

//exporting
module.exports = function doSomething(n) {
  // do something
};
```

- node 使用 CJS 模块格式
- 同步导入模块
- 导入的是对象的副本
- 不能在浏览器中直接使用

**AMD**

AMD stands for Asynchronous Module Definition.

```js
define(['dep1', 'dep2'], function (dep1, dep2) {
  //Define the module value by returning a value.
  return function () {};
});
```

or

```js
// "simplified CommonJS wrapping" https://requirejs.org/docs/whyamd.html
define(function (require) {
  var dep1 = require('dep1'),
    dep2 = require('dep2');
  return function () {};
});
```

- 异步导入模块
- 为前端而生
- 语法不如 CJS 直观

**UMD**

UMD stands for Universal Module Definition.

```js
(function (root, factory) {
    if (typeof define === "function" && define.amd) {
        define(["jquery", "underscore"], factory);
    } else if (typeof exports === "object") {
        module.exports = factory(require("jquery"), require("underscore"));
    } else {
        root.Requester = factory(root.$, root._);
    }
}(this, function ($, _) {
    // this is where I defined my module implementation

    var Requester = { // ... };

    return Requester;
}));
```

- 前后端适用
- 更像一个配置多个模块系统的模式
- 通常作为一个支持回退的模块系统

**ESM**

ESM stands for ES Modules. It is Javascript's proposal to implement a standard module system.

```js
import {foo, bar} from './myLib';

// ...

export default function() {
  // your Function
};
export const function1() {...};
export const function2() {...};
```

- 可直接在现代浏览器中使用

```html
<script type="module">
  import { func1 } from 'my-lib';

  func1();
</script>
```

- 支持类 CJS 的简单语法，以及 AMD 的异步加载 `import()`
- Tree Shaking，基于[静态模块结构](https://exploringjs.com/es6/ch_modules.html#static-module-structure)

此外，原文中包含各种规范的原文，有机会可以好生研究一下。

</details>

**12.12** [Web workers vs Service workers vs Worklets](https://bitsofco.de/web-workers-vs-service-workers-vs-worklets/)

<details>
<summary>阅读笔记</summary><br />

**Web workers**

通过类似 `const myWorker = new Worker('worker.js')` 的命令创建，通过 `postMessage` 通信。

**Service workers**

Service workers are a type of worker that serve the explicit purpose of being a **proxy between the browser and the network and/or cache**.

通过类似 `navigator.serviceWorker.register('/service-worker.js')` 的命令创建.

**Worklets**

Worklets are a very lightweight, highly specific, worker. They enable us as developers to hook into various parts of the browser’s rendering process.

通过类似 `CSS.paintWorklet.addModule('myWorklet.js')` 的命令创建。

</details>

**11.30** [React 运行时优化方案的演进](https://juejin.cn/post/7010539227284766751)

<details>
<summary>阅读笔记</summary><br />

开篇还推荐了几篇文章：

- [【React 深入】setState 的执行机制](https://mp.weixin.qq.com/s?__biz=Mzk0MDMwMzQyOA==&mid=2247490023&idx=1&sn=0ca662132f4f44ef61f608dcb095f1fa)
- [【React 深入】React 事件机制](https://mp.weixin.qq.com/s?__biz=Mzk0MDMwMzQyOA==&mid=2247490031&idx=1&sn=d2f80c18aef6ab40a0fdc2989cfb9906)
- [【React 深入】深入分析虚拟 DOM 的渲染过程和特性](https://mp.weixin.qq.com/s?__biz=Mzk0MDMwMzQyOA==&mid=2247490064&idx=1&sn=0f5047c2be91db25203c42b0ece074e9)
- [【React 深入】从 Mixin 到 HOC 再到 Hook](https://mp.weixin.qq.com/s?__biz=Mzk0MDMwMzQyOA==&mid=2247490057&idx=1&sn=e7a9abb4df2fb7f7baf406dbb20d8313)

看标题还挺有意思的。

> 编译时优化

> 运行时优化

说明了 Vue 在运行时和预编译取了一个很好地权衡，它保留了虚拟 dom，但是会通过响应式去控制虚拟 dom 的颗粒度，在预编译里面，又做了足够多的性能优化，做到了按需更新。而 React 在编译时很难做太多的事情，像 Vue 这样的编译时优化是很难实现的。所以，我们可以看到 React 几个大版本的的优化主要都在运行时。

另外还分析了 `getDerivedStateFromProps` API 和事件委托节点变更的历史原因以及 React 所做的各种运行时优化的工作，着实开了眼界，值得反复阅读，彻底弄懂文章提到的各种问题。

</details>

**11.16** 关于 JS 原型链

<p align="center">
  <img width="480" src="./assets/images/JavaScript-Object-Layout.jpg">
</p>
<p align="center"><a href="http://www.mollypages.org/tutorials/js.mp">JavaScript 对象模型</a></p>

- [原型链、继承和 instanceof](https://segmentfault.com/a/1190000008464190)
- [理解 JavaScript 的原型链和继承](https://blog.oyanglul.us/javascript/understand-prototype)
- [继承与原型链](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) 阅读前两遍文章后，阅读该文档更容易理解。

衍生问题 => `'abc' instanceof String; // false`

- [Why does instanceof return false for some literals?](https://stackoverflow.com/a/18057157/8335317)
- [Primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)
- [Object](https://developer.mozilla.org/en-US/docs/Glossary/Object)

**11.03** [字节跳动是如何落地微前端的](https://mp.weixin.qq.com/s/L9wbfNG5fTXF5bx7dcgj4Q)

<details>
<summary>阅读笔记</summary><br />

通过对比与实践介绍了微前端的优缺点及其整体架构。

</details>

**11.03** 关于设计模式

- [前端必备 10 种设计模式](https://segmentfault.com/a/1190000020179009)
- [前端需要了解的 9 种设计模式](https://zhuanlan.zhihu.com/p/133263261)

<details>
<summary>阅读笔记</summary><br />

设计原则

- 单一职责原则(SRP)：一个对象（只做一件事）。
  - 代理模式
  - 迭代器模式
  - 单例模式
  - 装饰者模式
- 最少知识原则(LKP)：一个软件实体应当尽可能少地与其他实体发生相互作用。
  - 中介者模式
- 开放封闭原则(OCP)：软件实体（类，模块，函数）应该都是可以扩展，但是不可修改
  - 发布订阅模式
  - 模板方法模式
  - 策略模式
  - 代理模式
  - 职责链模式

设计模式的类型

- 结构型模式（Structural Patterns）：通过识别系统中组件间的简单关系来简化系统的设计。
  - 外观模式（Facade Pattern）
  - 代理模式（Proxy Pattern）
- 创建型模式（Creational Patterns）：处理对象的创建，根据实际情况使用合适的方式创建对象。常规的对象创建方式可能会导致设计上的问题，或增加设计的复杂度。创建型模式通过以某种方式控制对象的创建来解决问题。
  - 工厂模式（Factory Pattern）
  - 单例模式（Singleton Pattern）
- 行为型模式（Behavioral Patterns）：用于识别对象之间常见的交互模式并加以实现，如此，增加了这些交互的灵活性。
  - 策略模式（Strategy Pattern）
  - 迭代器模式（Iterator Pattern）
  - 观察者模式（Observer Pattern）
  - 中介者模式（Mediator Pattern）
  - 访问者模式（Visitor Pattern）

</details>

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
