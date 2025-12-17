# 代码规范

代码规范是前端工程化的重要组成部分，它可以提高代码的可读性、可维护性和一致性，减少团队协作中的摩擦，提高开发效率。

## 1. 为什么需要代码规范

- **提高可读性**：统一的代码风格使代码更容易阅读和理解
- **提高可维护性**：一致的代码结构便于后续维护和修改
- **减少错误**：规范的代码编写方式可以减少常见错误
- **提高团队协作效率**：统一的规范避免了团队成员之间的代码风格冲突
- **便于自动化工具处理**：规范的代码更容易被自动化工具（如编译器、lint工具、格式化工具）处理

## 2. 常见的代码规范工具

### 2.1 ESLint

ESLint 是一个可配置的 JavaScript 代码检查工具，它可以检查代码中的语法错误和潜在问题，并强制执行代码风格规则。

#### 2.1.1 核心特性

- 可配置的规则集
- 支持插件扩展
- 支持自定义规则
- 与主流编辑器集成
- 支持 JavaScript、TypeScript、JSX 等

#### 2.1.2 基本配置

```json
// .eslintrc.json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "plugins": [
    "react",
    "@typescript-eslint"
  ],
  "rules": {
    "no-unused-vars": "warn",
    "semi": ["error", "always"],
    "quotes": ["error", "single"]
  }
}
```

#### 2.1.3 常用命令

```bash
# 安装 ESLint
npm install --save-dev eslint

# 初始化 ESLint 配置
npx eslint --init

# 检查特定文件或目录
npx eslint src/

# 自动修复可修复的问题
npx eslint src/ --fix
```

### 2.2 Prettier

Prettier 是一个代码格式化工具，它可以自动格式化代码，确保代码风格的一致性。与 ESLint 不同，Prettier 专注于代码格式化，而不是语法检查。

#### 2.2.1 核心特性

- 支持多种语言（JavaScript、TypeScript、CSS、HTML、JSON 等）
- 可配置的格式化规则
- 与主流编辑器集成
- 与 ESLint 等工具配合使用

#### 2.2.2 基本配置

```json
// .prettierrc.json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80,
  "arrowParens": "avoid"
}
```

#### 2.2.3 常用命令

```bash
# 安装 Prettier
npm install --save-dev prettier

# 格式化特定文件或目录
npx prettier --write src/

# 检查文件是否已格式化
npx prettier --check src/
```

### 2.3 Stylelint

Stylelint 是一个用于检查 CSS 代码风格和错误的工具，类似于 ESLint 但专注于 CSS。

#### 2.3.1 核心特性

- 支持 CSS、SCSS、Less 等
- 可配置的规则集
- 支持插件扩展
- 与主流编辑器集成

#### 2.3.2 基本配置

```json
// .stylelintrc.json
{
  "extends": [
    "stylelint-config-standard",
    "stylelint-config-sass-guidelines"
  ],
  "rules": {
    "indentation": 2,
    "selector-max-id": 0,
    "no-descending-specificity": null
  }
}
```

#### 2.3.3 常用命令

```bash
# 安装 Stylelint
npm install --save-dev stylelint stylelint-config-standard

# 检查特定文件或目录
npx stylelint src/**/*.css

# 自动修复可修复的问题
npx stylelint src/**/*.css --fix
```

### 2.4 Husky

Husky 是一个 Git 钩子工具，它可以在 Git 操作（如提交、推送）前执行自定义脚本，用于检查代码质量、运行测试等。

#### 2.4.1 核心特性

- 支持所有 Git 钩子
- 易于配置
- 与现代前端工具链集成

#### 2.4.2 基本配置

```bash
# 安装 Husky
npm install --save-dev husky

# 初始化 Husky
npx husky install

# 添加 pre-commit 钩子
npx husky add .husky/pre-commit "npx lint-staged"

# 添加 commit-msg 钩子
npx husky add .husky/commit-msg "npx --no -- commitlint --edit $1"
```

### 2.5 Lint-staged

Lint-staged 是一个用于在 Git 暂存区文件上运行脚本的工具，它可以只对修改过的文件进行检查，提高检查效率。

#### 2.5.1 核心特性

- 只对 Git 暂存区的文件进行检查
- 支持并行执行
- 易于配置
- 与 ESLint、Prettier 等工具配合使用

#### 2.5.2 基本配置

```json
// package.json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ],
    "*.{css,scss,less}": [
      "stylelint --fix",
      "prettier --write"
    ],
    "*.{json,md,yml,yaml}": [
      "prettier --write"
    ]
  }
}
```

## 3. 代码规范的最佳实践

### 3.1 建立统一的规范

- 团队成员共同制定和遵守同一套代码规范
- 根据项目特点选择合适的规则集
- 定期回顾和更新规范

### 3.2 自动化检查

- 使用 Git 钩子在提交前自动检查代码
- 在 CI/CD 流程中加入代码规范检查
- 配置编辑器自动格式化代码

### 3.3 教育和培训

- 对团队成员进行代码规范培训
- 定期进行代码审查，讨论代码规范问题
- 建立代码规范文档，方便团队成员查阅

### 3.4 合理配置规则

- 区分错误规则和警告规则
- 避免过于严格或过于宽松的规则
- 根据项目阶段调整规则严格程度

## 4. 常见的代码规范

### 4.1 Airbnb JavaScript 规范

- 一套广泛使用的 JavaScript 代码规范
- 包含 ESLint 配置和 Prettier 配置
- 支持 JavaScript、TypeScript、React 等

### 4.2 Google JavaScript 规范

- 由 Google 制定的 JavaScript 代码规范
- 强调代码的可读性和一致性

### 4.3 Standard JavaScript 规范

- 一套零配置的 JavaScript 代码规范
- 强调简洁性和一致性

## 5. 与其他工具的集成

### 5.1 与编辑器集成

- **VS Code**：安装 ESLint、Prettier、Stylelint 扩展
- **WebStorm**：内置支持 ESLint、Prettier、Stylelint
- **Sublime Text**：安装相应的插件

### 5.2 与构建工具集成

- **Webpack**：使用 eslint-webpack-plugin、stylelint-webpack-plugin
- **Vite**：使用 @vitejs/plugin-eslint

### 5.3 与 CI/CD 集成

- 在 GitHub Actions、GitLab CI 等流程中添加代码规范检查步骤
- 配置失败时阻止合并

## 6. 代码规范的未来趋势

- **更智能的代码检查**：利用 AI 技术自动发现代码问题和优化点
- **更强大的自动修复**：自动修复更复杂的代码问题
- **更好的跨语言支持**：统一的工具链支持多种语言
- **更紧密的 IDE 集成**：实时反馈和修复建议

代码规范是前端工程化的基础，建立良好的代码规范体系对于提高项目质量和团队效率至关重要。选择合适的工具，建立合理的规则，结合自动化检查，可以帮助团队写出更高质量、更易维护的代码。