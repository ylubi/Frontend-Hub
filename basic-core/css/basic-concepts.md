# CSS 基础概念

## 目录

- [什么是 CSS](#什么是-css)
- [CSS 的作用](#css-的作用)
- [CSS 语法](#css-语法)
- [CSS 选择器](#css-选择器)
- [CSS 盒模型](#css-盒模型)
- [CSS 优先级](#css-优先级)
- [CSS 继承](#css-继承)
- [CSS 单位](#css-单位)
- [CSS 颜色](#css-颜色)
- [最佳实践](#最佳实践)

## 什么是 CSS

CSS（Cascading Style Sheets）是层叠样式表，用于描述 HTML 元素的显示方式。CSS 定义了网页的布局、颜色、字体、间距等视觉样式，使网页更加美观和易于阅读。

CSS 与 HTML 分离，实现了内容与样式的分离，便于维护和修改。

## CSS 的作用

1. **美化网页**：设置字体、颜色、背景、边框等样式
2. **布局控制**：控制元素的位置、大小、间距等
3. **响应式设计**：使网页在不同设备上都能正常显示
4. **动画效果**：添加过渡和动画，增强用户体验
5. **提升可访问性**：通过样式调整，提高网页的可访问性

## CSS 语法

CSS 规则由选择器和声明块组成：

```css
选择器 {
    属性1: 值1;
    属性2: 值2;
    /* 注释 */
}
```

### 示例

```css
h1 {
    color: blue;
    font-size: 24px;
    text-align: center;
}

p {
    color: #333;
    line-height: 1.5;
}
```

## CSS 选择器

CSS 选择器用于选择要应用样式的 HTML 元素。常用的选择器包括：

### 基本选择器

- **元素选择器**：选择指定类型的元素
  ```css
  p { color: red; }
  ```

- **类选择器**：选择带有指定类名的元素
  ```css
  .class-name { color: red; }
  ```

- **ID 选择器**：选择带有指定 ID 的元素
  ```css
  #id-name { color: red; }
  ```

- **通配符选择器**：选择所有元素
  ```css
  * { margin: 0; padding: 0; }
  ```

### 组合选择器

- **后代选择器**：选择指定元素的后代元素
  ```css
  div p { color: red; }
  ```

- **子选择器**：选择指定元素的直接子元素
  ```css
  div > p { color: red; }
  ```

- **相邻兄弟选择器**：选择指定元素的下一个相邻兄弟元素
  ```css
  h1 + p { color: red; }
  ```

- **通用兄弟选择器**：选择指定元素的所有兄弟元素
  ```css
  h1 ~ p { color: red; }
  ```

### 伪类选择器

- **状态伪类**：根据元素的状态选择
  ```css
  a:hover { color: red; }
  input:focus { border-color: blue; }
  ```

- **结构伪类**：根据元素在文档中的位置选择
  ```css
  p:first-child { font-weight: bold; }
  p:last-child { margin-bottom: 0; }
  ```

### 属性选择器

- 根据元素的属性选择
  ```css
  input[type="text"] { width: 200px; }
  a[href^="https"] { color: green; }
  ```

## CSS 盒模型

CSS 盒模型是 CSS 布局的基础，它描述了元素在页面中占据的空间。每个元素都可以看作是一个盒子，包含以下部分：

1. **内容（Content）**：元素的实际内容
2. **内边距（Padding）**：内容与边框之间的空间
3. **边框（Border）**：围绕内容和内边距的边界
4. **外边距（Margin）**：元素与其他元素之间的空间

### 标准盒模型 vs IE 盒模型

- **标准盒模型**：宽度 = 内容宽度
- **IE 盒模型**：宽度 = 内容宽度 + 内边距 + 边框

可以通过 `box-sizing` 属性来设置盒模型：

```css
/* 标准盒模型 */
.box1 {
    box-sizing: content-box;
    width: 200px;
    padding: 20px;
    border: 1px solid black;
    /* 实际宽度 = 200 + 20*2 + 1*2 = 242px */
}

/* IE 盒模型（推荐使用） */
.box2 {
    box-sizing: border-box;
    width: 200px;
    padding: 20px;
    border: 1px solid black;
    /* 实际宽度 = 200px */
}
```

## CSS 优先级

当多个 CSS 规则应用于同一个元素时，优先级决定了哪个规则会被应用。优先级从高到低依次为：

1. **!important**：最高优先级，应谨慎使用
2. **内联样式**：通过 `style` 属性定义的样式
3. **ID 选择器**：`#id`
4. **类选择器**、**伪类选择器**、**属性选择器**：`.class`、`:hover`、`[type="text"]`
5. **元素选择器**、**伪元素选择器**：`p`、`::before`
6. **通配符选择器**：`*`
7. **继承的样式**：最低优先级

### 优先级计算

优先级可以用一个四元组 (a, b, c, d) 来表示：

- a：是否使用 !important（0 或 1）
- b：内联样式的数量
- c：ID 选择器的数量
- d：类选择器、伪类选择器、属性选择器的数量
- e：元素选择器、伪元素选择器的数量

比较优先级时，从左到右依次比较，数值大的优先级高。

## CSS 继承

有些 CSS 属性会从父元素继承到子元素，而有些则不会。

### 可继承的属性

- 字体相关：`font-family`、`font-size`、`font-weight` 等
- 文本相关：`color`、`text-align`、`line-height` 等
- 列表相关：`list-style` 等

### 不可继承的属性

- 盒模型相关：`width`、`height`、`margin`、`padding` 等
- 定位相关：`position`、`top`、`left` 等
- 背景相关：`background`、`border` 等

### 控制继承

- `inherit`：继承父元素的属性值
- `initial`：使用属性的默认值
- `unset`：如果属性可继承则继承，否则使用默认值
- `revert`：恢复属性值到浏览器默认样式或用户样式

## CSS 单位

CSS 支持多种单位，用于表示长度、百分比、角度等。

### 长度单位

- **绝对单位**：
  - `px`：像素
  - `pt`：点（1pt = 1/72 英寸）
  - `in`：英寸
  - `cm`：厘米
  - `mm`：毫米

- **相对单位**：
  - `em`：相对于父元素的字体大小
  - `rem`：相对于根元素的字体大小
  - `vw`：视口宽度的 1%
  - `vh`：视口高度的 1%
  - `vmin`：视口宽度和高度中的较小值的 1%
  - `vmax`：视口宽度和高度中的较大值的 1%
  - `%`：相对于父元素的百分比

### 角度单位

- `deg`：度
- `rad`：弧度
- `grad`：梯度
- `turn`：圈

## CSS 颜色

CSS 支持多种颜色表示方式：

1. **颜色名称**：如 `red`、`blue`、`green` 等
   ```css
   color: red;
   ```

2. **十六进制（Hex）**：以 `#` 开头， followed by 6 个十六进制字符
   ```css
   color: #ff0000; /* 红色 */
   color: #f00; /* 简写，等同于 #ff0000 */
   ```

3. **RGB/RGBA**：
   - RGB：`rgb(红色值, 绿色值, 蓝色值)`，取值范围 0-255
   - RGBA：`rgba(红色值, 绿色值, 蓝色值, 透明度)`，透明度取值范围 0-1
   ```css
   color: rgb(255, 0, 0); /* 红色 */
   color: rgba(255, 0, 0, 0.5); /* 半透明红色 */
   ```

4. **HSL/HSLA**：
   - HSL：`hsl(色相, 饱和度, 亮度)`
     - 色相：0-360 度（红色=0，绿色=120，蓝色=240）
     - 饱和度：0%-100%（0%=灰色，100%=全色）
     - 亮度：0%-100%（0%=黑色，50%=正常，100%=白色）
   - HSLA：`hsla(色相, 饱和度, 亮度, 透明度)`
   ```css
   color: hsl(0, 100%, 50%); /* 红色 */
   color: hsla(0, 100%, 50%, 0.5); /* 半透明红色 */
   ```

## 最佳实践

1. **使用外部 CSS 文件**：将样式与内容分离，便于维护
2. **使用语义化的类名**：类名应反映元素的用途，而非样式
3. **使用缩写属性**：如 `margin`、`padding`、`background` 等
4. **使用 CSS 预处理器**：如 Sass、Less 等，提高开发效率
5. **使用 CSS 变量**：便于主题切换和样式统一管理
6. **避免使用 !important**：除非必要，否则应通过调整选择器优先级来解决样式冲突
7. **使用响应式设计**：使网页在不同设备上都能正常显示
8. **优化 CSS 性能**：减少选择器复杂度，避免不必要的样式规则

## 参考资源

- [MDN Web Docs - CSS](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
- [CSS 参考](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Reference)
- [CSS 选择器参考](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Selectors)
- [CSS 盒模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
