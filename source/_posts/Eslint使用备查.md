---
title: ESLint使用备查
date: 2016-06-14 11:48:43
tags: Eslint
categories: 前端
---

ESLint是以可扩展、每条规则独立、不内置编码风格为理念的lint工具

### 1. 安装

```bash
npm install -g eslint
```

### 2. 使用

在项目目录下输入

```bash
eslint --init
```

之后便可以对项目下的任何js文件使用ESLnt，如
```bash
eslint test.js test2.js
```

### 3. 使用要点

#### 3.1 配置

可使用三种方式配置ESLint：
- 使用 `.eslintrc` 文件（可通过`eslint --init`生成）
- 在 `package.json` 文件内添加 `eslintConfig` 配置块
- 在代码文件中定义

###### 3.1.1 `.eslintrc` 示例
项目根目录的 `.eslintrc` 文件会应用到整个项目，子目录中如果也包含 `.eslintrc` 文件则会忽略根目录中的配置

```json
{
  "env": {
    "browser": true,
  },
  "globals": {
    "angular": true,
  },
  "rules": {
    "camelcase": 2,
    "curly": 2,
    "brace-style": [2, "1tbs"],
    "quotes": [2, "single"],
    "semi": [2, "always"],
    "space-in-brackets": [2, "never"],
    "space-infix-ops": 2,
  }
}
```

###### 3.1.2 `package.json` 示例

```json
{
  "name": "mypackage",
  "version": "0.0.1",
  "eslintConfig": {
    "env": {
      "browser": true,
      "node": true
    }
  }
}
```

###### 3.1.3 文件内配置
代码文件内的配置会覆盖配置文件中的规则

- 禁用ESLint:
```js
/* eslint-disable */
var obj = { key: 'value', };
/* eslint-enable */
```

- 禁用一条规则
```js
/*eslint-disable no-alert */
alert('doing awful things');
/* eslint-enable no-alert */
```

#### 3.2 工作流集成

- 在Gulp中使用
```js
var gulp = require('gulp');
var eslint = require('gulp-eslint');

gulp.task('lint', function() {
  return gulp.src('client/app/**/*.js')
    .pipe(eslint())
    .pipe(eslint.format());
});
```

- 在Webpack中使用
```js
var path = require('path')
var webpack = require('webpack')

module.exports = {
  devtool: 'cheap-module-eval-source-map',
  entry: [
    'webpack-hot-middleware/client?noInfo=true&reload=true',
    './index'
  ],
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'bundle.js',
    publicPath: '/static/'
  },
  plugins: [
    new webpack.optimize.OccurenceOrderPlugin(),
    new webpack.HotModuleReplacementPlugin()
  ],
  module: {
    loaders: [
      {
        test: /\.js$/,
        loaders: ['babel', 'eslint'],
        exclude: /node_modules/,
        include: __dirname
      }
    ]
  }
}
```

### 4. 配置规则

[Configuring ESLint](http://eslint.org/docs/user-guide/configuring)