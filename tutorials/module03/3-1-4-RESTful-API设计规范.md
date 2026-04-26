# 3.1.4 RESTful API设计规范

> **所属模块**：模块三 · 后端开发核心概念
> **学习难度**：★★★☆☆（进阶级）
> **建议学时**：3小时
> **前置知识**：[3.1.3 HTTP协议基础](3-1-3-HTTP协议基础.md)
> **后续学习**：[3.2.1 Java Spring Boot](3-2-1-Java-Spring-Boot.md)

---

## 学习目标

1. 理解RESTful API的核心理念和设计原则
2. 掌握RESTful URL设计规范
3. 能够阅读和理解API接口文档
4. 了解API设计中的常见陷阱

---

## 📖 核心内容

### 一、什么是RESTful API？

**定义**：REST（Representational State Transfer，表述性状态转移）是一种软件架构风格，用于设计网络应用程序的API。遵循REST风格的API被称为RESTful API。

**通俗比喻**：RESTful API就像一本标准化的"菜单"——每道菜（资源）有统一的命名规则，点菜方式（HTTP方法）有明确定义，上菜格式（JSON）统一规范。任何厨师（后端）和顾客（前端）只要遵循这个标准，就能顺畅沟通。

### 二、RESTful的核心原则

| 原则 | 含义 | 产品经理关注点 |
|------|------|----------------|
| **资源导向** | URL代表资源（名词），而非动作（动词） | `/users` 而非 `/getUsers` |
| **统一接口** | 使用标准HTTP方法操作资源 | GET查、POST增、PUT改、DELETE删 |
| **无状态** | 每次请求包含完整信息，服务器不记录会话 | 每次请求都要带认证信息 |
| **可缓存** | 响应可标注是否可缓存 | 提升性能，减少服务器压力 |

### 三、URL设计规范

**核心规则：URL中只使用名词，不使用动词**

| 错误示例 | 正确示例 | 说明 |
|----------|----------|------|
| `/getUser` | `GET /users/1` | 获取单个用户 |
| `/createUser` | `POST /users` | 创建用户 |
| `/updateUser` | `PUT /users/1` | 更新用户 |
| `/deleteUser` | `DELETE /users/1` | 删除用户 |
| `/getAllProducts` | `GET /products` | 获取所有产品 |

**层级资源表示**：
- `/users/1/orders` —— 获取用户1的所有订单
- `/users/1/orders/5` —— 获取用户1的第5号订单
- `/products/3/reviews` —— 获取产品3的所有评价

**常见操作映射表**：

| 操作 | HTTP方法 | URL | 状态码 |
|------|----------|-----|--------|
| 获取用户列表 | GET | `/users` | 200 |
| 获取单个用户 | GET | `/users/{id}` | 200 / 404 |
| 创建用户 | POST | `/users` | 201 |
| 更新用户 | PUT | `/users/{id}` | 200 |
| 删除用户 | DELETE | `/users/{id}` | 204 |
| 搜索用户 | GET | `/users?name=张三` | 200 |

### 四、请求与响应格式

**统一使用JSON格式**：

**请求示例（创建用户）**：
```json
POST /api/v1/users
Content-Type: application/json

{
  "name": "王五",
  "email": "wangwu@example.com",
  "role": "admin"
}
```

**响应示例（成功）**：
```json
{
  "code": 200,
  "message": "success",
  "data": {
    "id": 1,
    "name": "王五",
    "email": "wangwu@example.com",
    "created_at": "2024-01-15T10:30:00Z"
  }
}
```

**响应示例（失败）**：
```json
{
  "code": 400,
  "message": "邮箱格式不正确",
  "errors": [
    {
      "field": "email",
      "message": "请输入有效的邮箱地址"
    }
  ]
}
```

### 五、API版本管理

随着产品迭代，API需要升级版本。常见版本管理方式：

| 方式 | 示例 | 优点 | 缺点 |
|------|------|------|------|
| **URL路径版本** | `/api/v1/users` | 最直观，最常用 | URL中包含版本信息 |
| **请求头版本** | `Accept: application/vnd.api+json; version=1` | URL干净 | 不够直观 |
| **查询参数版本** | `/api/users?version=1` | 灵活 | 容易被忽略 |

**推荐**：使用URL路径版本管理，清晰明确，便于调试。

### 六、分页与过滤

**分页参数**：
```
GET /api/v1/users?page=1&size=20
```

**响应格式**：
```json
{
  "code": 200,
  "data": {
    "items": [...],
    "pagination": {
      "page": 1,
      "size": 20,
      "total": 150,
      "total_pages": 8
    }
  }
}
```

**过滤参数**：
```
GET /api/v1/users?status=active&role=admin&created_after=2024-01-01
```

### 七、常见设计陷阱

| 陷阱 | 说明 | 正确做法 |
|------|------|----------|
| **URL中使用动词** | `/deleteUser/1` | `DELETE /users/1` |
| **复数名词不一致** | `/user/1` 和 `/users` | 统一使用复数：`/users` |
| **过度嵌套** | `/users/1/orders/5/items/3/reviews` | 最多2-3层，超过则独立 |
| **状态码滥用** | 所有请求都返回200 | 正确使用201、400、404等 |
| **缺少错误信息** | 只返回 `{"error": "failed"}` | 返回具体错误字段和原因 |

---

## 案例分析

### 案例一：设计一个"博客系统"的API

**需求**：设计博客系统的核心API，包括文章管理、评论功能。

**API设计**：

| 操作 | 方法 | URL | 说明 |
|------|------|-----|------|
| 获取文章列表 | GET | `/api/v1/articles` | 支持分页、搜索、分类过滤 |
| 获取单篇文章 | GET | `/api/v1/articles/{id}` | 包含文章内容、作者信息 |
| 创建文章 | POST | `/api/v1/articles` | 需要登录，返回创建的文章 |
| 更新文章 | PUT | `/api/v1/articles/{id}` | 仅作者可操作 |
| 删除文章 | DELETE | `/api/v1/articles/{id}` | 仅作者/管理员可操作 |
| 获取文章评论 | GET | `/api/v1/articles/{id}/comments` | 支持分页 |
| 发表论 | POST | `/api/v1/articles/{id}/comments` | 需要登录 |

### 案例二：从非RESTful改造为RESTful

**改造前（混乱的API）**：
```
GET  /api/getUserList
POST /api/addUser
POST /api/updateUserInfo
GET  /api/delUser?id=5
POST /api/searchUser?keyword=张三
```

**改造后（RESTful）**：
```
GET    /api/v1/users                ← 获取用户列表
POST   /api/v1/users                ← 创建用户
PUT    /api/v1/users/{id}           ← 更新用户
DELETE /api/v1/users/{id}           ← 删除用户
GET    /api/v1/users?keyword=张三   ← 搜索用户（用GET+查询参数）
```

**改造收益**：
- URL更简洁直观
- 符合行业标准，新开发能快速上手
- 支持统一的权限控制和日志记录
- 便于生成自动化文档

---

## 产品经理视角的关键思考

- **API是前后端的"契约"**：好的API设计让前后端可以并行开发。产品经理在写PRD时应该同步思考"前端需要哪些数据"，协助设计API。
- **关注字段设计**：产品经理需要明确每个API返回哪些字段、哪些是必填项、数据格式是什么（日期、金额、状态枚举等）。
- **版本兼容是产品决策**：升级API时是否兼容旧版本，直接影响老用户能否正常使用。这个决策需要产品经理参与，不能纯技术决定。
- **错误提示影响用户体验**：API返回的错误信息直接决定前端能向用户展示什么提示。在PRD中要明确各种异常场景的交互文案。

---

## 思考问题

1. 如果产品需要实现"批量删除用户"功能，用RESTful风格应该如何设计API？
2. 为什么RESTful要求URL中使用名词而不是动词？这样做有什么好处？
3. 当你的产品用户从1000人增长到100万人时，哪些API设计问题会暴露出来？你会如何提前规划？

---

## 相关链接

- [上一节：3.1.3 HTTP协议基础](3-1-3-HTTP协议基础.md)
- [下一节：3.2.1 Java Spring Boot](3-2-1-Java-Spring-Boot.md)
- [返回总目录](../README.md)

---

*本教程为《AI编程时代产品经理入门》系列教材的一部分。*
