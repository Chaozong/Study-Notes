# 结构
## 一个简单的多模块项目
```
---app-parent
        |--pom.xml(pom)
        |--app-dao
        |     |--pom.xml(jar)
        |--app-web
        |     |--pom.xml(war)
        |--app-service
        |     |--pom.xml(jar)
```
# 聚合
\<modules\>聚合标签,可以将子模块(如简单多模块项目结构中,app-dao、app-web、app-service)的互相依赖关系整理为一个build顺序,然后依次build
# 依赖
### dependencyManagement 
此元素来提供了一种管理依赖版本号的方式。通常会在一个组织或者项目的最顶层的父POM 中看到dependencyManagement 元素。使用pom.xml 中的dependencyManagement 元素能让
所有在子项目中引用一个依赖而不用显式的列出版本号。Maven 会沿着父子层次向上走，直到找到一个拥有dependencyManagement 元素的项目，然后它就会使用在这个dependencyManagement 元素中指定的版本号
注：此元素并不会实际下载jar包
### dependencies
相对于dependencyManagement，所有声明在dependencies里的依赖都会自动引入，并默认被所有的子项目继承
# 注意事项
如果修改了pom,最好是把此模块clean一下后再install
