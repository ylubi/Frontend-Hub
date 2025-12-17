# HTML 基础概念

## 目录

- [什么是 HTML](#什么是-html)
- [HTML 文档结构](#html-文档结构)
- [HTML 元素与标签](#html-元素与标签)
- [HTML 属性](#html-属性)
- [语义化 HTML](#语义化-html)
- [HTML 版本历史](#html-版本历史)
- [最佳实践](#最佳实践)

## 什么是 HTML

HTML（HyperText Markup Language）是超文本标记语言，是用于创建网页的标准标记语言。它描述了网页的结构，浏览器根据 HTML 代码来渲染页面内容。

HTML 不是编程语言，而是一种标记语言，它使用标记标签来描述网页内容。

## HTML 文档结构

一个标准的 HTML 文档包含以下基本结构：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>页面标题</title>
</head>
<body>
    <!-- 页面内容 -->
    <h1>这是一个标题</h1>
    <p>这是一个段落。</p>
</body>
</html>
```

### 主要组成部分

- `<!DOCTYPE html>`：文档类型声明，告诉浏览器这是一个 HTML5 文档
- `<html>`：根元素，包含整个 HTML 文档
- `<head>`：包含文档的元数据，如字符集、视口设置、标题等
- `<body>`：包含页面的可见内容

## HTML 元素与标签

HTML 元素是由开始标签、内容和结束标签组成的：

```html
<标签名>内容</标签名>
```

有些 HTML 元素是空元素，它们没有结束标签，例如：

```html
<br> <!-- 换行 -->
<img src="image.jpg" alt="图片描述"> <!-- 图片 -->
<input type="text" placeholder="输入文本"> <!-- 输入框 -->
```

### 常用 HTML 元素

- **标题元素**：`<h1>` 到 `<h6>`
- **段落元素**：`<p>`
- **链接元素**：`<a>`
- **列表元素**：`<ul>`, `<ol>`, `<li>`
- **表格元素**：`<table>`, `<tr>`, `<td>`
- **表单元素**：`<form>`, `<input>`, `<select>`, `<textarea>`
- **媒体元素**：`<img>`, `<audio>`, `<video>`

## HTML 属性

HTML 属性提供了关于 HTML 元素的额外信息，它们总是在开始标签中指定，通常以名称/值对的形式出现：

```html
<标签名 属性名="属性值">内容</标签名>
```

### 常用属性

- `id`：唯一标识元素
- `class`：为元素指定一个或多个类名
- `src`：指定资源的 URL（用于 `<img>`, `<script>`, `<link>` 等）
- `href`：指定链接的目标 URL（用于 `<a>`, `<link>` 等）
- `alt`：为图像提供替代文本
- `title`：为元素提供额外信息（通常显示为工具提示）
- `style`：内联 CSS 样式

## 语义化 HTML

语义化 HTML 是指使用恰当的 HTML 元素来表示内容的含义，而不仅仅是为了展示效果。

### 语义化标签的优点

1. 提高代码的可读性和可维护性
2. 有助于搜索引擎优化（SEO）
3. 提高可访问性，有利于屏幕阅读器等辅助技术
4. 更好地支持未来的 HTML 版本

### 常用语义化标签

- `<header>`：页面或区块的头部
- `<nav>`：导航链接区域
- `<main>`：页面的主要内容
- `<section>`：文档中的区块或章节
- `<article>`：独立的、自包含的内容
- `<aside>`：侧边栏或相关内容
- `<footer>`：页面或区块的底部
- `<figure>`：独立的媒体内容，如图片、图表等
- `<figcaption>`：媒体内容的说明文字

## HTML 版本历史

1. **HTML 1.0**：1993 年，第一个 HTML 规范
2. **HTML 2.0**：1995 年，标准化的 HTML 规范
3. **HTML 3.2**：1997 年，引入了表格、表单等功能
4. **HTML 4.01**：1999 年，引入了样式表、脚本等功能
5. **XHTML 1.0**：2000 年，基于 XML 的 HTML 版本
6. **HTML5**：2014 年，引入了许多新特性，如语义化标签、Canvas、SVG 等

## 最佳实践

1. **使用语义化标签**：选择合适的标签来表示内容的含义
2. **保持代码简洁**：避免不必要的嵌套和冗余标签
3. **使用正确的缩进**：提高代码的可读性
4. **添加适当的注释**：解释复杂的代码结构
5. **使用外部资源**：将 CSS 和 JavaScript 放在外部文件中
6. **优化图像**：使用适当的图像格式和大小
7. **确保可访问性**：添加 alt 文本、使用 ARIA 属性等
8. **验证 HTML**：使用 W3C 验证器检查 HTML 代码的有效性

## 参考资源

- [MDN Web Docs - HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
- [W3Schools - HTML Tutorial](https://www.w3schools.com/html/)
- [HTML 规范](https://html.spec.whatwg.org/)
