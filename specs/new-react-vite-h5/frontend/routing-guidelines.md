# 路由规范

> 约定 **路由配置文件位置**、**声明方式** 及 **元信息（meta）语义**，便于权限、布局、埋点与面包屑等与路由对齐。

---

## 概述

<!--
请说明项目采用的路由方案：
- React Router v6+（createBrowserRouter / RouterProvider）
- 或 Vite 插件式文件路由等
-->

（待团队补充：技术选型与入口文件，如 `src/router/index.tsx`）

---

## 路由写在哪里

| 类型 | 路径 / 文件（示例占位） | 说明 |
|------|------------------------|------|
| 路由表 / 配置聚合 | `<!-- 例：src/router/routes.tsx -->` | 导出 `RouteObject[]` 或等价结构，**单一事实来源** |
| 布局与嵌套路由 | `<!-- 例：src/layouts/AppLayout.tsx -->` | `Outlet` 包裹业务页，公共壳层 |
| 懒加载页面 | `<!-- lazy(() => import('@/pages/...')) -->` | 与代码分割策略一致 |

（待团队补充：实际文件路径）

---

## 怎样写（结构约定）

<!--
以下为 React Router v6 风格示例占位，请替换为团队真实写法。
-->

**推荐**：

- 使用 **嵌套路由** 表达「布局 → 子页」；叶子节点为具体页面组件。
- **路径**使用无前导歧义的约定（如全小写、kebab-case），与菜单/文档一致。
- **索引路由**（`index: true`）用于默认子页。

```tsx
// 示例占位 — 请以项目为准替换
const routes: RouteObject[] = [
  {
    path: '/',
    element: <AppLayout />,
    children: [
      { index: true, element: <HomePage /> },
      { path: 'orders', element: <OrderListPage /> },
    ],
  },
];
```

（待团队补充：真实路由片段）

---

## 路由属性（meta）与功能对应

请在项目中统一 **meta 字段含义**，下表为常见约定模板，**请按需增删并写死团队词典**。

| 属性（示例） | 含义 / 用途 |
|--------------|-------------|
| `title` | 页面标题（Tab / 浏览器标题），可被 i18n 覆盖 |
| `requiresAuth` | 是否必须先登录；`false` 用于登录页等 |
| `roles` / `permissions` | 访问所需角色或权限码，供路由守卫或菜单过滤 |
| `layout` | 使用哪套布局（如 `main` / `blank`），或是否隐藏侧栏 |
| `keepAlive` | 是否缓存路由级状态（若项目接了 Keep-Alive 方案） |
| `breadcrumb` | 面包屑展示名或自定义层级 |
| `analyticsName` | 埋点页面名，与产品字典对齐 |

<!--
若使用 data router，说明 meta 如何从 loader / 静态配置注入。
-->

（待团队补充：项目实际 `meta` 类型定义与读取位置）

---

## 导航与参数

- **声明式导航**：`<Link to="...">` / `<NavLink>`；**命令式**：`useNavigate()`。
- **URL 参数**：`useParams` 用于路径参数；`useSearchParams` 用于查询串（列表筛选、页码等宜可分享）。

（待团队补充：是否禁止某些编码方式）

---

## 禁止项与常见错误

| 禁止 | 原因 |
|------|------|
| 多处维护互不同步的路由表 | 菜单、权限、面包屑漂移 |
| 在业务组件内硬编码大量 `navigate('/...')` 字符串 | 重构路径时难追溯；建议常量或路由工厂 |
| 忽略无权限时的重定向与回退 | 体验与安全问题 |

（待团队补充）

---

## 延伸阅读

- [Directory Structure](./directory-structure.md)
- [Shared Components Catalog](./shared-components-catalog.md) — 列表页与布局类能力的组件选型
