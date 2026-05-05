# API 规范

> 约定 **HTTP 请求封装位置**、**模块内接口定义方式** 与 **业务代码中的调用方式**，避免重复造轮子或风格分裂。

---

## 概述

<!--
请按项目实际情况替换以下内容：
- 使用的请求库（fetch / axios / ky / 自研 SDK 等）
- 是否统一经由网关、是否带鉴权头、错误码约定
-->

（待团队补充：基座能力、环境与 Base URL、鉴权与错误处理策略）

---

## 接口定义写在哪儿

| 层级 | 推荐路径 / 约定 | 职责 |
|------|-----------------|------|
| 全局 HTTP 客户端 / 拦截器 | `<!-- 例：src/services/http.ts 或 src/api/client.ts -->` | 实例化、BaseURL、超时、Token、统一错误与重试 |
| 按业务域拆分的接口模块 | `<!-- 例：src/api/modules/user.ts -->` | 与后端资源一一对应的 `request` 封装，**不写 UI 逻辑** |
| 与页面强绑定的请求（可选） | `<!-- 例：src/pages/xxx/api.ts -->` | 仅该页面使用的薄封装，仍应复用全局 client |

**原则**：

- 请求路径、方法、Query/Body 形状集中在 **API 模块**；组件 / Hook 只依赖 **有类型的函数**，不直接散落 `fetch` URL。
- 若团队有 **OpenAPI / Orval** 等生成代码，在此说明生成物目录与 **禁止手改** 范围。

（待团队补充：实际目录与命名）

---

## 如何调用（推荐流程）

1. **在 API 模块**导出形如 `getXxx`、`createXxx` 的函数（返回 `Promise` 或可组合数据层类型）。
2. **在组件或自定义 Hook** 中调用上述函数；列表/表单提交等可配合项目约定的数据获取方案（见 [State Management](./state-management.md)、[Hook Guidelines](./hook-guidelines.md)）。
3. **错误与 Loading**：在调用层或全局拦截器中统一处理；页面层仅处理「需用户感知的提示」。

<!--
示例占位（请替换为真实代码）：

```ts
// src/api/modules/order.ts
import { http } from '@/services/http';

export type OrderListParams = { page: number; pageSize: number; keyword?: string };
export const fetchOrderList = (params: OrderListParams) =>
  http.get<OrderRowDto[]>('/orders', { params });
```

```tsx
// 在 Hook 或组件中
const { data, isLoading } = useQuery({
  queryKey: ['orders', params],
  queryFn: () => fetchOrderList(params),
});
```
-->

（待团队补充：完整最小示例与项目所用数据获取方式）

---

## 类型与约定

- **请求/响应 DTO**：与后端契约对齐；必要时使用 `zod` / 手写类型标注。
- **命名**：动词 + 资源名（`fetch` / `create` / `update` / `delete`），避免与 React 组件同名。
- **幂等与副作用**：`GET` 只读；变更类接口在文档中说明是否需要防重复提交。

（待团队补充：DTO 放置路径、是否使用严格模式）

---

## 禁止项与常见错误

| 禁止 | 原因 |
|------|------|
| 在 JSX 内直接写长 URL + `fetch` | 难测试、无统一鉴权/错误处理 |
| 同一接口在多个文件复制粘贴参数拼装 | 变更后端时遗漏 |
| 把接口层写在 `components` 内部且无法复用 | 边界混乱 |

（待团队补充：团队真实踩坑）

---

## 延伸阅读

- [Directory Structure](./directory-structure.md) — 模块与 `api` 目录在整体结构中的位置。
