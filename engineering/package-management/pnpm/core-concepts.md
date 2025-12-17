# pnpm 核心概念

## 1. pnpm 基础

### 1.1 什么是 pnpm

pnpm（Performant npm）是一个高效的 JavaScript 包管理器，旨在解决 npm 和 Yarn 的一些性能和磁盘空间问题。pnpm 使用符号链接和硬链接来管理依赖，实现了极高的磁盘空间利用率和安装速度。

### 1.2 pnpm 的核心优势

1. **磁盘空间高效**：使用硬链接和符号链接共享依赖，避免重复安装
2. **安装速度快**：并行下载依赖，利用缓存加速安装
3. **依赖隔离**：每个项目的依赖相互隔离，避免依赖冲突
4. **可靠的依赖管理**：使用 lockfile 确保依赖版本的一致性
5. **支持 monorepo**：内置对 monorepo 的支持
6. **兼容 npm 生态**：支持 npm 命令和包格式
7. **安全性**：避免依赖劫持，提供更安全的依赖解析
8. **良好的 CLI 体验**：清晰的输出，友好的错误信息

### 1.3 pnpm 与其他包管理器对比

| 特性 | pnpm | npm | Yarn |
|------|------|-----|------|
| 磁盘空间利用率 | 极高（共享依赖） | 低（重复安装） | 中（部分共享） |
| 安装速度 | 快 | 相对较慢 | 快 |
| 依赖隔离 | 优秀 | 差（扁平化依赖树） | 中（yarn 1.x 扁平化，yarn 2+ PnP） |
| monorepo 支持 | 原生支持 | npm 7+ 支持 | 原生支持 |
| 依赖锁定 | pnpm-lock.yaml | package-lock.json | yarn.lock |
| 兼容性 | 兼容 npm 生态 | 原生 | 兼容 npm 生态 |
| CLI 命令 | 兼容 npm 命令 | 原生 | 部分兼容 |
| 缓存机制 | 高效缓存 | 缓存机制相对简单 | 高效缓存 |
| 安全性 | 优秀 | 中 | 优秀 |

## 2. pnpm 快速开始

### 2.1 安装 pnpm

#### 2.1.1 使用 npm 安装

```bash
npm install -g pnpm
```

#### 2.1.2 使用 Homebrew 安装（macOS）

```bash
brew install pnpm
```

#### 2.1.3 使用 Chocolatey 安装（Windows）

```bash
choco install pnpm
```

#### 2.1.4 使用 Scoop 安装（Windows）

```bash
scoop install pnpm
```

#### 2.1.5 验证安装

```bash
pnpm --version
```

### 2.2 基本使用

1. **初始化项目**：
   ```bash
   pnpm init
   ```

2. **安装依赖**：
   ```bash
   # 安装所有依赖
   pnpm install
   
   # 安装特定依赖
   pnpm add [package-name]
   
   # 安装开发依赖
   pnpm add -D [package-name]
   
   # 安装全局依赖
   pnpm add -g [package-name]
   
   # 安装特定版本的依赖
   pnpm add [package-name]@[version]
   
   # 安装最新版本的依赖
   pnpm add [package-name]@latest
   ```

3. **移除依赖**：
   ```bash
   # 移除依赖
   pnpm remove [package-name]
   
   # 移除开发依赖
   pnpm remove -D [package-name]
   
   # 移除全局依赖
   pnpm remove -g [package-name]
   ```

4. **更新依赖**：
   ```bash
   # 检查依赖更新
   pnpm outdated
   
   # 更新所有依赖
   pnpm update
   
   # 更新特定依赖
   pnpm update [package-name]
   
   # 更新到特定版本
   pnpm update [package-name]@[version]
   ```

5. **运行脚本**：
   ```bash
   # 运行 package.json 中的脚本
   pnpm [script-name]
   
   # 运行测试脚本
   pnpm test
   
   # 运行开发脚本
   pnpm dev
   
   # 运行构建脚本
   pnpm build
   ```

6. **查看依赖**：
   ```bash
   # 查看已安装的依赖
   pnpm list
   
   # 查看依赖树
   pnpm list --depth=1
   
   # 查看特定依赖的信息
   pnpm info [package-name]
   
   # 查看依赖来源
   pnpm why [package-name]
   ```

## 3. pnpm 核心特性

### 3.1 依赖管理机制

#### 3.1.1 符号链接和硬链接

pnpm 使用独特的依赖管理机制，通过符号链接和硬链接来共享依赖：

1. **全局存储**：所有依赖存储在全局存储目录中（默认 `~/.pnpm-store`）
2. **硬链接**：从全局存储硬链接到项目的 `.pnpm` 目录
3. **符号链接**：从 `.pnpm` 目录符号链接到项目的 `node_modules` 目录

这种机制确保了：
- 相同版本的依赖只安装一次
- 项目间共享依赖，节省磁盘空间
- 依赖相互隔离，避免冲突

#### 3.1.2 依赖树结构

pnpm 生成的 `node_modules` 目录结构与传统的 npm/yarn 不同，它保持了依赖的原始嵌套结构，同时通过符号链接实现依赖共享：

```
node_modules/
├── .pnpm/                  # 硬链接的依赖存储
│   ├── react@18.2.0/        # React 依赖
│   └── react-dom@18.2.0/    # React DOM 依赖
├── react -> .pnpm/react@18.2.0/node_modules/react  # 符号链接
└── react-dom -> .pnpm/react-dom@18.2.0/node_modules/react-dom  # 符号链接
```

### 3.2 依赖隔离

pnpm 提供了优秀的依赖隔离，每个项目的依赖相互独立，避免了依赖冲突。这种隔离机制确保了：

1. 项目只能访问声明的依赖
2. 避免了依赖劫持攻击
3. 确保了依赖版本的一致性
4. 简化了依赖管理

### 3.3 Monorepo 支持

pnpm 内置了对 monorepo 的支持，使用 `workspace:` 协议来管理工作区之间的依赖。

#### 3.3.1 配置 Monorepo

```yaml
# pnpm-workspace.yaml
packages:
  # 所有在 packages/ 和 components/ 目录下的包
  - 'packages/**'
  - 'components/**'
  # 排除测试目录
  - '!**/test/**'
```

```json
// package.json
{
  "name": "my-monorepo",
  "private": true,
  "packageManager": "pnpm@8.0.0"
}
```

#### 3.3.2 Monorepo 常用命令

```bash
# 安装所有工作区的依赖
pnpm install

# 安装依赖到根目录
pnpm add [package-name] -w

# 安装依赖到所有工作区
pnpm add [package-name] -r

# 安装依赖到特定工作区
pnpm add [dependency] -r --filter [package-name]

# 运行特定工作区的脚本
pnpm --filter [package-name] [script]

# 运行所有工作区的脚本
pnpm -r [script]

# 构建所有工作区
pnpm -r build
```

### 3.4 依赖缓存

pnpm 拥有高效的缓存机制，缓存已下载的依赖，避免重复下载：

```bash
# 查看缓存目录
pnpm store path

# 清理缓存
pnpm store prune

# 查看缓存内容
pnpm store status

# 从缓存中移除特定包
pnpm store remove [package-name]
```

## 4. pnpm 配置

### 4.1 配置文件

pnpm 使用 `.npmrc` 或 `pnpm-workspace.yaml` 文件进行配置。

#### 4.1.1 .npmrc 示例

```ini
# .npmrc
# 使用国内镜像
registry=https://registry.npmmirror.com/

# 保存确切的依赖版本
save-exact=true

# 自动安装 peer dependencies
auto-install-peers=true

# 启用严格的 peer dependencies 检查
strict-peer-dependencies=false

# 配置全局存储目录
store-dir=~/.pnpm-store

# 配置 node_modules 目录结构
node-linker=isolated

# 启用 shamefully-hoist（兼容旧项目）
# shamefully-hoist=true
```

### 4.2 命令行配置

pnpm 支持通过命令行选项进行配置：

```bash
# 设置配置
pnpm config set registry https://registry.npmmirror.com/

# 获取配置
pnpm config get registry

# 删除配置
pnpm config delete registry

# 列出所有配置
pnpm config list
```

## 5. pnpm 高级功能

### 5.1 工作区协议

pnpm 的工作区协议 `workspace:` 允许在 monorepo 中引用其他工作区的包：

```json
// packages/app/package.json
{
  "dependencies": {
    "@my-monorepo/utils": "workspace:^1.0.0"
  }
}
```

### 5.2 依赖过滤

pnpm 支持通过 `--filter` 选项过滤依赖：

```bash
# 只安装特定工作区的依赖
pnpm install --filter [package-name]

# 只构建特定工作区及其依赖
pnpm --filter [package-name]... build

# 只构建依赖于特定工作区的包
pnpm --filter ...[package-name] build
```

### 5.3 自动安装 Peer Dependencies

pnpm 支持自动安装 peer dependencies，简化了依赖管理：

```ini
# .npmrc
auto-install-peers=true
```

### 5.4 依赖版本管理

pnpm 提供了强大的依赖版本管理功能：

```bash
# 安装最新的稳定版本
pnpm add [package-name]

# 安装特定版本
pnpm add [package-name]@1.0.0

# 安装 beta 版本
pnpm add [package-name]@beta

# 安装最新的补丁版本
pnpm add [package-name]@~1.0.0

# 安装最新的次要版本
pnpm add [package-name]@^1.0.0
```

### 5.5 脚本运行钩子

pnpm 支持脚本运行钩子，可以在特定脚本运行前后执行额外的命令：

```json
// package.json
{
  "scripts": {
    "prebuild": "pnpm lint",
    "build": "vite build",
    "postbuild": "pnpm test"
  }
}
```

## 6. pnpm 最佳实践

### 6.1 项目配置最佳实践

1. **使用 pnpm**：享受高效的磁盘空间利用和安装速度
2. **配置合理的注册表**：使用国内镜像加速依赖下载
3. **启用自动安装 peer dependencies**：简化依赖管理
4. **使用 monorepo 管理多包项目**：提高开发效率
5. **提交 pnpm-lock.yaml**：确保依赖版本一致性
6. **使用 workspace: 协议**：在 monorepo 中引用其他工作区

### 6.2 依赖管理最佳实践

1. **明确依赖范围**：使用精确的版本范围，避免意外升级
2. **定期更新依赖**：使用 `pnpm outdated` 和 `pnpm update` 定期更新依赖
3. **使用 peerDependencies**：正确声明对等依赖
4. **避免全局安装**：尽量使用本地安装，避免版本冲突
5. **使用 devDependencies**：区分开发依赖和生产依赖
6. **清理未使用的依赖**：定期清理不再使用的依赖

### 6.3 Monorepo 最佳实践

1. **合理组织工作区结构**：按功能或类型组织包
2. **共享基础配置**：使用共享的配置文件（如 tsconfig.json, eslintrc.js）
3. **统一依赖版本**：确保所有工作区使用相同的依赖版本
4. **避免循环依赖**：防止工作区之间形成循环依赖
5. **使用依赖过滤**：只构建和测试需要的工作区
6. **自动化脚本**：编写自动化脚本简化开发流程

### 6.4 CI/CD 最佳实践

1. **缓存依赖**：缓存全局存储目录，加速 CI/CD 构建
2. **使用 `pnpm install --frozen-lockfile`**：确保依赖版本一致
3. **运行测试**：确保所有测试通过
4. **检查依赖安全**：使用 `pnpm audit` 检查依赖安全问题
5. **构建所有工作区**：使用 `pnpm -r build` 构建所有工作区

## 7. pnpm 常见问题

### 7.1 依赖冲突

```bash
# 查看依赖树
pnpm why [package-name]

# 强制重新安装
pnpm install --force

# 清理缓存后重新安装
pnpm store prune && pnpm install
```

### 7.2 与旧项目的兼容性

```ini
# .npmrc
# 启用 shamefully-hoist 兼容旧项目
shamefully-hoist=true
```

### 7.3 Peer Dependencies 问题

```ini
# .npmrc
# 自动安装 peer dependencies
auto-install-peers=true

# 禁用严格的 peer dependencies 检查
strict-peer-dependencies=false
```

### 7.4 安装失败

```bash
# 清除缓存
pnpm store prune

# 重新安装
pnpm install

# 离线模式安装
pnpm install --offline
```

## 8. pnpm 生态系统

### 8.1 常用工具

| 工具 | 用途 | 安装命令 |
|------|------|----------|
| `pnpm dlx` | 临时执行 npm 包命令，无需安装 | `pnpm dlx [package-name]` |
| `pnpm create` | 创建新项目 | `pnpm create vite` |
| `pnpm exec` | 在项目上下文中执行命令 | `pnpm exec eslint .` |

### 8.2 与其他工具集成

1. **Vite**：支持 pnpm 作为包管理器
2. **Next.js**：支持 pnpm 作为包管理器
3. **Vue CLI**：支持 pnpm 作为包管理器
4. **ESLint**：支持 pnpm 作为包管理器
5. **Prettier**：支持 pnpm 作为包管理器

## 9. 总结

pnpm 是一个高效的 JavaScript 包管理器，通过独特的依赖管理机制实现了极高的磁盘空间利用率和安装速度。它的核心优势包括磁盘空间高效、安装速度快、依赖隔离、可靠的依赖管理和内置对 monorepo 的支持。

pnpm 兼容 npm 生态，支持 npm 命令和包格式，同时提供了更好的性能和安全性。对于大型项目和 monorepo，pnpm 是一个非常优秀的选择。

了解 pnpm 的核心概念和最佳实践，能够帮助开发者更好地管理项目依赖，提高开发效率，节省磁盘空间，确保项目的可靠性和安全性。

pnpm 正在迅速发展，越来越多的项目和工具开始支持 pnpm，它有望成为未来 JavaScript 生态系统中的主流包管理器之一。