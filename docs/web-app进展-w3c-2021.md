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

## Indexed Database API 3.0

[Web 应用工作组](https://www.w3.org/2019/webapps/) 在 20210311 发布了第一个 working draft，2.0 的 Recommendation 版本是在 20180130， 1.0 的 Recommendation 版本是在 20150108。

### Indexed Database 是什么

IndexedDB 是一种可以让你在用户的浏览器内持久化存储数据的方法。IndexedDB 为生成 Web Application 提供了丰富的查询能力，使我们的应用在在线和离线时都可以正常工作，尤其是支持存储大容量的数据。

IndexedDB 和 Web SQL Database 都是本地数据库数据存储，Web SQL Database 数据库要出来的更早，然而，2010 年 11 月 18 日 W3C 宣布舍弃 Web SQL database 草案。

### 兼容性

可以看到 index db2.0 基本都是支持的。
![http://blog-bed.oss-cn-beijing.aliyuncs.com/webapp/index-db.png]

### Indexed Database 特性

- key/value 的存储方式：IndexedDB 和 localStorage 的存储方式很类似，都是通过一个 key 对应一个 value，而且 key 是唯一的方式进行存储的，但是 indexedDB 和 localStorage 有很不一样的一点，就是可以直接存储对象数组等，不需要想 localStorage 那样必须转为字符串。
- 异步调用：IndexedDB 是使用异步调用的，当我们存储一个较大的数据时，不会因为写入数据慢而导致页面阻塞。
- 支持事务：IndexedDB 支持事务，如果有用过 mysql 和 mongoDB 的人就很清楚了，能确保我们多个操作只要其中一步出现问题，可以整体回滚。
- 同源限制：IndexedDB 和 localStorage 一样，都是有同源策略的问题，不能跨协议、端口、域名使用。
- 支持二进制：IndexedDB 不但可以存储对象，字符串等，还可以存储二进制数据。
- 储存空间：IndexedDB 存储空间相比 localStorage 要大得多。

### Indexed Database 3.0 的修订历史

以下是 2.0 规范后更改的信息摘要。完整的修订历史可以在[这里](https://github.com/w3c/IndexedDB/)找到。有关第一版的修订历史，请参阅该文档的[修订历史](https://www.w3.org/TR/2015/REC-IndexedDB-20150108/#revision-history)。有关第二版的修订历史，请参阅该文档的[修订历史](https://www.w3.org/TR/IndexedDB-2/#revision-history)。

- 清理[索引数据库事务的算法](https://www.w3.org/TR/IndexedDB/#cleanup-indexed-database-transactions)([PR#232](https://github.com/w3c/IndexedDB/pull/232)）

- [更新了部分接口定义](https://www.w3.org/TR/IndexedDB/#global-scope)([PR #238](https://github.com/w3c/IndexedDB/pull/238))

- 添加了[databases()](https://www.w3.org/TR/IndexedDB/#dom-idbfactory-databases)方法([Issue #31](https://github.com/w3c/IndexedDB/issues/31))

- 添加了 [commit()](https://www.w3.org/TR/IndexedDB/#dom-idbtransaction-commit)方法([Issue #234](https://github.com/w3c/IndexedDB/issues/234)）

- 添加了 [request](https://www.w3.org/TR/IndexedDB/#dom-idbcursor-request) 属性([Issue #255](https://github.com/w3c/IndexedDB/issues/255)）

- 删除了 lastModifiedDate 对 [File](https://w3c.github.io/FileAPI/#dfn-file) 对象的非标准属性的处理([Issue #215](https://github.com/w3c/IndexedDB/issues/215)）

- 删除[includes()](https://www.w3.org/TR/IndexedDB/#dom-idbkeyrange-includes)方法([Issue #294](https://github.com/w3c/IndexedDB/issues/294)）
- 将数组键转换为[数组奇异对象](https://tc39.github.io/ecma262/#array-exotic-objects)(如代理)([Issue #309](https://github.com/w3c/IndexedDB/issues/309)）

- 在克隆操作期间，事务现在暂时处于非活动状态。

- 添加了 [durability](https://www.w3.org/TR/IndexedDB/#dom-idbtransactionoptions-durability) 选项和 [durability](https://www.w3.org/TR/IndexedDB/#dom-idbtransaction-durability) 属性([Issue #50](https://github.com/w3c/IndexedDB/issues/50)）

- 在[§ 2.7.2 Transaction scheduling](https://www.w3.org/TR/IndexedDB/#transaction-scheduling)添加更细致的说明，并在运行具有重叠范围的只读事务时禁止启动读/写事务([Issue #253](https://github.com/w3c/IndexedDB/issues/253)）

- 添加了[可访问性注意事项](https://www.w3.org/TR/IndexedDB/#accessibility)([Issue #327](https://github.com/w3c/IndexedDB/issues/327)）

- 使用[infra](https://www.w3.org/TR/IndexedDB/#biblio-infra)的列表排序定义([Issue #346](https://github.com/w3c/IndexedDB/issues/346)）

### 发布历史

```
2021-10-06	Working Draft
2021-06-18	Working Draft
2021-03-11	First Public Working Draft
```

### 参考文档

- [REC-IndexedDB-20150108/](https://www.w3.org/TR/2015/REC-IndexedDB-20150108/)
- [REC-IndexedDB-2-20180130](https://www.w3.org/TR/2018/REC-IndexedDB-2-20180130/)
- [history/IndexedDB-3](https://www.w3.org/standards/history/IndexedDB-3)
- [infra](https://infra.spec.whatwg.org/)
- [IndexedDB_API/Basic_Terminology](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Basic_Terminology)
- [html5-indexeddb-js-example](https://www.zhangxinxu.com/wordpress/2017/07/html5-indexeddb-js-example/)
- [新一代的前端存储方案--indexedDB](https://juejin.cn/post/6844903613240705038)

## PWA

This is Diego from the Microsoft Edge Team working on PWAs.

### Edge 团队在 PWA 上的进展

桌面 PWA 具有大量可能的功能——响应式设计、操作系统主题支持、自定义标题栏、快捷方式、从应用程序共享、共享到应用程序、处理方案、链接、文件以及对文件系统本身的访问。还有徽章和推送通知，但它们已被很好地涵盖，不会包含在本次演讲中。

#### 安装方式

1）通过浏览器安装
支持 PWA 的现代浏览器在打开 PWA 网站时，在地址栏会出现安装按钮，点击即可安装。
![](http://blog-bed.oss-cn-beijing.aliyuncs.com/webapp/pwa-install-browser.png)
安装完后就像普通的桌面程序一样，通过 Lanuchpad(mac 系统)就可以查找到了。
2）从 PWA 应用商店安装
目前 Windows 10 系统内置的 Microsoft Store 应用商店已经内置了很多 PWA 应用，当然还有其他很多 PWA 应用商店，如：
[appsco](https://appsco.pe/)、[pwastart](https://appstore.pwastart.com/)。

此外，通过 [PWABuilder](https://www.pwabuilder.com/)可以将 PWA 应用上传到 ios app store 或其他 PWA Builder process 上传到对应的 store。

And today, I'm gonna share with you a demo that showcases how the features that we're working on allow your installed web app to integrate with the desktop operating system, be it Windows, Linux, or even Mac OS. So, the first thing that we need to know is how to acquire the PWA.

#### PWA 具有的功能

- 响应式的设计和主题
  拖动改变窗口大小时 layout 可以动态的调整，此外改变系统主题，ui 也会跟着变化，这使得 PWA 与和本地操作系统结合得更紧密。

- 可以自定义窗口控制层(名称、关闭按钮、最小化、最大化等)
  窗口的各种状态也是会记住的，关闭 PWA 再打开会是上次打开的状态，比如改变了窗口大小、隐藏了保存、分享等按钮下次打开时还是之前的状态，这对用户更友好。

- 快捷图标
  快捷图标是在 manifest 文件中定义的。

- 分享

  1. 可以实现直接分享整个 PWA app
  2. 分享 link
     ![](http://blog-bed.oss-cn-beijing.aliyuncs.com/webapp/share-link.png)
  3. 分享不仅可以从 PWA 开始，还可以让 PWA 作为分享的目标
     ![](http://blog-bed.oss-cn-beijing.aliyuncs.com/webapp/share-to-pwa.png)

  分享通过本地的操作系统进行的。

- [自定义 schemes 或预定义 schemes](https://diek.us/pwinter/pwa-palette.html)

  ```json
  //manifest.json
  {
    "protocol_handlers": [
      {
        "protocol": "web+pwinter",
        "url": "index.html?colors=%s"
      }
    ]
  }
  ```

  ![](http://blog-bed.oss-cn-beijing.aliyuncs.com/webapp/custom-protocol.png)

- file system access API

### 参考文档

- [Progressive_web_apps](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
- [progressive-web-apps](https://web.dev/progressive-web-apps/)
- [code-21-big-stonking-post](https://weblog.200ok.com.au/2021/09/code-21-big-stonking-post.html)
- [publish-your-pwa-to-the-ios-app-store/](https://blog.pwabuilder.com/posts/publish-your-pwa-to-the-ios-app-store/)
