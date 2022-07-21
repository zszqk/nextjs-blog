---
title: 'nextjs学习'
date: '2022-07-21'
---

# Nextjs

## 基本特性

* Pages(页面)

  即根目录下的pages目录，该目录下的文件称为路由页面，文件名即为路径名；例如：如果你创建了一个命名为 `pages/about.js` 的文件并导出（export）一个如下所示的 React 组件，则可以通过 `/about` 路径进行访问。

  Nextjs支持动态路由，例如：如果你创建了一个命名为 `pages/posts/[id].js` 的文件，那么就可以通过 `posts/1`、`posts/2` 等类似的路径进行访问。

  1. 预渲染

     > 静态生成（Static Generation）：HTML在构建时生成，并在每次页面请求（request）时重用
     >
     > 服务端渲染（Server-side Rendering）：在每次页面请求时重新生成HTML

     出于性能考虑，相对服务器端渲染，我们更 **推荐** 使用 **静态生成** 。 CDN 可以在没有额外配置的情况下缓存静态生成的页面以提高性能。但是，在某些情况下，服务器端渲染可能是唯一的选择。

  2. 生成不带数据的静态页面

  3. 需要获取数据的静态生成

     - 页面内容取决于外部数据时：使用` getStaticProps`
     - 页面path（路径）取决于外部数据时：使用` getStaticPaths` 通常伴随使用` getStaticProps`

* 静态页面数据获取

  1. getStaticProps(context)

     > 用于预渲染时获取数据，即Next.js 允许你从同一文件 `export（导出）` 一个名为 `getStaticProps` 的 `async（异步）` 函数。该函数在构建时被调用，并允许你在预渲染时将获取的数据作为 `props` 参数传递给页面。返回值是一个类似{props:xxx}的对象
     >
     > context是一个包含了一些键的对象，例如：**params**（路由参数），preview，previewData，locale，locales，defaultLocale
     >
     > 返回值为一个包含了一些键的对象，例如props（传递给页面），notFound（返回404页面，无论页面是否生成），fallback，redirect（允许重定向到内部或外部资源，目前不允许在构建时重定向，如果重定向在构建时已知，则应将它们添加到 next.config.js 中。）

  2. getStaticPaths

     > 用于创建动态路由，预渲染的页面 **paths（路径）** 取决于外部数据。为了解决这个问题，Next.js 允许你从动态页面中 `export（导出）` 一个名为 `getStaticPaths` 的 `async（异步）` 函数。该函数在构建时被调用，并允许你指定要预渲染的路径。返回值为{paths, fallback:false}，paths为[{id:xx}]

* 服务端数据获取

  每次请求时重新生成HTML页面

  获取数据：getServerSideProps在每次页面请求时都会运行，而在构建时不运行。

* 内置css支持

  Next.js 允许你在 JavaScript 文件中导入（import） CSS 文件。 因为 Next.js 扩展了 JavaScript 中的import概念，才能让这一功能成为可能。

  从 Next.js 9.5.4 版本开始，你可以在应用程序中的任何位置从 node_modules 目录导入（import） CSS 文件了。

  1. 全局样式添加

     * 首先创建一个 pages/_app.js 文件 （如果不存在的话）。 然后 import 样式文件。
     * 以该种形式导入的样式将应用于所有组件和页面

  2. 组件级样式添加

     Next.js 通过 [name].module.css 文件命名约定来支持 CSS 模块 。

     CSS 模块通过自动创建唯一的类名从而将 CSS 限定在局部范围内。 这使您可以在不同文件中使用相同的 CSS 类名，而不必担心冲突。

  3. 对Sass的支持

     Next.js 允许你导入（import）具有 .scss 和 .sass 扩展名的 Sass 文件。 你可以通过 CSS 模块以及 .module.scss 或 .module.sass 扩展名来使用组件及的 Sass。使用之前请确保安装的Sass

  4. Css-in-Js

     内联；style-jsx组件

## blog入门案例

1. 创建基本的项目结构

   > npx create-next-app next-blog

2. 安装必要的包

   > date-fns格式化时间串
   >
   > gray-matter 解析markdown的元数据部分例如title，date等
   >
   > remark 将markdown转换为html
   >
   > remark-html

3. blog的呈现原理——解析指定目录的markdown文件为html到页面通过dangerouslySetInnerHTML进行显示

4. demo地址——https://nextjs-blog-tawny-theta.vercel.app/


​     

​     

​     

