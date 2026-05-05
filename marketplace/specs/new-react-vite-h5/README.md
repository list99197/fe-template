# React + Vite H5 规范（目录说明）

该目录用于作为「React + Vite 移动端 H5」前端脚手架/规范的文档集合（spec scaffold）。它主要由两部分组成：

- `frontend/`：前端开发约定与落地指南（代码组织、组件/Hook/状态、API、路由等）
- `guides/`：偏“思考方式”的共性指南（减少重复造轮子、避免跨层边界缺陷）

---

## 目录结构

```text
new-react-vite-h5/
├─ README.md                     // 你现在看到的目录说明
├─ frontend/                    // 前端落地规范（偏怎么写）
│  ├─ index.md
│  ├─ directory-structure.md  // src/ 等目录组织与模块边界（模板占位）
│  ├─ component-guidelines.md   // 组件模式与结构约定
│  ├─ hook-guidelines.md        // 自定义 Hook 约定与数据获取模式
│  ├─ state-management.md      // 本地/全局/服务端状态使用策略
│  ├─ quality-guidelines.md    // 代码质量标准、禁用/必用模式
│  ├─ type-safety.md           // 类型组织与运行时校验建议
│  ├─ api-guidelines.md        // API 请求封装与调用流程约定
│  ├─ routing-guidelines.md    // 路由配置位置、meta 语义与写法
│  └─ shared-components-catalog.md // 公共组件清单与复用选型
└─ guides/                      // 思考指南（偏先想清楚）
   ├─ index.md
   ├─ code-reuse-thinking-guide.md     // 先搜索/复用，避免重复实现
   └─ cross-layer-thinking-guide.md    // 跨层数据流与边界问题提前推演
```

---

## 如何使用这些文档

1. `frontend/index.md`：作为入口，列出各子指南并说明其用途与填写目标。
2. `guides/index.md`：当你要实现新功能前，可以先快速浏览“思考触发点”（跨层、复用）。
3. 对团队来说，最重要的是把 `frontend/*` 里的占位内容替换成「你们项目真实采用的写法/目录/禁用项」。

---

## 语言约定提醒

- 该 spec 中一些核心 scaffold 文件使用英文占位（如 `frontend/` 的部分说明）。
- 也存在中文的 starter 模板（如 `api-guidelines.md`、`routing-guidelines.md` 等）。
> 建议由团队统一：最终以“全中文”或“全英文 + 必要术语英文”的风格为准，避免文档与代码约定混乱。

