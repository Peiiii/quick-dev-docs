# 项目开发规范

## 文件命名规范

### 基本原则
- 所有文件名使用 kebab-case（短横线分隔）命名方式
- 文件名应简洁明了，能够准确描述文件内容
- 避免使用特殊字符和空格
- 使用小写字母

### 具体规范

#### 1. 目录命名
- 使用小写字母
- 使用短横线分隔单词
- 示例：
  ```
  src/
  ├── components/
  ├── pages/
  ├── utils/
  ├── hooks/
  └── styles/
  ```

#### 2. 文件命名
- 组件文件：使用 PascalCase 命名组件，文件名使用 kebab-case
  ```
  // 组件名：UserProfile
  // 文件名：user-profile.tsx
  ```

- 工具函数文件：使用 kebab-case
  ```
  // 文件名：format-date.ts
  // 文件名：http-request.ts
  ```

- 样式文件：与组件同名，使用 kebab-case
  ```
  // 文件名：user-profile.css
  // 文件名：user-profile.module.css
  ```

- 配置文件：使用 kebab-case
  ```
  // 文件名：vite.config.ts
  // 文件名：tailwind.config.js
  ```

#### 3. 测试文件命名
- 测试文件应与被测试文件同名，添加 `.test` 或 `.spec` 后缀
  ```
  // 文件名：user-profile.test.tsx
  // 文件名：format-date.spec.ts
  ```

#### 4. 文档文件命名
- 使用 kebab-case
- 使用 `.md` 扩展名
  ```
  // 文件名：getting-started.md
  // 文件名：api-documentation.md
  ```

### 命名示例

#### 正确的命名
```
src/
├── components/
│   ├── user-profile/
│   │   ├── user-profile.tsx
│   │   ├── user-profile.css
│   │   └── user-profile.test.tsx
│   └── button-group/
│       ├── button-group.tsx
│       └── button-group.css
├── utils/
│   ├── format-date.ts
│   └── http-request.ts
└── hooks/
    ├── use-local-storage.ts
    └── use-window-size.ts
```

#### 错误的命名
```
src/
├── components/
│   ├── UserProfile/          // 错误：目录名使用 PascalCase
│   │   ├── UserProfile.tsx   // 错误：文件名使用 PascalCase
│   │   └── user profile.css  // 错误：使用空格
│   └── buttonGroup/          // 错误：目录名使用 camelCase
└── utils/
    ├── formatDate.ts         // 错误：文件名使用 camelCase
    └── HTTPRequest.ts        // 错误：文件名使用大写
```

## 其他规范

### 1. 代码组织
- 相关文件应该放在同一个目录下
- 每个组件应该有自己独立的目录
- 共享的工具函数应该放在 `utils` 目录下

### 2. 导入规范
- 使用相对路径导入
- 导入顺序：第三方库 > 项目内部模块
- 示例：
  ```typescript
  // 第三方库
  import React from 'react';
  import { useState } from 'react';
  
  // 项目内部模块
  import { formatDate } from '../utils/format-date';
  import { UserProfile } from '../components/user-profile';
  ```

### 3. 注释规范
- 使用 JSDoc 风格的注释
- 为复杂的函数和组件添加注释
- 示例：
  ```typescript
  /**
   * 格式化日期为 YYYY-MM-DD 格式
   * @param date - 要格式化的日期对象
   * @returns 格式化后的日期字符串
   */
  function formatDate(date: Date): string {
    // ...
  }
  ```

## 注意事项
1. 保持命名的一致性
2. 新文件创建时遵循规范
3. 定期检查并修正不符合规范的命名
4. 在团队中推广和培训这些规范 