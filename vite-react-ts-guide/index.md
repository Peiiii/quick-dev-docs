# 快速搭建Vite-React-TS项目指南

本文档将指导你如何使用以下技术栈快速创建一个现代化的前端项目：

- Vite - 快速的构建工具
- React - 用户界面库
- TypeScript - 类型安全的JavaScript超集
- pnpm - 高效的包管理器
- Tailwind CSS - 实用优先的CSS框架
- Shadcn UI - 可定制的UI组件库

## 前置要求

确保你的系统上已安装：

- Node.js (推荐v16+)
- pnpm (`npm install -g pnpm`)

## 文档目录

本指南分为以下几个部分：

1. [项目初始化](./01-project-initialization.md) - 创建Vite项目并安装基础依赖
2. [配置Tailwind CSS](./02-configure-tailwind-css.md) - 添加和配置Tailwind CSS
3. [安装Shadcn UI](./03-install-shadcn-ui.md) - 设置和配置Shadcn UI组件库
4. [示例和问题解决](./04-examples-and-troubleshooting.md) - 组件使用示例和常见问题解决方案

按照上述顺序阅读文档，可以完整地搭建一个基于Vite的React+TypeScript项目，并集成现代化的UI工具链。

## 快速开始

如果你想要最快速地搭建项目，可以执行以下命令：

```bash
# 创建项目
pnpm create vite my-project --template react-ts
cd my-project
pnpm install

# 添加Tailwind CSS
pnpm add tailwindcss @tailwindcss/vite

# 配置Vite以使用Tailwind
# 编辑vite.config.ts添加:
# import tailwindcss from '@tailwindcss/vite';
# 并在plugins数组中添加tailwindcss()

# 在src/index.css中添加:
# @import "tailwindcss";

# 添加Shadcn UI
pnpm add -D @types/node
pnpm dlx shadcn init

# 安装常用组件
pnpm dlx shadcn add button card

# 启动项目
pnpm dev
```

详细的配置步骤和最佳实践，请参考各个子文档。 