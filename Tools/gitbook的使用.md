# 是什么
实际上，GitBook 是一个基于 **Node.js 的命令行工具**，支持 Markdown 和 AsciiDoc 两种语法格式，可以输出 HTML、PDF、eBook 等格式的电子书

# 如何使用
1. 安装nodejs环境，npm包管理工具
2. 使用npm安装gitbook cli环境
3. 在文件夹中打开命令行界面，执行 gitbook init 执行完后就会在当前目录下生成README.md和 SUMMARY.md文件
4. 开始编辑笔记,执行gitbook serve后，浏览器中访问http://localhost:4000进行预览
5. 如果要部署到github上，只需要在当前目录下git init初始化仓库，执行git remote add添加远程仓库地址，再push过去即可