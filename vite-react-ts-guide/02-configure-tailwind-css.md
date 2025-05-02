# 配置Tailwind CSS

本文档介绍如何在Vite+React+TypeScript项目中添加和配置Tailwind CSS。

## 步骤一：安装Tailwind CSS相关包

首先，安装Tailwind CSS及其Vite插件：

```bash
pnpm add tailwindcss @tailwindcss/vite
```

## 步骤二：配置Vite插件

编辑`vite.config.ts`文件，添加Tailwind CSS插件：

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';
import path from 'path';

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

## 步骤三：导入Tailwind CSS

在`src/index.css`文件中，添加Tailwind的导入：

```css
@import "tailwindcss";
```

这个简单的导入语句会自动包含Tailwind的所有样式。

## 步骤四：自定义主题（可选）

如果你想自定义Tailwind配置，可以创建一个`tailwind.config.js`文件：

```bash
npx tailwindcss init
```

这将创建一个基本的配置文件，你可以根据需要自定义：

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        primary: '#3490dc',
        secondary: '#ffed4a',
        danger: '#e3342f',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
    },
  },
  plugins: [],
}
```

`content`数组指定了Tailwind应该扫描哪些文件来查找类名。上述配置将扫描所有HTML文件和`src`目录下的所有JavaScript和TypeScript文件（包括JSX和TSX）。

## 步骤五：验证配置

创建或修改一个组件来测试Tailwind CSS是否正确配置。例如，修改`src/App.tsx`：

```tsx
function App() {
  return (
    <div className="min-h-screen bg-gray-100 flex items-center justify-center">
      <div className="bg-white p-8 rounded-lg shadow-md">
        <h1 className="text-2xl font-bold text-gray-800 mb-4">
          Tailwind CSS 配置成功！
        </h1>
        <p className="text-gray-600">
          你现在可以在项目中使用Tailwind CSS了。
        </p>
        <button className="mt-4 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 transition-colors">
          开始使用
        </button>
      </div>
    </div>
  );
}

export default App;
```

启动开发服务器，验证Tailwind样式是否生效：

```bash
pnpm dev
```

## 常见问题解决

### 样式未生效

- 确保你在`src/index.css`中正确导入了Tailwind
- 确保在`index.html`中引用了正确的CSS文件
- 检查`vite.config.ts`是否正确配置了tailwindcss插件
- 如果有创建`tailwind.config.js`，检查`content`配置是否包含了你的组件文件路径

### 自定义配置不生效

- 确保`tailwind.config.js`文件位于项目根目录
- 检查配置语法是否正确
- 尝试重启开发服务器

## 下一步

现在Tailwind CSS已经配置完成，继续前往[安装Shadcn UI](./03-install-shadcn-ui.md)。 