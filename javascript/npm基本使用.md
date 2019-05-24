# npm介绍
## 包管理器(Package Manager)
npm 最初它只是被称为 Node Package Manager，用来作为Node.js的包管理器。但是随着其它构建工具(webpack、browserify)的发展，npm已经变成了 "the package manager for JavaScript"，它用来安装、管理和分享JavaScript包，同时会自动处理多个包之间的依赖。

## 常见命令
```
# 全局升级npm版本 
npm install npm -g

# 安装包(默认./node_modules)
npm install <包名>

# 查看全局包安装路径
npm prefix -g

# 卸载包
npm uninstall <包名>

# 搜索包
npm search <关键字>
```

## 使用 package.json
当你的项目需要依赖多个包时，推荐使用 package.json。其优点为：

它以文档的形式规定了项目所依赖的包
可以确定每个包所使用的版本
项目的构建可以重复，在多人协作时更加方便

### 创建package.json文件
npm init 生成文件  
npm init -y 使用默认规则生成文件  
package.json案例如下
```
{
  "name": "gameApp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "pack": "node_modules/.bin/webpack --mode development"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "file-loader": "^3.0.1",
    "url-loader": "^1.1.2",
    "webpack": "^4.32.2",
    "webpack-cli": "^3.3.2"
  }
}
```
需要注意的配置项:  
1. scripts：可以自定义命令，如此处webpack打包命令定义为pack,可以
使用npm run pack执行

2. devDependencies：仅在开发和测试环节中需要依赖的包,通过**npm install <packge> --save-dev**命令自动添加依赖到文件（或者使用简写的参数 -D）

3. dependencies: 在生产环境中需要依赖的包。通过**npm install <packge> --save**命令自动添加依赖到文件（或者使用简写的参数 -S）。  

如果其他人也需要这个项目，只需要把这个 package.json 文件给他，然后进行简单的 npm install 即可。