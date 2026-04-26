# 2.1.1 前端三剑客：HTML、CSS、JavaScript

> **所属模块**：模块二 · 前端开发核心概念  
> **学习难度**：★★☆☆☆（入门级）  
> **建议学时**：2.5小时  
> **前置知识**：[1.1.3 典型产品架构分层](../module01/1-1-3-典型产品架构分层.md)  
> **后续学习**：[2.1.2 DOM与页面渲染机制](2-1-2-DOM与页面渲染机制.md) | [2.2.1 React组件化思维](2-2-1-React组件化思维.md)

---

## 🎯 学习目标

完成本节学习后，你将能够：
1. 理解HTML、CSS、JavaScript各自的核心职责和协作关系
2. 读懂简单的HTML页面结构，识别关键标签
3. 理解CSS选择器、盒模型和布局的基本原理
4. 了解JavaScript如何为页面添加交互能力

---

## 📖 核心内容

### 一、前端三剑客的关系

**通俗比喻**：建造一栋房子
- **HTML** = 钢筋骨架（决定房子有几个房间、门窗在哪里）
- **CSS** = 装修装饰（决定墙壁颜色、家具风格、灯光氛围）
- **JavaScript** = 智能家电（决定按下开关灯会亮、门锁会开）

### 二、HTML（超文本标记语言）

**定义**：HTML（HyperText Markup Language）是用于描述网页结构和内容的标记语言。

**核心概念**：

| 概念 | 说明 | 示例 |
|------|------|------|
| **标签（Tag）** | HTML的基本单元，用尖括号包裹 | `<p>你好</p>` |
| **元素（Element）** | 标签+内容 | `<h1>标题</h1>` |
| **属性（Attribute）** | 给标签添加额外信息 | `<a href="url">链接</a>` |
| **嵌套** | 标签可以包含其他标签 | `<div><p>文字</p></div>` |

**常用标签分类**：

| 类别 | 标签 | 用途 |
|------|------|------|
| 结构标签 | `<html>`, `<head>`, `<body>` | 页面基本结构 |
| 文本标签 | `<h1>`-`<h6>`, `<p>`, `<span>` | 标题、段落、行内文字 |
| 链接标签 | `<a>` | 超链接 |
| 图片标签 | `<img>` | 插入图片 |
| 列表标签 | `<ul>`, `<ol>`, `<li>` | 无序列表、有序列表 |
| 表单标签 | `<form>`, `<input>`, `<button>` | 用户输入 |
| 容器标签 | `<div>`, `<section>` | 包裹和组织内容 |

**HTML页面基本结构**：

```html
<!DOCTYPE html>
<html>
<head>
    <title>页面标题</title>
    <meta charset="UTF-8">
</head>
<body>
    <h1>主标题</h1>
    <p>这是一段文字。</p>
    <a href="https://example.com">点击跳转</a>
</body>
</html>
```

### 三、CSS（层叠样式表）

**定义**：CSS（Cascading Style Sheets）是用于控制网页外观和布局的样式语言。

**核心概念**：

| 概念 | 说明 | 示例 |
|------|------|------|
| **选择器** | 选中要设置样式的元素 | `p { color: red; }` |
| **属性** | 要设置的样式 | `color`, `font-size`, `margin` |
| **值** | 样式的具体数值 | `red`, `16px`, `center` |
| **盒模型** | 每个元素都是一个矩形盒子 | content + padding + border + margin |

**CSS选择器类型**：

| 选择器 | 语法 | 说明 |
|--------|------|------|
| 元素选择器 | `p` | 选中所有p标签 |
| 类选择器 | `.title` | 选中class="title"的元素 |
| ID选择器 | `#header` | 选中id="header"的元素 |
| 后代选择器 | `div p` | 选中div内的所有p |
| 伪类选择器 | `a:hover` | 鼠标悬停时的a标签 |

**CSS盒模型**：

```
┌─────────────────────────────────┐
│           margin（外边距）          │
│  ┌───────────────────────────┐  │
│  │       border（边框）         │  │
│  │  ┌─────────────────────┐  │  │
│  │  │  padding（内边距）     │  │  │
│  │  │  ┌───────────────┐  │  │  │
│  │  │  │   content      │  │  │  │
│  │  │  │   （内容）       │  │  │  │
│  │  │  └───────────────┘  │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### 四、JavaScript（脚本语言）

**定义**：JavaScript是用于为网页添加交互功能的编程语言。

**核心概念**：

| 概念 | 说明 | 示例 |
|------|------|------|
| **变量** | 存储数据的容器 | `let name = "张三";` |
| **函数** | 可复用的代码块 | `function sayHello() { ... }` |
| **事件** | 用户触发的动作 | 点击、鼠标移动、键盘输入 |
| **DOM操作** | 修改页面元素 | `document.getElementById("title").textContent = "新标题";` |
| **条件判断** | 根据不同情况执行不同代码 | `if (isLoggedIn) { ... } else { ... }` |
| **循环** | 重复执行代码 | `for (let i = 0; i < 10; i++) { ... }` |

**JavaScript常见交互场景**：

| 场景 | JavaScript的作用 |
|------|----------------|
| 表单验证 | 检查用户输入是否符合要求 |
| 弹窗提示 | 显示确认框、提示框 |
| 动态加载 | 不刷新页面获取新内容 |
| 动画效果 | 平滑滚动、淡入淡出 |
| 数据交互 | 向服务器发送请求、接收响应 |

### 五、三者协作示例

```html
<!-- HTML：定义结构 -->
<button id="submitBtn" class="btn-primary">提交</button>

<!-- CSS：定义样式 -->
<style>
.btn-primary {
    background-color: #1890ff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
}
.btn-primary:hover {
    background-color: #40a9ff;
}
</style>

<!-- JavaScript：定义交互 -->
<script>
document.getElementById("submitBtn").addEventListener("click", function() {
    alert("提交成功！");
});
</script>
```

---

## 📦 案例分析

### 案例一：淘宝商品详情页的三剑客拆解

| 层 | 内容 | 实现方式 |
|----|------|---------|
| HTML | 商品标题、图片、价格、规格选择、购买按钮 | `<h1>`, `<img>`, `<span>`, `<select>`, `<button>` |
| CSS | 价格红色高亮、按钮渐变背景、图片圆角 | `.price { color: #ff4400; }`, `border-radius: 8px` |
| JavaScript | 切换商品图片、数量加减、加入购物车动画 | `addEventListener`, DOM操作, CSS动画 |

### 案例二：登录页面的三剑客协作

**HTML**：提供输入框和按钮  
**CSS**：美化表单，添加聚焦效果  
**JavaScript**：验证输入、提交表单、显示错误提示

---

## 💡 产品经理视角的关键思考

- 当开发说"这个效果CSS做不到"时，可能需要用JavaScript或换方案
- HTML结构决定了页面的语义化和SEO效果
- CSS改动通常风险低，JavaScript改动需要更多测试

---

## 📝 思考问题

1. 如果一个页面只有HTML没有CSS，会是什么样子？
2. CSS中的"层叠"是什么意思？多个样式冲突时以哪个为准？
3. 为什么说JavaScript是"脚本语言"而不是"编程语言"？

---

## 📚 扩展阅读

- MDN Web Docs：[HTML入门](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
- MDN Web Docs：[CSS入门](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
- MDN Web Docs：[JavaScript入门](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

---

## 🔗 相关链接

- [返回总目录](../README.md)
- [上一节：1.2.4 产品需求文档的标准结构与写法](../module01/1-2-4-产品需求文档的标准结构与写法.md)
- [下一节：2.1.2 DOM与页面渲染机制](2-1-2-DOM与页面渲染机制.md)
- [相关：1.1.3 典型产品架构分层](../module01/1-1-3-典型产品架构分层.md)

---

*本教程为《AI编程时代产品经理入门》系列教材的一部分。*
