# Yarn 核心概念

## 1. Yarn 基础

### 1.1 什么是 Yarn

Yarn（Yet Another Resource Negotiator）是 Facebook 开发的 JavaScript 包管理器，旨在解决 npm 的一些性能和安全性问题。Yarn 提供了更快的安装速度、更可靠的依赖管理和更好的安全性。

### 1.2 Yarn 的核心优势

1. **速度快**：并行下载依赖，缓存已下载的依赖，避免重复下载
2. **可靠性**：使用 lockfile 确保依赖版本的一致性
3. **安全性**：自动验证依赖的完整性，防止恶意代码
4. **离线模式**：可以使用缓存的依赖进行离线安装
5. **确定性**：相同的依赖会生成相同的 node_modules 目录结构
6. **良好的 CLI 体验**：清晰的输出，友好的错误信息
7. **插件系统**：支持插件扩展功能
8. **Workspaces**：支持单仓库多包管理

### 1.3 Yarn 与 npm 的对比

| 特性 | Yarn | npm |
|------|------|-----|
| 安装速度 | 快（并行下载） | 相对较慢（早期版本串行下载，npm 5+ 并行） |
| 依赖锁定 | yarn.lock | package-lock.json |
| 离线模式 | 支持 | 有限支持 |
| 缓存机制 | 高效缓存 | 缓存机制相对简单 |
| 工作区支持 | 原生支持 | npm 7+ 支持 |
| 脚本命令 | 支持 | 支持 |
| 全局安装 | 支持 | 支持 |
| 安全性 | 自动验证依赖完整性 | npm 6+ 支持依赖验证 |
| CLI 体验 | 清晰友好 | 相对复杂 |
| 插件系统 | 支持 | 有限支持 |

## 2. Yarn 快速开始

### 2.1 安装 Yarn

#### 2.1.1 使用 npm 安装

```bash
npm install -g yarn
```

#### 2.1.2 使用 Homebrew 安装（macOS）

```bash
brew install yarn
```

#### 2.1.3 使用 Chocolatey 安装（Windows）

```bash
choco install yarn
```

#### 2.1.4 验证安装

```bash
yarn --version
```

### 2.2 基本使用

1. **初始化项目**：
   ```bash
yarn init
```

2. **安装依赖**：
   ```bash
   # 安装所有依赖
   yarn
   
   # 安装特定依赖
   yarn add [package-name]
   
   # 安装开发依赖
   yarn add -D [package-name]
   
   # 安装全局依赖
   yarn global add [package-name]
   
   # 安装特定版本的依赖
   yarn add [package-name]@[version]
   
   # 安装最新版本的依赖
   yarn add [package-name]@latest
   ```

3. **移除依赖**：
   ```bash
   # 移除依赖
   yarn remove [package-name]
   
   # 移除开发依赖
   yarn remove -D [package-name]
   
   # 移除全局依赖
   yarn global remove [package-name]
   ```

4. **更新依赖**：
   ```bash
   # 检查依赖更新
   yarn outdated
   
   # 更新所有依赖
   yarn upgrade
   
   # 更新特定依赖
   yarn upgrade [package-name]
   
   # 更新到特定版本
   yarn upgrade [package-name]@[version]
   ```

5. **运行脚本**：
   ```bash
   # 运行 package.json 中的脚本
   yarn [script-name]
   
   # 运行测试脚本
   yarn test
   
   # 运行开发脚本
   yarn dev
   
   # 运行构建脚本
   yarn build
   ```

6. **查看依赖**：
   ```bash
   # 查看已安装的依赖
   yarn list
   
   # 查看特定依赖的信息
   yarn info [package-name]
   ```

## 3. Yarn 核心特性

### 3.1 依赖管理

#### 3.1.1 依赖锁定

Yarn 使用 `yarn.lock` 文件锁定依赖版本，确保在不同环境中安装的依赖版本一致。

```yaml
# yarn.lock 示例
react@^18.0.0:
  version "18.2.0"
  resolved "https://registry.npmjs.org/react/-/react-18.2.0.tgz#555bd98592883255fa00de14f1151a917b5d77d5"
  integrity sha512-/3IjMdb2L9QbBdWiW5e3P2/npwMBaU9mHCSCUzNln0ZCYbcfTsGbTJrU/kGemdH2IWmB2ioZ+zkxtmq6g09fGQ==
```

#### 3.1.2 依赖树

Yarn 使用扁平化的依赖树结构，减少依赖重复，优化 node_modules 目录大小。

### 3.2 缓存机制

Yarn 将所有下载的依赖缓存到全局缓存目录中，避免重复下载相同的依赖，提高安装速度。

```bash
# 查看缓存目录
yarn cache dir

# 清除缓存
yarn cache clean

# 查看缓存内容
yarn cache list
```

### 3.3 离线模式

Yarn 支持离线模式，可以使用缓存的依赖进行安装，无需网络连接。

```bash
# 离线安装依赖
yarn install --offline
```

### 3.4 Workspaces

Yarn Workspaces 允许在单个仓库中管理多个包，共享依赖，提高开发效率。

#### 3.4.1 配置 Workspaces

```json
// package.json
{
  "name": "my-monorepo",
  "private": true,
  "workspaces": [
    "packages/*",
    "apps/*"
  ]
}
```

#### 3.4.2 Workspaces 常用命令

```bash
# 安装所有工作区的依赖
yarn install

# 安装依赖到根目录
yarn add [package-name] -W

# 安装依赖到特定工作区
yarn workspace [package-name] add [dependency]

# 运行特定工作区的脚本
yarn workspace [package-name] [script]

# 运行所有工作区的脚本
yarn workspaces run [script]
```

### 3.5 插件系统

Yarn 支持插件扩展功能，可以通过插件添加新的命令和功能。

```bash
# 安装插件
yarn plugin import [plugin-name]

# 示例：安装约束插件
yarn plugin import constraints

# 示例：安装交互式升级插件
yarn plugin import interactive-tools
```

## 4. Yarn 配置

### 4.1 配置文件

Yarn 使用 `.yarnrc` 或 `.yarnrc.yml` 文件进行配置。

#### 4.1.1 .yarnrc.yml 示例

```yaml
# .yarnrc.yml
nodeLinker: node-modules

yarnPath: .yarn/releases/yarn-3.2.0.cjs

npmRegistryServer: "https://registry.npm.taobao.org"

unsafeHttpWhitelist:
  - localhost
  - 127.0.0.1

packageExtensions:
  "react-dom@*":
    dependencies:
      react: ^18.0.0
```

### 4.2 常用配置选项

| 选项 | 描述 | 示例 |
|------|------|------|
| `nodeLinker` | 依赖链接方式 | `nodeLinker: node-modules` |
| `yarnPath` | Yarn 可执行文件路径 | `yarnPath: .yarn/releases/yarn-3.2.0.cjs` |
| `npmRegistryServer` | npm 注册表地址 | `npmRegistryServer: "https://registry.npm.taobao.org"` |
| `cacheFolder` | 缓存目录 | `cacheFolder: .yarn/cache` |
| `enableGlobalCache` | 是否启用全局缓存 | `enableGlobalCache: true` |
| `pnpMode` | PnP 模式 | `pnpMode: loose` |
| `checksumBehavior` | 校验和行为 | `checksumBehavior: update` |

### 4.3 命令行配置

Yarn 支持通过命令行选项进行配置：

```bash
yarn config set npmRegistryServer https://registry.npm.taobao.org
yarn config get npmRegistryServer
yarn config delete npmRegistryServer
yarn config list
```

## 5. Yarn 高级功能

### 5.1 PnP (Plug'n'Play)

PnP 是 Yarn 2+ 引入的新特性，替代传统的 node_modules 目录，提高依赖解析速度和安全性。

#### 5.1.1 启用 PnP

```bash
yarn set version berry
yarn install
```

#### 5.1.2 PnP 优势

1. **更快的依赖解析**：直接通过映射表查找依赖，无需遍历 node_modules
2. **更小的安装体积**：无需生成庞大的 node_modules 目录
3. **更好的安全性**：精确控制依赖访问，防止依赖劫持
4. **更可靠的依赖管理**：确保只使用声明的依赖

### 5.2 Constraints

Constraints 允许定义工作区之间的依赖关系规则，确保工作区之间的依赖一致性。

```yaml
# .yarnrc.yml
plugins:
  - path: .yarn/plugins/@yarnpkg/plugin-constraints.cjs
    spec: "@yarnpkg/plugin-constraints"
```

```yaml
# constraints.pro
# 确保所有包的 React 版本一致
gen_enforced_dependency(WorkspaceCwd, DependencyIdent, DependencyRange):
  DependencyIdent == "react" or DependencyIdent == "react-dom"
  =>
  DependencyRange == "^18.0.0";

# 确保所有包使用相同的 TypeScript 版本
gen_enforced_dependency(WorkspaceCwd, "typescript", DependencyRange):
  =>
  DependencyRange == "^4.6.0";
```

### 5.3 Zero-Installs

Zero-Installs 是 Yarn 2+ 的特性，将依赖缓存提交到版本控制系统，实现零安装部署。

#### 5.3.1 启用 Zero-Installs

```yaml
# .yarnrc.yml
nodeLinker: pnp
enableGlobalCache: false
cacheFolder: .yarn/cache
```

#### 5.3.2 Zero-Installs 优势

1. **更快的 CI/CD**：无需重新下载依赖，直接使用缓存
2. **简化部署流程**：无需运行 `yarn install` 即可部署
3. **提高一致性**：确保所有环境使用相同的依赖

### 5.4 交互式升级

Yarn 提供了交互式升级命令，可以可视化地选择要升级的依赖。

```bash
# 安装交互式工具插件
yarn plugin import interactive-tools

# 交互式升级
yarn upgrade-interactive
```

## 6. Yarn 最佳实践

### 6.1 项目配置最佳实践

1. **使用 Yarn 2+（Berry）**：享受新特性和性能提升
2. **启用 PnP**：提高依赖解析速度和安全性
3. **使用 Workspaces**：管理单仓库多包项目
4. **配置合理的注册表**：使用国内镜像加速依赖下载
5. **提交 yarn.lock**：确保依赖版本一致性
6. **使用 Zero-Installs**：简化 CI/CD 流程

### 6.2 依赖管理最佳实践

1. **明确依赖范围**：使用精确的版本范围，避免意外升级
2. **定期更新依赖**：使用 `yarn upgrade-interactive` 定期更新依赖
3. **使用 peerDependencies**：正确声明对等依赖
4. **避免全局安装**：尽量使用本地安装，避免版本冲突
5. **使用 devDependencies**：区分开发依赖和生产依赖
6. **清理未使用的依赖**：定期清理不再使用的依赖

### 6.3 Workspaces 最佳实践

1. **合理组织工作区结构**：按功能或类型组织包
2. **共享基础配置**：使用共享的配置文件（如 tsconfig.json, eslintrc.js）
3. **统一依赖版本**：使用 constraints 确保依赖版本一致
4. **避免循环依赖**：防止工作区之间形成循环依赖
5. **使用 yarn workspaces run**：统一运行所有工作区的脚本

### 6.4 CI/CD 最佳实践

1. **使用 Zero-Installs**：减少 CI/CD 构建时间
2. **缓存依赖**：如果不使用 Zero-Installs，确保缓存依赖目录
3. **使用 `yarn install --frozen-lockfile`**：确保依赖版本一致
4. **运行测试**：确保所有测试通过
5. **检查依赖安全**：使用 `yarn audit` 检查依赖安全问题

## 7. Yarn 生态系统

### 7.1 官方插件

| 插件 | 用途 | 安装命令 |
|------|------|----------|
| `@yarnpkg/plugin-constraints` | 依赖约束 | `yarn plugin import constraints` |
| `@yarnpkg/plugin-interactive-tools` | 交互式工具 | `yarn plugin import interactive-tools` |
| `@yarnpkg/plugin-version` | 版本管理 | `yarn plugin import version` |
| `@yarnpkg/plugin-workspace-tools` | 工作区工具 | `yarn plugin import workspace-tools` |
| `@yarnpkg/plugin-pnp` | PnP 支持 | 默认安装 |
| `@yarnpkg/plugin-npm` | npm 支持 | 默认安装 |

### 7.2 常用工具

| 工具 | 用途 | 安装命令 |
|------|------|----------|
| `yarn-deduplicate` | 重复依赖去重 | `npm install -g yarn-deduplicate` |
| `yarn-audit-fix` | 自动修复安全问题 | `npm install -g yarn-audit-fix` |
| `yarn-upgrade-all` | 升级所有依赖 | `npm install -g yarn-upgrade-all` |

## 8. Yarn 常见问题

### 8.1 依赖冲突

```bash
# 查看依赖树
yarn why [package-name]

# 去重依赖
yarn-deduplicate
```

### 8.2 安装失败

```bash
# 清除缓存
yarn cache clean

# 重新安装
yarn install --force

# 离线模式安装
yarn install --offline
```

### 8.3 版本不兼容

```bash
# 查看 Yarn 版本
yarn --version

# 切换 Yarn 版本
yarn set version latest
yarn set version classic
```

### 8.4 PnP 兼容性问题

```bash
# 生成 node_modules 兼容层
yarn dlx @yarnpkg/pnpify --sdk vscode
```

## 9. 总结

Yarn 是一个强大的 JavaScript 包管理器，提供了更快的安装速度、更可靠的依赖管理和更好的安全性。它的核心特性包括并行下载、依赖锁定、缓存机制、Workspaces 支持、PnP 等。

Yarn 2+（Berry）引入了许多新特性，如 PnP、Zero-Installs、Constraints 等，进一步提高了依赖管理的效率和安全性。

对于大型项目和单仓库多包项目，Yarn Workspaces 是一个非常有用的特性，可以共享依赖，提高开发效率。

了解 Yarn 的核心概念和最佳实践，能够帮助开发者更好地管理项目依赖，提高开发效率，确保项目的可靠性和安全性。