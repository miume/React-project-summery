## React项目总结

##### React + React-Router + Ant-design + axios

#### 项目创建流程

```js
1、打开控制台，输入npm -v 查看npm版本
2、进入创建项目目录 cd ./users
3、先全局安装create-react-app,控制台输入 npm install -g create-react-app
3、npm create-react-app app-name
4、通过脚手架create-react-app能快速构建一个项目结构进行开发
5、在github上新建一个空白项目，本地项目绑定远程项目 
   git remote add origin url
   git push -u origin master  //第一次提交
```

##### 项目启动流程

```js
1、控制台进入项目所在目录
2、npm install      //第一次启动前 先下载项目所需依赖
3、npm start    //启动项目
```

##### React框架介绍

- 用于构用户界面的javaScript库
- React主要用于构建UI，很多人认为React是MVC中的V（视图）
- React起源于facebook的内部项目，有强大的社区支持
- React特点
  - 声明式设计（表明想要实现什么目的，应该做什么，但是不指定具体怎么做）
  - 高效（引入虚拟DOM，减少之间操作DOM元素）
  - JSX（js语法的扩展，all in js）
  - 组件（通过React构建组件，使代码容易得到复用）
  - 单向数据流（数据的流向只能由父组件通过props将数据传递给自组件，不能由自组件直接向父组件传递数据）


<a href='./state和props区别.md' >1、state和props区别.md</a>
<div><a href='./React生命周期' >2、React生命周期介绍（旧和新）</a></div>

