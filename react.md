# 命令
脚手架: npm-create-react-app -g
版本: create-react-app --version
创建 create-react-app xxx   (React规范：小写字母+数字+_)

# 结构
React项目
结构
|- node modules
|- src
|- public (存放页面模板)
  |-index.html
|- ...

package.json
- React：核心框架
- React-dom：师徒渲染核心-构建WebApp页面
- react-scripts：打包命令的封装。webpack相关程序隐藏到了node_modules下

# 修改脚手架配置
eject命令
yarn eject

---

babel-preset-env es6+react语法转为es5

create-react-app脚手架使用的是sass

使用less 

```
yarn add less less-loader@8
yarn remove sass-loader
```

