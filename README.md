# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

归档：[[2021](./2021.md)]

**08.16** [Moving the mouse: mouseover/out, mouseenter/leave](https://javascript.info/mousemove-mouseover-mouseout-mouseenter-mouseleave)

These things are good to note:

- A fast mouse move may skip intermediate elements.
- Events `mouseover/out` and `mouseenter/leave` have an additional property: `relatedTarget`. That’s the element that we are coming from/to, complementary to `target`.

Events `mouseover/out` trigger even when we go from the parent element to a child element. The browser assumes that the mouse can be only over one element at one time – the deepest one.

Events `mouseenter/leave` are different in that aspect: they only trigger when the mouse comes in and out the element as a whole. Also they do not bubble.

值得注意的是，当需要鼠标移出窗口时触发回调直接通过 `document.addEventListener('mouseleave')` 实现在火狐浏览器环境是不生效的，当前的解决方案是通过 `document.documentElement.addEventListener('mouseleave')` 实现在谷歌和火狐浏览器都有效。

**08.01** [不需要 JS！仅用 CSS 也能达到监听页面滚动的效果！](https://mp.weixin.qq.com/s/aDJp-Vk2wsYRRFu7O8hkFg)

**05.18** [Understanding How Node.js Release Lines Work](https://nodesource.com/blog/understanding-how-node-js-release-lines-work/)

**05.15** [React官方出手，补齐原生Hook短板。Vue官方给出提醒：为什么在Vue中不需要useEvent？](https://mp.weixin.qq.com/s/gZ7eq8aq423FPH8C4eIxLA)

介绍了 React 一个新的 Hook —— `useEvent`，主要使用场景：**封装事件处理函数**。`useEvent` 当前还处于 [`RFC (Request For Comments)`](https://github.com/reactjs/rfcs/blob/useevent/text/0000-useevent.md) 阶段。

**05.12** [Element size and scrolling](https://javascript.info/size-and-scroll)

系统介绍了浏览器相关的坐标系统，特别的是提到了 [**Don’t take width/height from CSS**](https://javascript.info/size-and-scroll#don-t-take-width-height-from-css)，这下好了，又有活儿可以干了。

另外，评论中提到的一个 [swimyoung/web-coordinates](https://github.com/swimyoung/web-coordinates) 的项目，可以[在线预览](https://swimyoung.github.io/web-coordinates/)各种坐标值和大小，相当实用了，目前看来感觉还需要一个缩放获取相关数值的功能。

**05.11** [Web 字体 font-family 浅谈](https://segmentfault.com/a/1190000038284125)

分析了 font-family 的使用技巧，特别的还点评了各大网站的 font-family 配置。

**05.11** [Deep dive CSS: font metrics, line-height and vertical-align](https://iamvdo.me/en/blog/css-font-metrics-line-height-and-vertical-align)

深度解析了浏览器字体排版相关原理，仔细研读后获益匪浅，另外关于字体排版还有不少概念需要了解，比如 [10 Typography Terms Every Designer Should Know](https://creativemarket.com/blog/10-typography-terms-every-designer-should-know) 涉及的相关概念。

**05.10** [Typography](https://web.dev/learn/design/typography/)

系统讲解了文本排版的响应式。

**05.10** [A COMPREHENSIVE GUIDE TO FONT LOADING STRATEGIES](https://www.zachleat.com/web/comprehensive-webfonts/)

字体加载策略的综合指南，[FOUT, FOIT, FOFT](https://css-tricks.com/fout-foit-foft/) 说明了相关缩写的具体含义。

**05.09** [为什么现在我更推荐 pnpm 而不是 npm/yarn?](https://jishuin.proginn.com/p/763bfbd3bcff)

较为系统的分析的 pnpm 与 npm/yarn 的优劣，分为以下几个方面：

- 速度
- 磁盘空间
- monorepo
- 安全性

特别的，有个评论提到如果修改依赖中的代码怎么办？这也激发了我的好奇心，最后在 [patch-package](https://github.com/ds300/patch-package) 找到了一些线索：

- [Support pnpm package manager](https://github.com/ds300/patch-package/issues/35)
- [make work with pnpm and git, use pnpm-lock.yaml](https://github.com/ds300/patch-package/pull/302)
- [@milahu/patch-package](https://github.com/milahu/patch-package)

突然想起来我已经把项目改成 pnpm 了，还用了 [patch-package](https://github.com/ds300/patch-package)，好像没什么问题啊，有必要明天检查一下了 \_(:з」∠)\_

---

补充分析，今天实测下来，初步估计是因为在使用 yarn 的时候已经生成了 patches 补丁，在直接更换为 pnpm 的时候还是能用的，如果想重新打补丁就会报错了。因此如果使用 pnpm 的话，目前要么使用 `@milahu/patch-package` 包，要么自己重新发包，实在不行只能放弃使用 pnpm 管理了。

---

再补充一下，今天偶然发现一个 TS 类型问题，推测是 yarn (v1) 导致的。`@types/react-router` 有 `@types/react@*` 的依赖，目前最新的 `@types/react` 已经到了 18 了，此时如果项目内安装 `@types/react@^17` 的依赖，yarn 会为 `@types/react-router` 独立安装 v18 的依赖，部分代码会将 React 的相关类型指向 v18 的依赖，这就导致了 TS 报错类型不兼容，人傻了 \_(:з」∠)\_ 目前判断是 yarn 装依赖导致的。删除依赖和 lock 文件，使用 pnpm 装了一下，一切正常，看了一下 lock 文件，根本没有 `@types/react@^18` 的安装项。再看 yarn.lock 中：

```
"@types/react@*":
  version "18.0.9"
  resolved "https://registry.npmmirror.com/@types/react/-/react-18.0.9.tgz#d6712a38bd6cd83469603e7359511126f122e878"
  integrity sha512-9bjbg1hJHUm4De19L1cHiW0Jvx3geel6Qczhjd0qY5VKVE2X5+x77YxAepuCwVh4vrgZJdgEJw48zrhRIeF4Nw==
  dependencies:
    "@types/prop-types" "*"
    "@types/scheduler" "*"
    csstype "^3.0.2"
```

我想不必多言了。

**03.20** [这几个高级前端常用的API，你用到了吗？](https://segmentfault.com/a/1190000040942225)

做了下列 API 的简要说明并给出了一些很有趣的例子。

- MutationObserver
- IntersectionObserver
- getComputedStyle
- getBoundingClientRect
- requestAnimationFrame

**03.14** [新一代Web建站技术栈的演进：SSR、SSG、ISR、DPR都在做什么？](https://zhuanlan.zhihu.com/p/365113639)

**02.07** [CSS Grid 网格布局教程](https://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)

很久之前就听说 Grid 布局了，今天简单了解了一下，发现确实挺好的，如果不管 IE 兼容的话。

> 通过最近的实践，Grid 布局的适用场景还是完全网格化的布局（可存在网格合并），如果可能存在长度不成比例的情况下，还是 Flex 布局更佳。 —— 2022.03.14

**01.17** [重新构想原子化 CSS](https://antfu.me/posts/reimagine-atomic-css-zh)

<details>
<summary>阅读笔记</summary><br />

## 什么是原子化 CSS？

> 原子化 CSS 是一种 CSS 的架构方式，它倾向于小巧且用途单一的 class，并且会以视觉效果进行命名。

## 原子化 CSS 方案

- 传统方案，提供所有你可能需要用到的 CSS 工具
- 按需生成，预先扫描源代码 => 监听文件变化 => 按需生成

## 探讨的解决方案

- [框架] Tailwind CSS
- [框架] Windi CSS
- [引擎] UnoCSS

看来是时候对 CSS 的使用做出一些改变了。

</details>

**01.07** [Introduction to events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

<details>
<summary>阅读笔记</summary><br />

> [Event bubbling and capture](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling_and_capture)

分为三个阶段：

- 捕获阶段（capturing phase）
- 目标阶段（target phase）
- 冒泡阶段（bubbling phase）

更有关于阶段划分的详细 Demo。

> [Event delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation)

- event.target
- event.currentTarget

</details>
