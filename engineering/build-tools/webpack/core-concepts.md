# Webpack 核心概念

## 1. Webpack 基础

### 1.1 什么是 Webpack

Webpack 是一个现代 JavaScript 应用程序的静态模块打包器（module bundler）。当 Webpack 处理应用程序时，它会递归地构建一个依赖关系图（dependency graph），其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

### 1.2 Webpack 的核心概念

- **入口（Entry）**：指示 Webpack 应该从哪个模块开始构建其内部依赖图
- **输出（Output）**：告诉 Webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件
- **加载器（Loaders）**：让 Webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript 和 JSON）
- **插件（Plugins）**：用于执行范围更广的任务，包括打包优化和压缩，以及重新定义环境中的变量
- **模式（Mode）**：提供 `development` 和 `production` 两种模式，内置了优化配置

## 2. Webpack 配置

### 2.1 基本配置

```javascript
// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // 入口
  entry: './src/index.js',
  
  // 输出
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
    clean: true, // 清理旧文件
  },
  
  // 模式
  mode: 'development',
  
  // 加载器
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.m?js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
    ],
  },
  
  // 插件
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  
  // 开发服务器
  devServer: {
    static: './dist',
    hot: true,
    port: 3000,
    open: true,
  },
  
  // 模块解析
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx'],
  },
};
```

### 2.2 入口配置

```javascript
// 单入口
module.exports = {
  entry: './src/index.js',
};

// 多入口
module.exports = {
  entry: {
    main: './src/index.js',
    vendor: './src/vendor.js',
  },
};

// 动态入口
module.exports = {
  entry: () => new Promise((resolve) => {
    resolve(['./src/index.js', './src/app.js']);
  }),
};
```

### 2.3 输出配置

```javascript
module.exports = {
  output: {
    filename: '[name].[contenthash].js', // 带哈希的文件名
    path: path.resolve(__dirname, 'dist'),
    publicPath: '/', // 公共路径
    chunkFilename: '[name].[contenthash].chunk.js', // 动态导入的文件名
    assetModuleFilename: 'assets/[hash][ext][query]', // 资源文件的输出路径
  },
};
```

## 3. Webpack 加载器

### 3.1 常用加载器

| 加载器 | 用途 | 示例配置 |
|-------|------|----------|
| babel-loader | 转换 ES6+ 代码 | `{ test: /\.m?js$/, use: 'babel-loader' }` |
| css-loader | 解析 CSS 文件 | `{ test: /\.css$/, use: 'css-loader' }` |
| style-loader | 将 CSS 注入到 DOM | `{ test: /\.css$/, use: ['style-loader', 'css-loader'] }` |
| sass-loader | 解析 Sass/SCSS 文件 | `{ test: /\.s[ac]ss$/i, use: ['style-loader', 'css-loader', 'sass-loader'] }` |
| file-loader | 处理文件资源 | `{ test: /\.(png|jpe?g|gif)$/i, use: 'file-loader' }` |
| url-loader | 将小文件转换为 Data URL | `{ test: /\.(png|jpg|gif)$/i, use: { loader: 'url-loader', options: { limit: 8192 } } }` |
| ts-loader | 处理 TypeScript 文件 | `{ test: /\.tsx?$/, use: 'ts-loader' }` |
| vue-loader | 处理 Vue 组件 | `{ test: /\.vue$/, use: 'vue-loader' }` |

### 3.2 资源模块

Webpack 5 引入了资源模块（Asset Modules），用于替代 file-loader、url-loader 和 raw-loader。

```javascript
module.exports = {
  module: {
    rules: [
      // 输出为单独文件
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
      // 转换为 Data URL
      {
        test: /\.txt$/i,
        type: 'asset/inline',
      },
      // 作为字符串导入
      {
        test: /\.md$/i,
        type: 'asset/source',
      },
      // 自动选择（根据文件大小）
      {
        test: /\.svg$/i,
        type: 'asset',
        parser: {
          dataUrlCondition: {
            maxSize: 8 * 1024, // 8kb
          },
        },
      },
    ],
  },
};
```

## 4. Webpack 插件

### 4.1 常用插件

| 插件 | 用途 | 示例配置 |
|------|------|----------|
| HtmlWebpackPlugin | 生成 HTML 文件 | `new HtmlWebpackPlugin({ template: './src/index.html' })` |
| MiniCssExtractPlugin | 提取 CSS 到单独文件 | `new MiniCssExtractPlugin({ filename: '[name].[contenthash].css' })` |
| CleanWebpackPlugin | 清理输出目录 | `new CleanWebpackPlugin()` |
| DefinePlugin | 定义全局变量 | `new webpack.DefinePlugin({ 'process.env.NODE_ENV': JSON.stringify('production') })` |
| CopyWebpackPlugin | 复制静态文件 | `new CopyWebpackPlugin({ patterns: [{ from: 'public', to: 'dist' }] })` |
| BundleAnalyzerPlugin | 分析 bundle 大小 | `new BundleAnalyzerPlugin()` |
| HotModuleReplacementPlugin | 热模块替换 | `new webpack.HotModuleReplacementPlugin()` |
| TerserPlugin | 压缩 JavaScript | `new TerserPlugin()` |

### 4.2 插件配置示例

```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: [MiniCssExtractPlugin.loader, 'css-loader'],
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(),
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css',
      chunkFilename: '[id].[contenthash].css',
    }),
    new CopyWebpackPlugin({
      patterns: [
        {
          from: path.resolve(__dirname, 'public'),
          to: path.resolve(__dirname, 'dist'),
          globOptions: {
            ignore: ['**/.DS_Store'],
          },
        },
      ],
    }),
  ],
};
```

## 5. Webpack 优化

### 5.1 代码分割

#### 5.1.1 入口分割

```javascript
module.exports = {
  entry: {
    main: './src/index.js',
    vendor: ['react', 'react-dom'],
  },
};
```

#### 5.1.2 动态导入

```javascript
// 动态导入
import('./module.js').then((module) => {
  // 使用模块
});

// React 中的动态导入
const LazyComponent = React.lazy(() => import('./LazyComponent'));
```

#### 5.1.3 SplitChunksPlugin

```javascript
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        // 提取 node_modules 中的代码
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all',
        },
        // 提取公共代码
        common: {
          name: 'common',
          minChunks: 2,
          chunks: 'all',
          priority: -10,
          reuseExistingChunk: true,
        },
      },
    },
  },
};
```

### 5.2 缓存

#### 5.2.1 模块缓存

```javascript
module.exports = {
  cache: {
    type: 'filesystem', // 使用文件系统缓存
    buildDependencies: {
      config: [__filename], // 当配置文件变化时，重新构建
    },
  },
};
```

#### 5.2.2 持久化缓存

```javascript
module.exports = {
  optimization: {
    runtimeChunk: 'single', // 提取 runtime 到单独文件
    moduleIds: 'deterministic', // 稳定的模块 ID
    chunkIds: 'deterministic', // 稳定的 chunk ID
  },
};
```

### 5.3 生产环境优化

```javascript
module.exports = {
  mode: 'production',
  optimization: {
    minimize: true,
    minimizer: [
      // 压缩 CSS
      new CssMinimizerPlugin(),
      // 压缩 JavaScript
      new TerserPlugin({
        terserOptions: {
          compress: {
            drop_console: true, // 移除 console
            drop_debugger: true, // 移除 debugger
          },
        },
      }),
    ],
  },
};
```

## 6. Webpack 开发环境

### 6.1 开发服务器

```javascript
module.exports = {
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    compress: true,
    port: 3000,
    hot: true, // 启用热模块替换
    open: true, // 自动打开浏览器
    historyApiFallback: true, // 支持 SPA 路由
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        pathRewrite: { '^/api': '' },
      },
    },
  },
};
```

### 6.2 热模块替换 (HMR)

```javascript
// webpack.config.js
module.exports = {
  devServer: {
    hot: true,
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
  ],
};

// 在应用中启用 HMR
if (module.hot) {
  module.hot.accept('./module.js', () => {
    // 模块更新时的处理
  });
}
```

## 7. Webpack 高级配置

### 7.1 多环境配置

```javascript
// webpack.common.js（公共配置）
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [/* ... */],
  },
  plugins: [/* ... */],
};

// webpack.dev.js（开发配置）
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'development',
  devServer: { /* ... */ },
});

// webpack.prod.js（生产配置）
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'production',
  optimization: { /* ... */ },
});
```

### 7.2 环境变量

```javascript
// 使用 DefinePlugin 定义环境变量
const webpack = require('webpack');

module.exports = {
  plugins: [
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV),
      'process.env.API_URL': JSON.stringify(process.env.API_URL),
    }),
  ],
};

// 使用 EnvironmentPlugin
module.exports = {
  plugins: [
    new webpack.EnvironmentPlugin(['NODE_ENV', 'API_URL']),
  ],
};
```

### 7.3 性能提示

```javascript
module.exports = {
  performance: {
    hints: 'warning', // 性能提示级别：false, 'error', 'warning'
    maxEntrypointSize: 512000, // 入口文件最大大小（字节）
    maxAssetSize: 512000, // 单个资源最大大小（字节）
    assetFilter: function (assetFilename) {
      return assetFilename.endsWith('.js'); // 只检查 JavaScript 文件
    },
  },
};
```

## 8. Webpack 生态系统

### 8.1 常用插件和工具

| 工具 | 用途 |
|------|------|
| webpack-cli | Webpack 命令行工具 |
| webpack-dev-server | 开发服务器 |
| webpack-merge | 合并 Webpack 配置 |
| html-webpack-plugin | 生成 HTML 文件 |
| mini-css-extract-plugin | 提取 CSS 到单独文件 |
| clean-webpack-plugin | 清理输出目录 |
| copy-webpack-plugin | 复制静态文件 |
| webpack-bundle-analyzer | 分析 bundle 大小 |
| css-minimizer-webpack-plugin | 压缩 CSS |
| terser-webpack-plugin | 压缩 JavaScript |

### 8.2 集成框架

#### 8.2.1 React 集成

```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
    ],
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
};
```

#### 8.2.2 Vue 集成

```javascript
// webpack.config.js
const { VueLoaderPlugin } = require('vue-loader');

module.exports = {
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
      },
      {
        test: /\.css$/,
        use: ['vue-style-loader', 'css-loader'],
      },
    ],
  },
  plugins: [new VueLoaderPlugin()],
};
```

## 9. Webpack 最佳实践

### 9.1 开发环境最佳实践

1. 使用 `mode: 'development'` 启用开发模式
2. 配置 `devServer` 提供热更新和快速重载
3. 启用 source map 方便调试
4. 使用 `webpack-merge` 分离开发和生产配置
5. 配置合理的别名，简化导入路径

### 9.2 生产环境最佳实践

1. 使用 `mode: 'production'` 启用生产模式
2. 配置代码分割，优化加载性能
3. 启用持久化缓存，提高构建速度
4. 压缩 CSS 和 JavaScript
5. 移除不必要的代码（tree shaking）
6. 配置合理的哈希策略，实现长效缓存

### 9.3 配置文件最佳实践

1. 分离公共、开发和生产配置
2. 使用环境变量管理不同环境的配置
3. 配置合理的别名，简化导入路径
4. 注释重要的配置项
5. 使用 TypeScript 编写配置文件（可选）

## 10. Webpack 与其他构建工具对比

| 构建工具 | 优势 | 劣势 | 适用场景 |
|---------|------|------|----------|
| Webpack | 强大的插件生态，灵活的配置，支持所有资源类型 | 配置复杂，学习曲线陡峭，构建速度相对较慢 | 大型复杂项目，需要高度定制化的构建流程 |
| Vite | 极快的启动速度，按需编译，原生 ESM 支持 | 生态相对较小，一些高级特性需要插件支持 | 现代前端项目，特别是 Vue 和 React 项目 |
| Rollup | 优秀的 tree shaking，输出体积小，适合库开发 | 配置相对复杂，对动态导入支持不如 Webpack | 库开发，需要优化输出体积的项目 |
| Parcel | 零配置，快速上手，自动安装依赖 | 配置灵活性差，插件生态相对较小 | 小型项目，快速原型开发 |
| Esbuild | 极快的构建速度，支持多种语言 | 生态不成熟，配置选项有限 | 需要快速构建的项目，CI/CD 环境 |

## 11. 总结

Webpack 是一个功能强大的静态模块打包器，拥有丰富的插件生态和灵活的配置选项，能够处理各种复杂的构建场景。虽然学习曲线相对陡峭，但对于大型复杂项目来说，Webpack 提供的强大功能和灵活性是不可或缺的。

随着 Vite 等新型构建工具的兴起，Webpack 的地位受到了一定的挑战，但 Webpack 仍然是前端构建领域的重要工具，特别是对于需要高度定制化构建流程的项目。

了解 Webpack 的核心概念和最佳实践，能够帮助前端开发者更好地配置和使用 Webpack，优化项目的构建流程和性能。