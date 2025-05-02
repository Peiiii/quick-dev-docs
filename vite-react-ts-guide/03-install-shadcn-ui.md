# 安装Shadcn UI

本文档介绍如何在Vite+React+TypeScript项目中配置和使用Shadcn UI组件库。

## 什么是Shadcn UI？

Shadcn UI不是一个传统的组件库，而是一套高质量、可定制的组件集合，你可以直接复制到你的项目中使用。它建立在Radix UI和Tailwind CSS的基础上，提供了完全可控的组件代码。

## 步骤一：安装必要依赖

首先，安装Node.js类型定义（用于路径别名支持）：

```bash
pnpm add -D @types/node
```

## 步骤二：初始化Shadcn UI

使用Shadcn CLI进行初始化：

```bash
pnpm dlx shadcn init
```

在初始化过程中，CLI会询问一系列问题：

1. **你想使用哪种样式？** 
   - 推荐选择：`default`（默认）

2. **你想使用哪种基本颜色？** 
   - 根据偏好选择，如：`slate`

3. **全局CSS文件的路径是？** 
   - 使用：`src/index.css`（已包含Tailwind导入的文件）

4. **你想自定义CSS变量前缀吗？** 
   - 通常使用默认值（直接回车）

5. **你想使用React Server组件吗？** 
   - 对于纯前端Vite项目，选择：`no`

6. **组件使用的路径别名是？** 
   - 使用：`@/*`

7. **组件目录是？** 
   - 使用：`src/components`

8. **工具类文件是？** 
   - 使用：`src/lib/utils.ts`

## 步骤三：配置路径别名

### 更新TypeScript配置

编辑`tsconfig.json`文件，添加路径别名：

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
    // ...其他配置保持不变
  }
}
```

### 更新Vite配置

确保你的`vite.config.ts`文件包含必要的配置：

```ts
import path from "path";
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})
```

## 步骤四：设置工具类

创建工具类目录和文件：

```bash
mkdir -p src/lib
```

在`src/lib/utils.ts`中添加以下内容：

```ts
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

这个`cn`函数用于合并Tailwind类名，同时处理潜在的冲突。

## 步骤五：安装组件

Shadcn UI的组件需要按需安装。例如，安装按钮和卡片组件：

```bash
# 安装按钮组件
pnpm dlx shadcn add button

# 安装卡片组件
pnpm dlx shadcn add card
```

其他常用组件：

```bash
# 表单相关组件
pnpm dlx shadcn add input form label checkbox select textarea

# 交互组件
pnpm dlx shadcn add dialog dropdown-menu tooltip

# 导航组件
pnpm dlx shadcn add tabs navigation-menu
```

每个组件安装后，会自动添加到`src/components/ui`目录下，你可以直接导入和使用，也可以根据需要进行自定义。

## 步骤六：主题配置（可选）

Shadcn UI使用CSS变量来管理主题。你需要在`src/index.css`中添加CSS变量来支持Shadcn UI组件：

```css
@import "tailwindcss";
 
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
 
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
 
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
 
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
 
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
 
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
 
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
 
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
 
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
 
    --radius: 0.5rem;
  }
 
  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
 
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
 
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
 
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
 
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
 
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
 
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
 
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
 
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}
 
@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

注意这里使用了`@import "tailwindcss";`替代了旧版本的`@tailwind`指令，以符合最新的Tailwind CSS使用方法。

## 常见问题解决

### 组件导入路径问题

确保`tsconfig.json`和`vite.config.ts`中的路径别名配置正确。如果遇到导入问题，检查这两个文件。

### clsx或tailwind-merge未安装

如果遇到与`clsx`或`tailwind-merge`相关的错误，手动安装它们：

```bash
pnpm add clsx tailwind-merge
```

### 组件样式不加载

如果创建了`tailwind.config.js`文件，确保content配置正确：

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
    // 确保包含组件目录
    "./src/components/**/*.{js,ts,jsx,tsx}",
  ],
  // ...
}
```

同时，检查：
- `src/index.css`文件是否使用了正确的导入方式
- `vite.config.ts`中的Tailwind插件是否已正确设置
- 网页中是否正确引入了CSS文件

## 下一步

现在Shadcn UI已经配置完成，继续前往[示例和问题解决](./04-examples-and-troubleshooting.md)。 