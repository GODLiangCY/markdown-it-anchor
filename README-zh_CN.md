# markdown-it-anchor [![npm version](http://img.shields.io/npm/v/markdown-it-anchor.svg?style=flat-square)](https://www.npmjs.org/package/markdown-it-anchor)

> 中文版翻译基于 version 8.6.7。
> 一个 markdown-it 插件，将 `id` 属性添加到标题和可选的永久链接。

[markdown-it]: https://github.com/markdown-it/markdown-it

中文 | [English](./README.md)

## 概述

本插件将一个 `id` 属性添加到了标题中，例如将`## Foo`转换成
`<h2 id="foo">Foo</h2>`。

可选地，它也可以包括[永久链接](#永久链接)，例如`<h2 id="foo"><a class="header-anchor" href="#foo">Foo</a></h2>`以及一堆其他变体！

* [**使用方式**](#使用方式)
* [用户友好的 URLs](#用户友好的 URLs)
* [手动设置 `id` 属性](#手动设置 `id` 属性)
* [兼容的目录插件](#兼容的目录插件)
* [从 HTML 块中解析标题](#从 HTML 块中解析标题)
* [浏览器示例](#浏览器示例)
* [**永久链接**](#永久链接)
  * [Header link](#header-link)
  * [Link after header](#link-after-header)
  * [Link inside header](#link-inside-header)
  * [ARIA hidden](#aria-hidden)
  * [Custom permalink](#custom-permalink)
* [调试](#调试)
* [开发](#开发)

## 使用方式

```js
const md = require('markdown-it')()
  .use(require('markdown-it-anchor'), opts)
```

这里是demo [demo as JSFiddle](https://jsfiddle.net/9ukc8dy6/).

其中 `opts` 对象可能包含:

名称                   | 描述                                                    | 默认值
-----------------------|----------------------------------------------------------------|-----------------------------------
`level`                | 若传入数字，代表最少包含的渲染层级；若传入一个数组，则会渲染数组中选定的层级 | 1
`slugify`              | 生成有效url的自定义函数 function.                               | 详见 [`index.js`](index.js)
`uniqueSlugStartIndex` | 使重复锚点变得唯一的新增起始索引        | 1
`permalink`            | 是否在标题旁加入永久链接                     | `false`
`renderPermalink`      | 自定义永久链接渲染函数                         | 详见 [`index.js`](index.js)
`permalinkClass`       | 生成永久链接的 class 名称.                             | `header-anchor`
`permalinkSpace`       | 标题和锚点之间放置空格  | `true`
`permalinkSymbol`      | 永久链接的符号.                            | `¶`
`permalinkBefore`      | 将永久链接放在标题的前面.                          | `false`
`permalinkHref`        | 自定义渲染 `href` 函数.                  | 详见 [`index.js`](index.js)
`permalinkAttrs`       | 自定义标题渲染函数.              | 详见 [`index.js`](index.js)
`callback`             | 渲染后的 callback 函数.                    | `undefined`

`renderPermalink` 功能函数需要一个slug，格式和上面的格式一样，其余的参数和通常 markdown-it 的渲染函数的参数一致。

所有比 `level` 大的标题都会渲染出一个被 slugify 函数处理后的`id` 属性 。
`level` 可能是一个数组代表渲染的标题层级，比如`[2, 3]`是要只要渲染层级2和层级3 。

如果开启 `permalink` , 将会在标题旁添加链接符号 `¶` 

你可能也想使用链接符号 [link symbol](http://graphemica.com/🔗) 作为`permalinkSymbol`, 或者你喜欢的网站的符号.

`callback` 是一个将在渲染`token` and  `info` 结束后被调用的函数。 `info`对象拥有`title` and `slug` 属性在 token 块中，`slug`将会用在identifier 中。 

## 用户友好的 URLs

自从 `v5.0.0` 版本, `markdown-it-anchor` 抛弃 `string` 为了保持他的核心功能的纯粹和安全。
然而，寻求向后兼容的老用户可能需要旧的slugify：


```sh
$ npm i -S string
```

```js
const string = require('string')
const legacySlugify = s => string(s).slugify().toString()

const md = require('markdown-it')()
const anchor = require('markdown-it-anchor', {
	slugify: legacySlugify
})
```

## 手动设置 `id` 属性

## 兼容的目录插件

找寻自动生成目录的方法?
推荐使用[markdown-it-toc-done-right](https://www.npmjs.com/package/markdown-it-toc-done-right) 它是这个插件好伴侣

## 从 HTML 块中解析标题

## 浏览器示例

## 永久链接

### Header link

### Link after header

### Link inside header

### ARIA hidden

### Custom permalink

## 调试

## 开发
