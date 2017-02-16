1.npm
    全称：node package manager（node 包管理器）
    会随着node.js的安装自动下载
    作用：
        允许用户从npm服务器下载别人编写的第三包到本地使用
        允许用户从npm服务器下载并安装别人编写的命令行程序到本地使用
        允许用户将自己编写的包或命令行程序上传到npm服务器供别人使用
     安装包
        npm install
     创建项目文件
        npm init
     查看全局目录
        npm config get prefix
     npm允许在package.josn文件中，使用scripts字段定义脚本命令
        npm run 脚本名
     查看npm可用的所有脚本
        npm run


2.webpack
    -作用：模块打包器，在webpack里所有的文件都可以是模块

    -首先全局安装webpack ：npm install webpack -g
    -其次在项目中初始化package.json:npm init
    -再局部安装webpack：npm install webpack --save-dev
        --save：将模块写入dependencies属性(项目应用运行时依赖)
        --save-dev:将模块写入devDependencies(项目应用开发时依赖)
        为什么全局安装之后还要局部安装
            全局安装：使开发者能在任何目录底下运行webpack命令
                      还会锁定webpack的版本
            局部安装：使项目使用本地的webpack版本
     -进行打包
         webpack {entry file/入口文件} {destination for bundled file/存放bundle.js的地方}
         webpack app/main.js public/bundle.js（全局安装）
         node_modules/.bin/webpack app/main.js public/bundle.js（没有全局安装）
     -通过配置文件webpack.config.js来使用Webpack
          module.exports = {
              devtool: 'eval-source-map',
              // 注“__dirname”是node.js中的一个全局变量，它指向当前执行脚本所在的目录。
              entry:  __dirname + "/app/main.js",//已多次提及的唯一入口文件
              output: {
                  path: __dirname + "/public",//打包后的文件存放的地方
                  filename: "bundle.js"//打包后输出文件的文件名
              }
          }
          这条命令会自动参考webpack.config.js文件中的配置选项打包你的项目
          webpack(非全局安装需使用node_modules/.bin/webpack)
     -更快捷的执行打包任务
         在package.json中对npm的脚本部分进行相关设置即可
              script: {
                 "start": "webpack" //配置的地方就是这里啦，相当于把npm的start命令指向webpack命令
               },

         npm的start是一个特殊的脚本名称，它的特殊性表现在，在命令行中使用npm start就可以执行相关命令，
         如果对应的此脚本名称不是start，想要在命令行中运行时，需要这样用npm run {script name}如npm run build

         package.json中的脚本部分已经默认在命令前添加了node_modules/.bin路径，所以无论是全局还是局部安装的Webpack，
         你都不需要写前面那指明详细的路径了。
     -使用webpack构建本地服务器
          // 首先要全局安装依赖
          npm install -g webpack-dev-server
          devServer: {
                  contentBase: "./public",//本地服务器所加载的页面所在的目录
                  colors: true,//终端中输出结果为彩色
                  historyApiFallback: true,//不跳转
                  inline: true//实时刷新
              }
            contentBase	：默认webpack-dev-server会为根文件夹提供本地服务器，
                          如果想为另外一个目录下的文件提供本地服务器，
                          应该在这里设置其所在目录（本例设置到“public"目录）
            port	    ：设置默认监听端口，如果省略，默认为”8080“
            inline	    ：设置为true，当源文件改变时会自动刷新页面
            colors	    ：设置为true，使终端输出的文件为彩色的
            historyApiFallback：在开发单页应用时非常有用，它依赖于HTML5 history API，
                                如果设置为true，所有的跳转将指向index.html



