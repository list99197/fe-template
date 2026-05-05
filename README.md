# Spec 模板仓库

可下载的 Trellis `.trellis/spec/` 模板集合，用法对齐 [mindfold-ai/marketplace](https://github.com/mindfold-ai/marketplace)。

## 目录结构

```
.
├── specs/       # Spec 模板（复制到项目的 .trellis/spec/）
├── index.json   # 模板索引（id、path、tags 等）
└── README.md
```

## 使用方式

### 手动安装

将 `specs/<模板 id>/` 下需要的内容复制到目标项目的 `.trellis/spec/`。

例如使用 **new-react-vite-h5** 的前端规范：

- 复制 `specs/new-react-vite-h5/frontend/` → `.trellis/spec/frontend/`

### 通过 npx skills（若你的工具链与 Trellis marketplace 一致）

按你组织的仓库地址替换下方命令：

```bash
npx skills add <org>/<repo>
```

## 模板列表

见根目录 `index.json` 中的 `templates` 数组。
