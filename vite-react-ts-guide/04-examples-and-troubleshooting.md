# 示例和问题解决

本文档提供了在Vite+React+TS+Tailwind+Shadcn项目中的实用示例和常见问题解决方案。

## 完整示例：创建一个简单页面

下面是一个使用Shadcn UI组件创建页面的示例：

```tsx
// src/App.tsx
import { useState } from 'react';
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

function App() {
  const [tasks, setTasks] = useState<string[]>([]);
  const [newTask, setNewTask] = useState('');

  const addTask = () => {
    if (newTask.trim()) {
      setTasks([...tasks, newTask.trim()]);
      setNewTask('');
    }
  };

  return (
    <div className="flex min-h-screen items-center justify-center bg-gray-100 p-4">
      <Card className="w-full max-w-md">
        <CardHeader>
          <CardTitle>任务管理器</CardTitle>
          <CardDescription>使用Shadcn UI和Tailwind CSS构建</CardDescription>
        </CardHeader>
        <CardContent>
          <div className="grid w-full items-center gap-4">
            <div className="flex flex-col space-y-1.5">
              <Label htmlFor="new-task">新任务</Label>
              <div className="flex space-x-2">
                <Input 
                  id="new-task" 
                  placeholder="输入任务..." 
                  value={newTask}
                  onChange={(e) => setNewTask(e.target.value)}
                  onKeyDown={(e) => e.key === 'Enter' && addTask()}
                />
                <Button onClick={addTask}>添加</Button>
              </div>
            </div>
            
            {tasks.length > 0 ? (
              <div className="space-y-2">
                <h3 className="text-sm font-medium">任务列表</h3>
                <ul className="space-y-1">
                  {tasks.map((task, index) => (
                    <li 
                      key={index}
                      className="flex items-center justify-between rounded-md border px-3 py-2 text-sm"
                    >
                      <span>{task}</span>
                      <Button 
                        variant="ghost" 
                        size="sm"
                        onClick={() => setTasks(tasks.filter((_, i) => i !== index))}
                      >
                        删除
                      </Button>
                    </li>
                  ))}
                </ul>
              </div>
            ) : (
              <p className="text-sm text-muted-foreground">还没有任务，添加一个吧！</p>
            )}
          </div>
        </CardContent>
        <CardFooter className="flex justify-between">
          <Button 
            variant="outline" 
            onClick={() => setTasks([])}
            disabled={tasks.length === 0}
          >
            清空所有
          </Button>
          <div className="text-sm text-muted-foreground">
            总计: {tasks.length} 个任务
          </div>
        </CardFooter>
      </Card>
    </div>
  );
}

export default App;
```

要运行此示例，你需要先安装以下组件：

```bash
pnpm dlx shadcn add button card input label
```

## 创建自定义主题

以下是如何创建一个自定义主题的示例：

1. 在`src/index.css`中更新主题变量：

```css
@import "tailwindcss";

@layer base {
  :root {
    /* 主色调改为蓝色系 */
    --primary: 221 83% 53%;
    --primary-foreground: 210 40% 98%;
    
    /* 圆角调整为更圆润的感觉 */
    --radius: 0.75rem;
    
    /* ...其他变量保持不变 */
  }
}
```

2. 创建自定义组件主题：

```tsx
// src/components/ui/custom-button.tsx
import { Button, ButtonProps } from "@/components/ui/button"
import { cn } from "@/lib/utils"

interface CustomButtonProps extends ButtonProps {
  gradient?: boolean;
}

export function CustomButton({ 
  gradient = false, 
  className, 
  ...props 
}: CustomButtonProps) {
  return (
    <Button
      className={cn(
        gradient && "bg-gradient-to-r from-blue-500 to-indigo-600 hover:from-blue-600 hover:to-indigo-700", 
        className
      )}
      {...props}
    />
  )
}
```

## 常见问题及解决方案

### 1. TypeScript路径别名不工作

**问题**：导入使用`@/`路径别名的组件时出现"找不到模块"错误。

**解决方案**：

确保在以下文件中正确配置了路径别名：

1. `tsconfig.json`：
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

2. `vite.config.ts`：
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

### 2. 组件样式不加载

**问题**：Shadcn UI组件渲染，但是样式不正确。

**解决方案**：

1. 确保已正确导入Tailwind：
```css
/* src/index.css */
@import "tailwindcss";
```

2. 如果创建了`tailwind.config.js`，检查其中的`content`配置：
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  // ...
}
```

3. 检查`vite.config.ts`中是否正确配置了Tailwind插件：
```ts
import tailwindcss from '@tailwindcss/vite';
// ...
plugins: [
  // 其他插件...
  tailwindcss(),
],
```

4. 尝试重启开发服务器：
```bash
pnpm dev
```

### 3. Shadcn UI组件未正确显示

**问题**：安装Shadcn UI组件后，组件不能正常工作。

**解决方案**：

1. 检查是否已安装所有必要的依赖：
```bash
pnpm add clsx tailwind-merge
```

2. 确保组件的引入路径正确：
```tsx
// 正确的引入方式
import { Button } from "@/components/ui/button";

// 错误的引入方式
import { Button } from "shadcn/button"; // Shadcn UI不是一个npm包
```

3. 检查Shadcn CLI安装组件时是否报错，可能需要手动修复某些组件的依赖。

### 4. 控制台错误："Class value undefined is undefined"

**问题**：使用组件时出现与clsx或类名相关的错误。

**解决方案**：

确保已正确创建并导出`cn`函数：

```ts
// src/lib/utils.ts
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

### 5. 暗色模式不工作

**问题**：设置`.dark`类但暗色模式样式不应用。

**解决方案**：

1. 安装和配置`next-themes`（尽管在Vite项目中，它仍然可以工作）：

```bash
pnpm add next-themes
```

2. 创建主题提供者：

```tsx
// src/components/theme-provider.tsx
import { createContext, useContext, useEffect, useState } from "react";

type Theme = "dark" | "light" | "system";

type ThemeProviderProps = {
  children: React.ReactNode;
  defaultTheme?: Theme;
  storageKey?: string;
};

type ThemeProviderState = {
  theme: Theme;
  setTheme: (theme: Theme) => void;
};

const ThemeProviderContext = createContext<ThemeProviderState | undefined>(undefined);

export function ThemeProvider({
  children,
  defaultTheme = "system",
  storageKey = "vite-ui-theme",
  ...props
}: ThemeProviderProps) {
  const [theme, setTheme] = useState<Theme>(
    () => (localStorage.getItem(storageKey) as Theme) || defaultTheme
  );

  useEffect(() => {
    const root = window.document.documentElement;
    
    root.classList.remove("light", "dark");
    
    if (theme === "system") {
      const systemTheme = window.matchMedia("(prefers-color-scheme: dark)")
        .matches
        ? "dark"
        : "light";
      
      root.classList.add(systemTheme);
      return;
    }
    
    root.classList.add(theme);
  }, [theme]);

  const value = {
    theme,
    setTheme: (theme: Theme) => {
      localStorage.setItem(storageKey, theme);
      setTheme(theme);
    },
  };

  return (
    <ThemeProviderContext.Provider {...props} value={value}>
      {children}
    </ThemeProviderContext.Provider>
  );
}

export const useTheme = () => {
  const context = useContext(ThemeProviderContext);
  
  if (context === undefined)
    throw new Error("useTheme must be used within a ThemeProvider");
    
  return context;
};
```

3. 在应用主入口使用主题提供者：

```tsx
// src/main.tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import './index.css'
import { ThemeProvider } from './components/theme-provider.tsx'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <ThemeProvider defaultTheme="system" storageKey="vite-ui-theme">
      <App />
    </ThemeProvider>
  </React.StrictMode>,
)
```

## 优化建议

### 1. 组件懒加载

对于较大的应用，使用React.lazy和Suspense进行组件懒加载：

```tsx
import { Suspense, lazy } from 'react';

const HeavyComponent = lazy(() => import('./HeavyComponent'));

function App() {
  return (
    <Suspense fallback={<div>加载中...</div>}>
      <HeavyComponent />
    </Suspense>
  );
}
```

### 2. 使用TS严格模式

在`tsconfig.json`中启用严格模式，提高代码质量：

```json
{
  "compilerOptions": {
    "strict": true,
    // ...
  }
}
```

### 3. 使用Vite的构建优化

利用Vite的分块策略优化生产构建：

```ts
// vite.config.ts
export default defineConfig({
  // ...
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          react: ['react', 'react-dom'],
          ui: ['@/components/ui'],
        },
      },
    },
  },
})
```

## 总结

本文档提供了Vite+React+TS+Tailwind+Shadcn项目的实用示例和常见问题解决方案。通过遵循这些最佳实践，你可以创建高质量的现代化React应用。

回到[项目概述](./index.md)。 