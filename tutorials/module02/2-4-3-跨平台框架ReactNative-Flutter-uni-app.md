# 2.4.3 跨平台框架：React Native、Flutter、uni-app

> **所属模块**：模块二 · 前端开发核心概念  
> **学习难度**：★★★☆☆（进阶级）  
> **建议学时**：2.5小时  
> **前置知识**：[2.4.2 混合开发（Hybrid）](2-4-2-混合开发Hybrid.md)  
> **后续学习**：[2.4.4 小程序生态](2-4-4-小程序生态.md) | [3.1.1 什么是后端](../module03/3-1-1-什么是后端.md)

---

## 🎯 学习目标

1. 理解三大跨平台框架的核心差异和适用场景
2. 掌握React Native、Flutter、uni-app的技术特点
3. 能够根据产品特点选择合适的跨平台方案
4. 了解跨平台开发的常见陷阱和优化方向

---

## 📖 核心内容

### 一、什么是跨平台框架？

**定义**：使用一套代码同时生成iOS和Android（甚至更多平台）应用的开发框架。

**通俗比喻**：跨平台框架就像"翻译官"——你用一种语言写代码，它帮你翻译成iOS和Android都能理解的语言。

### 二、三大框架对比

| 维度 | React Native | Flutter | uni-app |
|------|-------------|---------|---------|
| **开发商** | Facebook（Meta） | Google | DCloud（中国） |
| **语言** | JavaScript/React | Dart | Vue/React |
| **渲染方式** | 原生组件映射 | 自绘引擎（Skia） | WebView + 原生桥接 |
| **性能** | 接近原生 | 接近原生 | 中等 |
| **生态** | 丰富 | 快速增长 | 国内丰富 |
| **支持平台** | iOS、Android、Web | iOS、Android、Web、Desktop | iOS、Android、小程序、H5、PC |
| **学习门槛** | 中等（需React基础） | 中等（需学Dart） | 低（会Vue即可） |
| **包体积** | 中 | 较大 | 小 |

### 三、React Native

**核心原理**：将React组件映射为原生组件，实现"Write Once, Run Anywhere"。

```jsx
// React Native代码
import { View, Text, StyleSheet } from 'react-native';

function App() {
    return (
        <View style={styles.container}>
            <Text style={styles.title}>Hello React Native</Text>
        </View>
    );
}
```

**优势**：
- 复用React开发者的技能
- 生态成熟，社区活跃
- Facebook、Instagram等大厂使用验证

**劣势**：
- 性能略低于Flutter（Bridge通信开销）
- 复杂动画和手势处理困难
- 原生模块兼容性偶有问题

**典型产品**：Facebook、Instagram、Airbnb、Discord

### 四、Flutter

**核心原理**：自带渲染引擎（Skia），直接绘制UI，不依赖原生组件。

```dart
// Flutter代码
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            home: Scaffold(
                appBar: AppBar(title: Text('Hello Flutter')),
                body: Center(child: Text('Hello World')),
            ),
        );
    }
}
```

**优势**：
- 性能优异，接近原生
- UI一致性好（不受系统版本影响）
- 热重载开发体验极佳
- Google持续投入，发展迅速

**劣势**：
- 需要学习Dart语言
- 包体积较大
- 第三方库生态不如React Native

**典型产品**：Google Pay、闲鱼、字节跳动部分产品

### 五、uni-app

**核心原理**：基于Vue语法，编译到多个平台（App、小程序、H5）。

```vue
<template>
    <view class="container">
        <text class="title">Hello uni-app</text>
    </view>
</template>
```

**优势**：
- 一套代码发布到7+平台（App、微信/支付宝/百度小程序、H5等）
- 学习成本低（Vue开发者快速上手）
- 国内生态完善，插件市场丰富
- 适合国内多端分发场景

**劣势**：
- App端性能不如React Native和Flutter
- 深度定制需要原生开发能力
- 国际化程度低

**典型产品**：国内大量中小企业App、电商小程序

### 六、选择决策树

```
需要发布到哪些平台？
    ├── 只iOS和Android → React Native 或 Flutter
    │       ├── 团队会React → React Native
    │       ├── 追求极致性能 → Flutter
    │       └── 需要高度定制UI → Flutter
    │
    └── 还需要小程序/H5 → uni-app
            ├── 团队会Vue → uni-app（Vue版）
            └── 团队会React → Taro
```

---

## 📦 案例分析

### 案例一：闲鱼为什么选择Flutter？

**背景**：闲鱼需要重构App，面临React Native和Flutter的选择。

**选择Flutter的原因**：
1. 性能要求高（商品列表、图片流）
2. UI一致性问题（React Native在不同Android版本表现不一致）
3. 团队规模适中，可以学习Dart
4. 阿里巴巴集团内部对Flutter有技术支持

**效果**：开发效率提升30%，性能接近原生，UI一致性大幅改善。

### 案例二：创业公司如何选择？

**场景**：一个3人团队要开发电商App，同时需要微信小程序。

**推荐方案**：uni-app

**理由**：
- 一套代码覆盖App和小程序
- 学习成本低（会Vue即可）
- 快速上线验证
- 后期如果性能不够，可以针对核心页面做原生优化

---

## 💡 产品经理视角的关键思考

- 跨平台方案不是银弹，适合大多数产品，但不适合高性能要求的产品
- 选择框架时要考虑团队技术栈，而非单纯比较技术优劣
- 国内产品如果需要小程序，uni-app/Taro是更好的选择

---

## 📝 思考问题

1. React Native和Flutter的核心差异是什么？为什么Flutter性能更好？
2. 如果你的产品是短视频App，你会选择哪个框架？为什么？
3. 为什么说"跨平台开发节省了开发成本，但可能增加维护成本"？

---

## 🔗 相关链接

- [返回总目录](../README.md)
- [上一节：2.4.2 混合开发（Hybrid）](2-4-2-混合开发Hybrid.md)
- [下一节：2.4.4 小程序生态](2-4-4-小程序生态.md)

---

*本教程为《AI编程时代产品经理入门》系列教材的一部分。*
