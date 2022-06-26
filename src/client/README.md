# 创建一个模板项目

## 1. 初始化项目

```shell
yarn init -y
```

创建.gitignore文件

```
node_modules
build
dist
.vscode
.idea
yarn.lock
```



## 2. 建立规范的git commit和变更日志

### 2.1 安装依赖

```sh
yarn global add commitizen
```

```sh
yarn add commitizen husky  validate-commit-msg conventional-changelog-cli -D
```

- [commitizen](https://www.npmjs.com/package/commitizen)是一个格式化commit message的工具

- [validate-commit-msg](https://www.npmjs.com/package/validate-commit-msg) 用于检查项目的 `Commit message` 是否符合格式

- [conventional-changelog-cli](https://www.npmjs.com/package/conventional-changelog-cli)可以从`git metadata`生成变更日志

- [husky](https://www.npmjs.com/package/husky)可以使用[git hook](https://git-scm.com/book/zh/v2/%E8%87%AA%E5%AE%9A%E4%B9%89-Git-Git-%E9%92%A9%E5%AD%90)(在git的特定动作发生触发的自定义脚本)

### 2.2 用husky添加git hook

在package.json中添加scripts:

```javascript
  "scripts": {
    "prepare:commit-msg": "husky install && husky add .husky/commit-msg \"yarn validate-commit-msg\" && git add .husky/commit-msg && commitizen init cz-conventional-changelog --save --save-exact"
  },
```

执行命令, 即会加入校验

```javascript
yarn prepare:commit-msg
```

### 2.3 根据提交生成变更日志

```sh
commitizen init cz-conventional-changelog --save --save-exact
```

 在package.json中添加scripts

```javascript
"scripts": {
    "changelogs": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
}
```

想要生成变更日志，可以执行命令

```javascript
yarn changelogs
```

## 3. 提交规范代码

### 3.1 安装lint-staged

[Lint-staged](https://github.com/okonet/lint-staged)可以在commit之前对staged（添加之后）的文件执行一些命令

```sh
yarn add lint-staged -d
```

Lint-staged配置

```javascript
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}":["eslint","git add"],
    "*.{css,less,scss}":["eslint","git add"]
  }
}
```

### 3.2 安装eslint以及代码转换工具

```sh
yarn add eslint typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin --D
```

配置eslint规则

在package.json中配置检查命令

```javascript
  "scripts": {
    "lint": "eslint \"{client,server}/src/**/*.{js,jsx,ts,tsx,css,less,scss}\"",
    "lint:fix": "eslint \"{client,server}/src/**/*.{js,jsx,ts,tsx,css,less,scss}\" --fix"
  },
```





### 3.1 常见的代码规范

- [airbnb中文版](https://github.com/lin-123/javascript)

- [standard中文版](https://github.com/standard/standard/blob/master/docs/README-zhcn.md)

- [百度前端编码规范](https://github.com/ecomfe/spec)

- [styleguide](https://github.com/fex-team/styleguide/blob/master/css.md)

- [CSS编码规范](https://github.com/ecomfe/spec/blob/master/css-style-guide.md)

  

