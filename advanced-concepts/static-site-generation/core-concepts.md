# 静态站点生成 (SSG) 核心概念

## 1. SSG 基础

### 1.1 什么是 SSG

静态站点生成（Static Site Generation）是一种前端构建技术，在构建时预渲染所有页面为静态 HTML 文件，然后将这些文件部署到服务器。用户访问时，服务器直接返回预渲染的 HTML 文件，无需在运行时进行渲染。

### 1.2 SSG 与其他渲染方式对比

| 渲染方式 | 渲染时机 | 优势 | 劣势 | 适用场景 |
|---------|---------|------|------|----------|
| SSG | 构建时 | 极快的首屏加载速度，优秀的 SEO 表现，低成本部署 | 内容更新需要重新构建，不适合频繁更新的内容 | 博客、文档站、营销页面、产品展示 |
| SSR | 运行时 | 良好的 SEO 表现，支持动态内容 | 服务器压力大，首屏加载速度中等 | 电商网站、新闻网站、社交平台 |
| CSR | 客户端 | 良好的交互体验，前后端分离 | SEO 表现差，首屏加载速度慢 | 单页应用、后台管理系统、交互复杂的应用 |
| ISR | 构建时 + 运行时 | 结合 SSG 和 SSR 的优势，支持增量更新 | 实现复杂，需要缓存策略 | 内容频繁更新但流量不均的站点 |

## 2. SSG 工作原理

### 2.1 核心工作流程

1. **数据获取**：从 API、数据库、Markdown 文件等数据源获取内容
2. **模板渲染**：使用模板引擎将数据与模板结合，生成 HTML
3. **静态资源处理**：处理 CSS、JavaScript、图片等静态资源
4. **构建输出**：生成完整的静态站点文件（HTML、CSS、JS、图片等）
5. **部署**：将生成的静态文件部署到 CDN 或静态托管服务

### 2.2 关键技术点

- **预渲染**：在构建时生成所有页面的 HTML
- **静态资源优化**：压缩、合并、哈希处理等
- **路由生成**：根据配置或文件系统自动生成路由
- **增量构建**：只重新构建变化的页面，提高构建效率

## 3. 主流 SSG 框架

### 3.1 Next.js (React)

Next.js 是基于 React 的全栈框架，支持 SSG、SSR、ISR 等多种渲染方式。

#### 3.1.1 SSG 实现方式

```javascript
// 页面级数据获取 - getStaticProps
export async function getStaticProps() {
  const posts = await fetchPosts();
  return {
    props: {
      posts,
    },
    revalidate: 60, // 可选：ISR，每60秒重新生成
  };
}

// 动态路由生成 - getStaticPaths
export async function getStaticPaths() {
  const posts = await fetchPosts();
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }));
  
  return {
    paths,
    fallback: false, // 或 'blocking' 或 true
  };
}

export default function Blog({ posts }) {
  return (
    <div>
      {posts.map((post) => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.content}</p>
        </article>
      ))}
    </div>
  );
}
```

#### 3.1.2 核心特性

- **自动静态优化**：默认静态化所有页面
- **ISR（增量静态再生）**：支持按需更新页面
- **Image 组件**：自动优化图片加载
- **Font 组件**：优化字体加载
- **Middleware**：支持边缘计算

### 3.2 Nuxt.js (Vue)

Nuxt.js 是基于 Vue.js 的全栈框架，提供 SSG、SSR、SPA 等多种渲染模式。

#### 3.2.1 SSG 实现方式

```javascript
// nuxt.config.js
export default {
  target: 'static', // 启用 SSG 模式
  generate: {
    interval: 2000, // 生成间隔
    fallback: true, // 为动态路由生成 404.html
    routes: ['/extra-route'], // 手动添加路由
  },
};

// pages/blog/_id.vue
<script>
export default {
  async asyncData({ $axios, params }) {
    const post = await $axios.$get(`https://api.example.com/posts/${params.id}`);
    return { post };
  },
};
</script>

<template>
  <div>
    <h1>{{ post.title }}</h1>
    <div v-html="post.content"></div>
  </div>
</template>
```

#### 3.2.2 核心特性

- **零配置 SSG**：简单配置即可启用 SSG
- **自动路由生成**：基于文件系统的路由
- **模块生态**：丰富的官方和社区模块
- **静态站点生成器**：支持生成完全静态的站点

### 3.3 Astro

Astro 是一个新型的静态站点生成器，支持多框架集成（React、Vue、Svelte 等）。

#### 3.3.1 核心概念

- **Astro 组件**：类似 HTML 的组件，默认在服务端渲染
- **群岛架构**：只在需要时激活交互组件
- **混合渲染**：支持 SSG、SSR、ISR 等多种渲染方式

#### 3.3.2 SSG 实现方式

```astro
---
// src/pages/index.astro
// 组件级数据获取
const posts = await Astro.glob('../posts/*.md');
---

<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>My Blog</title>
</head>
<body>
  <h1>My Blog</h1>
  <ul>
    {posts.map((post) => (
      <li key={post.url}>
        <a href={post.url}>{post.frontmatter.title}</a>
        <p>{post.frontmatter.description}</p>
      </li>
    ))}
  </ul>
  
  <!-- 集成 React 组件 -->
  <MyReactComponent client:load />
</body>
</html>
```

#### 3.3.3 核心特性

- **多框架支持**：在同一项目中使用 React、Vue、Svelte 等
- **群岛架构**：减少 JavaScript 体积，提高性能
- **MDX 支持**：直接在 Markdown 中使用组件
- **快速构建**：优化的构建引擎

### 3.4 Hugo

Hugo 是用 Go 语言编写的高性能静态站点生成器，以速度著称。

#### 3.4.1 核心特性

- **极快的构建速度**：即使是大型站点也能在几秒内构建完成
- **灵活的模板系统**：基于 Go 模板
- **丰富的主题生态**：大量现成的主题可用
- **强大的内容管理**：支持多种内容格式

#### 3.4.2 基本使用

```bash
# 创建新站点
hugo new site mysite

# 添加主题
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

# 创建内容
hugo new posts/my-first-post.md

# 构建站点
hugo

# 本地预览
hugo server
```

### 3.5 Gatsby

Gatsby 是基于 React 的静态站点生成器，强调性能和现代 Web 技术。

#### 3.5.1 核心特性

- **GraphQL 数据源**：统一的数据获取层
- **插件生态**：丰富的插件系统
- **图像优化**：自动优化图像
- **渐进式 Web App (PWA)**：内置 PWA 支持

#### 3.5.2 基本使用

```javascript
// gatsby-config.js
module.exports = {
  siteMetadata: {
    title: 'My Gatsby Site',
    description: 'A static site built with Gatsby',
  },
  plugins: [
    'gatsby-plugin-react-helmet',
    'gatsby-plugin-sass',
    {
      resolve: 'gatsby-source-filesystem',
      options: {
        name: 'posts',
        path: `${__dirname}/src/posts`,
      },
    },
    'gatsby-transformer-remark',
  ],
};

// src/pages/index.js
import React from 'react';
import { graphql } from 'gatsby';

const IndexPage = ({ data }) => {
  return (
    <div>
      <h1>My Blog</h1>
      <ul>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <li key={node.id}>
            <h2>{node.frontmatter.title}</h2>
            <p>{node.excerpt}</p>
          </li>
        ))}
      </ul>
    </div>
  );
};

export const query = graphql`
  query { 
    allMarkdownRemark {
      edges {
        node {
          id
          frontmatter {
            title
          }
          excerpt
        }
      }
    }
  }
`;

export default IndexPage;
```

## 4. SSG 最佳实践

### 4.1 性能优化

1. **代码分割**：将代码拆分为更小的块，按需加载
2. **静态资源优化**：
   - 图片压缩和格式优化（WebP、AVIF）
   - 字体优化（预加载、子集化）
   - CSS 和 JavaScript 压缩
3. **CDN 部署**：将静态资源部署到 CDN，提高全球访问速度
4. **缓存策略**：合理设置缓存头，利用浏览器缓存

### 4.2 SEO 优化

1. **语义化 HTML**：使用合适的 HTML 标签
2. **Meta 标签**：优化 title、description、og 标签等
3. **结构化数据**：添加 JSON-LD 结构化数据
4. **XML Sitemap**：生成和提交 sitemap.xml
5. ** robots.txt**：合理配置爬虫规则

### 4.3 内容管理

1. **Markdown 优先**：使用 Markdown 编写内容，便于维护
2. **内容分层**：合理组织内容结构
3. **版本控制**：使用 Git 管理内容和代码
4. **内容预览**：实现本地预览功能，便于内容创作者查看效果

### 4.4 部署策略

1. **自动化部署**：结合 CI/CD 实现自动构建和部署
2. **预览环境**：为每个分支创建预览环境
3. **回滚机制**：确保可以快速回滚到之前的版本
4. **多环境部署**：开发、测试、生产环境分离

## 5. SSG 高级特性

### 5.1 增量静态再生 (ISR)

增量静态再生是 SSG 的扩展，允许在构建后更新特定页面，而无需重新构建整个站点。

```javascript
// Next.js 中的 ISR 配置
export async function getStaticProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
    revalidate: 3600, // 每小时重新生成一次
  };
}
```

### 5.2 动态路由

SSG 支持生成动态路由，基于数据源生成多个页面。

```javascript
// Next.js 中的动态路由
export async function getStaticPaths() {
  const posts = await fetchPosts();
  const paths = posts.map(post => ({
    params: { id: post.id },
  }));
  
  return {
    paths,
    fallback: 'blocking', // 或 false 或 true
  };
}
```

### 5.3 国际化 (i18n)

主流 SSG 框架都支持国际化，允许生成多语言站点。

```javascript
// nuxt.config.js 中的 i18n 配置
export default {
  i18n: {
    locales: ['zh', 'en'],
    defaultLocale: 'zh',
    vueI18n: {
      fallbackLocale: 'zh',
      messages: {
        zh: {
          welcome: '欢迎',
        },
        en: {
          welcome: 'Welcome',
        },
      },
    },
  },
};
```

## 6. SSG 未来趋势

### 6.1 混合渲染

未来的 SSG 框架将更加注重混合渲染，根据页面内容和需求自动选择最佳的渲染方式。

### 6.2 边缘计算

结合边缘计算，在边缘节点进行部分渲染和数据处理，进一步提高性能和降低延迟。

### 6.3 无服务器集成

与无服务器函数结合，实现静态站点的动态功能，如表单提交、用户认证等。

### 6.4 实时内容更新

改进的 ISR 机制，实现更实时的内容更新，同时保持 SSG 的性能优势。

### 6.5 更好的开发者体验

简化配置，提供更友好的开发体验，降低 SSG 的使用门槛。

## 7. 总结

静态站点生成是一种强大的前端构建技术，具有优秀的性能表现和 SEO 效果。随着 Next.js、Nuxt.js、Astro 等框架的发展，SSG 的功能越来越强大，适用场景也越来越广泛。

在选择 SSG 框架时，需要根据项目需求、团队技术栈和性能要求进行综合考虑。无论选择哪种框架，遵循 SSG 最佳实践都能帮助你构建出高性能、易维护的静态站点。

SSG 正在成为现代前端开发的重要组成部分，特别是对于内容驱动的网站和应用，SSG 提供了一种高效、高性能的解决方案。
