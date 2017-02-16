1.vue-cli：vue的脚手架工具
  作用：
      -为我们生成基础的目录结构
      -本地调试
      -代码部署
      -热加载
      -单元测试
  安装：
      -确保node的版本在4以上
        node -v
      -全局安装vue-cli
        npm install -g vue-cli
      -测试安装是否成功
        vue
      -查看可用模板
        vue list
      -使用webpack模版
        vue init webpack sell（项目名）
      -安装依赖
        npm install
      -运行
        npm run dev

2.vue-cli生成项目文件分析
   -build
   -config：都是跟webpack配置相关的文件
   -node_modules:通过npm install安装的依赖库
   -src：源码
   -static：存放第三方静态资源
       gitkeep：一般情况底下git提交会忽略掉空目录，有了这个文件之后，git提交会把这个空目录提交到仓库里
   -babelsrc：barbel的一些配置
   -editorconfig：编辑器的一些配置
   -eslintignore：忽略语法检查的目录文件
   -eslintrc.js: eslint的一些配置
   -gitignore:git会忽略的文件
   -index.html:入口文件
   -package.json:项目的配置文件
   -read.me:项目描述文件

3.项目如何运行
    -修改webstorm中的语法检查
      file - settings - Language&Farmeworks -javascript
    -运行
      npm run dev ----> 本质上执行了 node build/dev-server.js


