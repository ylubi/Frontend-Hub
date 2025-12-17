# npm 核心概念

npm（Node Package Manager）是 Node.js 的包管理工具，用于安装、分享和分发代码，以及管理项目依赖关系。

## 1. 基础概念

### 1.1 包（Package）
包是 npm 生态系统的基本单位，包含可复用的代码、配置文件和元数据。一个包通常包含：
- `package.json` - 包的元数据配置文件
- 源代码文件
- 文档
- 测试文件

### 1.2 模块（Module）
模块是可以被 Node.js `require()` 函数加载的文件或目录。在 npm 中，包和模块通常可以互换使用，但严格来说：
- 包是可以被发布到 npm 注册表的代码单元
- 模块是可以被 Node.js 加载的代码单元

### 1.3 依赖（Dependency）
依赖是项目所需的外部包，分为：
- `dependencies` - 生产环境依赖
- `devDependencies` - 开发环境依赖
- `peerDependencies` - 对等依赖，需要用户手动安装
- `optionalDependencies` - 可选依赖，安装失败不会导致整个安装过程失败
- `bundleDependencies` - 捆绑依赖，会被打包到最终的发布包中

## 2. package.json 配置

`package.json` 是 npm 包的核心配置文件，包含包的元数据和依赖信息。

### 2.1 基本字段

```json
{
  "name": "package-name",
  "version": "1.0.0",
  "description": "包的描述",
  "main": "index.js",
  "scripts": {
    "test": "jest",
    "build": "webpack"
  },
  "keywords": ["keyword1", "keyword2"],
  "author": "作者信息",
  "license": "MIT",
  "dependencies": {
    "react": "^18.0.0"
  },
  "devDependencies": {
    "jest": "^29.0.0"
  }
}
```

### 2.2 关键字段详解

- **name**: 包名，必须唯一，用于在 npm 注册表中标识包
- **version**: 版本号，遵循语义化版本规范（SemVer）
- **main**: 包的入口文件，默认是 `index.js`
- **scripts**: 定义可执行脚本命令
- **dependencies**: 生产环境依赖
- **devDependencies**: 开发环境依赖
- **peerDependencies**: 对等依赖，用于插件类库
- **engines**: 指定 Node.js 和 npm 的版本要求
- **files**: 指定发布到 npm 时包含的文件
- **repository**: 代码仓库地址

## 3. 版本管理

### 3.1 语义化版本规范（SemVer）

npm 使用语义化版本规范，格式为 `MAJOR.MINOR.PATCH`：
- **MAJOR**: 主版本号，不兼容的 API 变更
- **MINOR**: 次版本号，向后兼容的功能性新增
- **PATCH**: 修订号，向后兼容的问题修正

### 3.2 版本范围符号

| 符号 | 描述 | 示例 |
|------|------|------|
| `^` | 兼容最新的次版本号 | `^1.2.3` 表示 `>=1.2.3 <2.0.0` |
| `~` | 兼容最新的修订号 | `~1.2.3` 表示 `>=1.2.3 <1.3.0` |
| `>` | 大于指定版本 | `>1.2.3` |
| `<` | 小于指定版本 | `<1.2.3` |
| `>=` | 大于等于指定版本 | `>=1.2.3` |
| `<=` | 小于等于指定版本 | `<=1.2.3` |
| `=` | 等于指定版本 | `=1.2.3` |
| `*` | 任意版本 | `*` |
| `x` | 匹配任意数字 | `1.x` 表示 `>=1.0.0 <2.0.0` |

## 4. npm 命令行工具

### 4.1 安装命令

```bash
# 全局安装
npm install -g package-name
npm i -g package-name

# 本地安装到 dependencies
npm install package-name
npm i package-name

# 本地安装到 devDependencies
npm install --save-dev package-name
npm i -D package-name

# 安装特定版本
npm install package-name@1.2.3

# 安装对等依赖
npm install --peer

# 安装所有依赖
npm install
npm i
```

### 4.2 卸载命令

```bash
# 卸载本地包
npm uninstall package-name
npm un package-name

# 卸载全局包
npm uninstall -g package-name
npm un -g package-name

# 卸载开发依赖
npm uninstall --save-dev package-name
npm un -D package-name
```

### 4.3 更新命令

```bash
# 查看可更新的包
npm outdated

# 更新指定包
npm update package-name
npm up package-name

# 更新所有包
npm update
npm up

# 全局更新指定包
npm update -g package-name
npm up -g package-name

# 更新 npm 自身
npm install -g npm
```

### 4.4 脚本命令

```bash
# 执行 package.json 中定义的脚本
npm run script-name

# 执行 start 脚本（可省略 run）
npm start

# 执行 test 脚本（可省略 run）
npm test

# 执行 build 脚本（可省略 run）
npm run build
```

### 4.5 发布命令

```bash
# 登录 npm
npm login

# 发布包
npm publish

# 发布测试版本
npm publish --tag beta

# 撤销发布
npm unpublish package-name@version
```

### 4.6 其他常用命令

```bash
# 查看包信息
npm view package-name
npm info package-name

# 查看包版本
npm view package-name versions

# 查看已安装的包
npm list
npm ls

# 查看全局已安装的包
npm list -g
npm ls -g

# 查看包的依赖树
npm list package-name

# 检查项目中是否存在安全漏洞
npm audit

# 修复项目中的安全漏洞
npm audit fix

# 初始化新包
npm init
npm init -y # 快速初始化，使用默认值
```

## 5. 工作区（Workspaces）

工作区是 npm 7+ 引入的功能，用于管理多个相关联的包（monorepo）。

### 5.1 配置工作区

在项目根目录的 `package.json` 中配置：

```json
{
  "name": "monorepo-root",
  "workspaces": [
    "packages/*",
    "apps/*"
  ]
}
```

### 5.2 工作区命令

```bash
# 安装所有工作区的依赖
npm install

# 安装依赖到根目录
npm install package-name -w .

# 安装依赖到指定工作区
npm install package-name -w @scope/package-name

# 在指定工作区执行命令
npm run build -w @scope/package-name

# 在所有工作区执行命令
npm run build -ws
```

## 6. 最佳实践

### 6.1 依赖管理

- 明确区分生产依赖和开发依赖
- 定期更新依赖，修复安全漏洞
- 使用 `package-lock.json` 或 `yarn.lock` 确保依赖版本一致性
- 避免安装过多不必要的依赖
- 优先使用稳定版本的依赖

### 6.2 版本管理

- 严格遵循语义化版本规范
- 使用 git tag 管理版本
- 发布前进行充分测试
- 考虑使用 Conventional Commits 规范自动生成 CHANGELOG

### 6.3 性能优化

- 使用 `npm ci` 替代 `npm install` 进行持续集成
- 配置 `.npmignore` 文件排除不必要的文件
- 考虑使用 pnpm 提高安装速度和节省磁盘空间
- 合理使用缓存机制

### 6.4 安全实践

- 定期运行 `npm audit` 检查安全漏洞
- 避免在生产环境安装开发依赖
- 谨慎使用第三方包，优先选择知名度高、维护活跃的包
- 配置 `npm token` 管理发布权限
- 考虑使用 Snyk 等工具进行依赖安全扫描

## 7. 常见问题与解决方案

### 7.1 安装依赖失败

- 检查网络连接
- 清理 npm 缓存：`npm cache clean --force`
- 删除 `node_modules` 目录和 `package-lock.json` 文件后重新安装
- 尝试使用不同版本的 Node.js
- 检查依赖包是否存在兼容性问题

### 7.2 版本冲突

- 使用 `npm ls` 查看依赖树，定位冲突包
- 使用 `npm dedupe` 消除重复依赖
- 考虑使用 `resolutions` 字段强制指定依赖版本
- 升级或降级冲突的包

### 7.3 权限问题

- 避免使用 `sudo npm install -g`，可以配置 npm 全局安装路径
- 检查文件和目录权限
- 尝试使用 `--unsafe-perm` 标志

### 7.4 发布问题

- 确保包名唯一
- 检查 `package.json` 配置是否正确
- 确保已登录 npm：`npm login`
- 检查 npm 注册表访问权限
- 考虑使用 npm 私有注册表

## 8. 与其他包管理器的比较

### 8.1 Yarn

- 优点：更快的安装速度、离线模式、更严格的依赖锁定
- 缺点：生态相对较小、命令与 npm 不完全兼容

### 8.2 pnpm

- 优点：极致的安装速度、节省磁盘空间、严格的依赖隔离
- 缺点：社区相对较小、某些旧项目可能存在兼容性问题

### 8.3 选择建议

- 新项目：可以考虑使用 pnpm 或 Yarn
- 现有项目：保持使用原有的包管理器
- 团队协作：确保团队成员使用相同的包管理器
- 考虑项目规模和复杂性：大型项目或 monorepo 推荐使用 pnpm 或 Yarn

## 9. 未来发展趋势

- 更高效的安装机制
- 更好的 monorepo 支持
- 更强的安全性保障
- 更好的生态系统整合
- 更智能的依赖管理

npm 作为 Node.js 生态系统的核心工具，不断发展和完善，为前端工程化提供了坚实的基础。掌握 npm 的核心概念和最佳实践，对于提高前端开发效率和代码质量至关重要。