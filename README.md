# father-template

```sh
# 使用 npm version 命令更新版本号
npm version patch -m "build: release %s"
```

## 使用 decorators

father的umd模式使用babel转译，且只使用了`@babel/preset-env`，需要手动添加decorators支持。

```sh
pnpm add inversify reflect-metadata
pnpm add -D @babel/plugin-proposal-decorators babel-plugin-transform-typescript-metadata
```

`.fatherrc.ts`中新增配置

```js
export default {
  extraBabelPlugins: [
    'babel-plugin-transform-typescript-metadata',
    ['@babel/plugin-proposal-decorators', { legacy: true }],
    // ['@babel/plugin-proposal-class-properties', { loose: true }],
  ],
}
```

storybook需要修改配置`.storybook/main.ts`：

```ts
export default {
  typescript: {
    // 解决编译时 decorate parameters 报错问题
    reactDocgen: 'react-docgen-typescript',
  },
}
```

## TODO

- [] esm/cjs的decorators兼容性还待测试
