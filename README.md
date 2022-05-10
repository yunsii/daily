# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

归档：[[2021](./2021.md)]

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
