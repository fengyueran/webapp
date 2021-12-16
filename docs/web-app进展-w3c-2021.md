# Web App 进展-W3C-2021

## ARIA

ARIA 是 Accessible Rich Internet Applications 的缩写，它是 W3C 的[Web 无障碍推进组织(Web Accessibility Initiative / WAI)](http://www.w3.org/WAI/)在 2014 年 3 月 20 日发布的[可访问富互联网应用实现指南](http://www.w3.org/TR/2014/REC-wai-aria-20140320/)。

WAI-ARIA 是一个为残疾人士等提供无障碍访问动态、可交互 Web 内容的技术规范。在 WAI-ARIA 概述中对 WAI-ARIA 及其他支持文档进行了介绍，主要包括以下内容：

- ARIA 是 W3C 的一个独立规范，帮助 Web 应用程序和 Web 页面变得更具可访问性

  可访问性即尽可能最大范围覆盖各能力范围内的人群和各种情形下的操作, 即对所有人是可访问的(无论他们访问 Web 是否有障碍)。

- ARIA 主要是为了提升网页的可用性，网页对残疾人士的无障碍化

  主要针对的是视觉缺陷，失聪，行动不便的残疾人。尤其像盲人，眼睛看不到，其浏览网页则需要借助辅助设备，如屏幕阅读器，屏幕阅读机可以大声朗读或者输出盲文，而 ARIA 就是可以让屏幕阅读器准确识别网页中的内容，变化，状态的技术规范，可以让盲人这类用户也能无障碍阅读！

- HTML5 已经开始使用 ARIA，并且 W3C 发布的很多其他标准也开始使用 ARIA
- ARIA 是对 HTML 语义化的补充。它具备比现有的 HTML 元素和属性更完善的表达能力，并让你页面中元素的关系和含义更明确
- ARIA 规范为浏览器和解析 HTML 文档的辅助性技术提供了一种可以让人们以多种方式访问和使用 Web 的标准方法

### 为什么需要 ARIA

回答标题问题前我先问其他几个问题？

- 如何让盲人用户知道当前浏览区域就是网站主导航？
- 如果让盲人用户知道点击某个按钮后出来的是弹框？
- 如何让盲人用户知道点击某个按钮后页面另外一个区域的文字发生了变化？
- 如何让盲人用户知道您使用了 li 标签是用来模拟标准 select 控件呢？
- 如何让盲人用户知道您模拟的 select 控件是单选呢还是可以多选呢？

在你现有的知识范围内，您有办法解决上面的问题吗？有人会说，我使用 HTML5, 恩，确实，HTML5 的出现大大增强了网页的可访问性和无障碍阅读，但是，其不是万能的，例如无法让盲人知道模拟控件的类型等。

因此，才需要 ARIA.

### 如何使用 ARIA

应用于 HTML 的 ARIA 有两部分组成：**role**（角色）和带**aria-**前缀的属性，其作用：

- role(角色)标识了一个元素的作用
- aria-属性描述了与之有关的事物（特征）及其是什么样的（状态）

如下：通过 ARIA 实现一个进度条

```html
<div
  role="progressbar"
  aria-valuenow="75"
  aria-valuemin="0"
  aria-valuemax="100"
></div>
```

在 mac 上通过 Voice Over(cmd+f5)就可以识别上述的进度条，朗读出：

> web content; 50%, progress indicator

这样就可以让视力障碍着能够知道当前的网页内容是一个进度条，进度到了 50%。
如果不用 ARIA 是什么效果呢，下面是通过普通 div+css 实现的简单的 progress bar：

```html
<!DOCTYPE html>
<html lang="en">
  <style>
    .progressbar {
      position: relative;
      width: 200px;
      height: 20px;
      border: 1px solid;
    }
    .progressbar::after {
      position: absolute;
      content: "";
      width: 100px;
      height: 100%;
      background: red;
    }
  </style>
  <body>
    <div class="progressbar"></div>
  </body>
</html>
```

通过 voice over 读不出任何内容，这就是 ARIA 的作用。

### ARIA 在 HTML 中的使用

ARIA 在 HTML 中使用有其自己的规范，并不是说在 HTML 中使用了 ARIA，Web 页面就无障碍化了，就提高了可访问性了。言外之意，ARIA 没有用好，反而会把你带到另一个坑中，使用你的页面可访问性更差。

有关于 HTML 中 ARIA 的文档可以[点击这里阅读](https://specs.webplatform.org/html-aria/webspecs/master/)。
ARIA 在 HTML 中的使用有一些规则：

- 如果你使用的元素(HTML5)具有语义化，应该使用这些元素，而不应该重新定义一个添加 ARIA 的角色、状态或属性的元素。
- 不改变语义，除非你真的需要使用。例如，开发者想创建一个标题，而且它是一个按钮。
- 所有的 ARIA 制作控件都必须具有键盘(keyboard)事件。
- 不建议在可获取焦点元素(focusable)使用 ARIA 的角色：role=presentation 或 aria-hidden="true"。
- 所有交互元素都必须有一个[可访问的名称](https://www.w3.org/TR/accname-1.1/#dfn-accessible-name)。

### 2021 年更新

- 2021 年 5 月 13 日： [为 ARIA 角色更新允许添加的后代](https://github.com/w3c/html-aria/pull/322)
- 2021 年 3 月 7 日： [更新 nav 元素允许的角色](https://github.com/w3c/html-aria/commit/daca00dc304f5c3944ed0a0ae4d3b6f9d60039bc)。添加 menu,menubar 和 tablist 作为允许的角色
- 2021 年 2 月 20 日： [为 aria-\*HTML 中的特定属性添加单独的指南](https://github.com/w3c/html-aria/pull/262)。包括 aria-checked、aria-disabled、aria-hidden、aria-placeholder、aria-valuemax、aria-valuemin、aria-readonly、aria-required、aria-colspan、aria-rowspan、 的指南 aria-invalid
- 2021 年 2 月 19 日： [在 svg 上允许使用任何角色](https://github.com/w3c/html-aria/commit/4f246657493a1ecd87e762b17fffb3a09b919a13)
- 2021 年 2 月 19 日： [aria-disabled 不推荐在拥有 href 属性的 a 元素上 使用](https://github.com/w3c/html-aria/commit/8ab33901c72dd5a049a6ee04eb715c6f7ac3ac5c)
  2021 年 2 月 13 日：[阐明自定义元素角的用法](https://github.com/w3c/html-aria/commit/3a0d3dc62a7cf7be41e3253c98944b8594c8ecca)
  2021 年 2 月 13 日： [更新允许子元素的角色](https://gist.github.com/scottaohara/8df322bd24b1b687d21822287d9ea709)

### [Recommendation Track Process Maturity Levels](https://www.w3.org/2004/02/Process-20040205/tr.html)

The maturity level of a published technical report indicates its place in the Recommendation Track process. The maturity levels "Working Draft" and "Working Group Note" represent the possible initial states of a technical report in the Recommendation Track process. The maturity levels "Recommendation", "Working Group Note", and "Rescinded Recommendation" represent the possible end states.

- Working Draft (WD)

  A Working Draft is a document that W3C has published for review by the community, including W3C Members, the public, and other technical organizations(the group that is developing it).

- Candidate Recommendation (CR)

  A Candidate Recommendation is a document that W3C believes has been widely reviewed and satisfies the Working Group's technical requirements. W3C publishes a Candidate Recommendation to gather implementation experience.

- Proposed Recommendation (PR)
  A Proposed Recommendation is a mature technical report that, after wide review for technical soundness and implementability, W3C has sent to the W3C Advisory Committee for final endorsement.

- W3C Recommendation (REC)

  A W3C Recommendation is a specification or set of guidelines that, after extensive consensus-building, has received the endorsement of W3C Members and the Director. W3C recommends the wide deployment of its Recommendations. Note: W3C Recommendations are similar to the standards published by other organizations.

### ARIA IN HTML PUBLICATION HISTORY

```
2021-12-09	ARIA in HTML Recommendation
2021-09-30	Proposed Recommendation
2021-09-24	Candidate Recommendation Draft
2021-09-23	Candidate Recommendation Draft
2021-09-05	Candidate Recommendation Draft
2021-08-31	Candidate Recommendation Draft
2021-08-23	Candidate Recommendation Draft
2021-08-04	Candidate Recommendation Draft
2021-07-27	Candidate Recommendation Draft
2021-07-17	Candidate Recommendation Draft
2021-07-16	Candidate Recommendation Draft
2021-07-07	Candidate Recommendation Draft
2021-07-06	Candidate Recommendation Snapshot
2021-06-28	Working Draft
...
2015-05-14	Working Draft
2015-04-14	First Public Working Draft
```

### 参考资料

- [WAI-ARIA 无障碍 Web 规范](https://www.w3cplus.com/wai-aria/wai-aria.html)
- [wai-aria-无障碍阅读](https://www.zhangxinxu.com/wordpress/2012/03/wai-aria-%E6%97%A0%E9%9A%9C%E7%A2%8D%E9%98%85%E8%AF%BB/)
- [可访问性](https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility)
- [Recommendation Track Process Maturity Levels](https://www.w3.org/2004/02/Process-20040205/tr.html)
- [accessibility](https://developers.google.com/web/fundamentals/accessibility/semantics-aria?hl=zh-cn)
- [2021/10/w3c-highlights](https://www.w3.org/2021/10/w3c-highlights/Overview.html)
- [REC-html-aria-20211209](https://www.w3.org/TR/2021/REC-html-aria-20211209/)
