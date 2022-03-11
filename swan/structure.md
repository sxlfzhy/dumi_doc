# 目录结构

- apps 小程序文件夹
  - src
    - pages 页面文件夹
    - components 组件文件夹
    - static 静态文件夹
    - util 工具函数文件夹
  - dist 产出文件夹
  - output 打包产出文件夹
  - [.babelrc](https://www.babeljs.cn/docs/configuration) babel配置文件
  - [.npmrc](https://docs.npmjs.com/cli/v7/configuring-npm/npmrc) npm配置文件
  - [.eslintrc.json](https://cn.eslint.org/docs/user-guide/configuring) eslint配置文件
  - [.prettierrc.json](https://prettier.io/docs/en/configuration.html) prettier配置文件
  - [tsconfig.json](https://www.tslang.cn/docs/handbook/tsconfig-json.html) ts配置文件
  - [yarn.lock](http://yarnpkg.top/Yarn.lock.html) yarn依赖锁定文件 精确存储每个依赖关系的安装版本，确保跨机器的安装一致性，构建时自动生成
  - package.json
    - [husky](https://typicode.github.io/husky/#/)
    - [lint-staged](https://www.npmjs.com/package/lint-staged)
  - package-lock.json
