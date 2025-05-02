# 项目初始化

本文档介绍如何使用pnpm和Vite创建React+TypeScript项目，并安装基础依赖。

## 步骤一：创建Vite项目

首先，使用pnpm和Vite创建一个React+TypeScript项目：

```bash
pnpm create vite my-project --template react-ts
cd my-project
```

创建项目时，Vite会询问一些基本信息：
- 项目名称：可以直接在命令中指定（如上面的`my-project`）
- 框架：选择`react`
- 语言：选择`typescript`

## 步骤二：安装依赖

进入项目目录后，安装项目依赖：

```bash
pnpm install
```

这将安装`package.json`中列出的所有依赖。

## 项目结构

初始化完成后，你的项目结构应该如下：

```
my-project/
├── node_modules/
├── public/
│   └── vite.svg
├── src/
│   ├── assets/
│   │   └── react.svg
│   ├── App.css
│   ├── App.tsx
│   ├── index.css
│   ├── main.tsx
│   └── vite-env.d.ts
├── .eslintrc.cjs
├── .gitignore
├── index.html
├── package.json
├── pnpm-lock.yaml
├── README.md
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts
```

## 默认可用的脚本

Vite项目默认提供以下npm脚本：

- `pnpm dev` - 启动开发服务器
- `pnpm build` - 构建生产版本
- `pnpm lint` - 运行ESLint检查代码
- `pnpm preview` - 预览构建后的项目

## 验证项目配置

启动开发服务器，验证项目已正确设置：

```bash
pnpm dev
```

这将在本地启动开发服务器（默认为http://localhost:5173），你应该能看到Vite+React的欢迎页面。

## 下一步

成功初始化项目后，继续前往[配置Tailwind CSS](./02-configure-tailwind-css.md)。 