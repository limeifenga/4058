1、报错如下：

npm WARN checkPermissions Missing write access to C:wrap..............
npm ERR! path C:\........
npm ERR! code ENOENT
npm ERR! errno -4058
npm ERR! syscall access
npm ERR! enoent ENOENT: no such file or directory, access 'ordwrap'........
npm ERR! enoent This is related to npm not being able to find a file.
npm ERR! enoent

.............................大坑记录

出现原因，在vue项目中安装 sass 时 ，步骤如下：

cnpm install node-sass --save-dev //安装node-sass
cnpm install sass-loader --save-dev //安装sass-loader
cnpm install style-loader --save-dev //安装style-loader

在webpack.base.config.js 中增加了 module.rules.push了
　{
   test: /\.scss$/,
    loaders: ["style", "css", "sass"]
  }


导致后面出现一连串的错误，直到4058的出现，导致npm无法安装编译工作，想办法解决4058.


找了很多答案都不行，包括
1、换一个npm安装源

2、通过config命令
npm config set registry https://registry.npm.taobao.org

3、命令行指定
npm --registry https://registry.npm.taobao.org info underscore


最后还是  执行了npm 清除缓存 解决问题。
npm  cache clean -f

然后重新安装sass

只执行了2个安装
npm install node-sass sass-loader

然后直接 在页面上 lang = sass 或 lang = scss  使用