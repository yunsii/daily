# daily

🌱 种一棵树最好的时间是十年前，其次是现在。

<hr />

归档：[[2021](./2021.md)]

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
