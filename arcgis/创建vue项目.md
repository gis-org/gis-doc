## 创建vue项目

## 介绍(自己看官网)


- [vue2官网](https://cn.vuejs.org/) ([vue3在这里](https://v3.cn.vuejs.org/))
- [vue-rotuer官网](https://router.vuejs.org/zh/)
- [vuex官网](https://vuex.vuejs.org/zh/)
- [vue调试工具(必装,需要科学上网)](https://devtools.vuejs.org/)
- [vue组件大全](https://github.com/vuejs/awesome-vue)
- [vue-cli开发工具](https://cli.vuejs.org/zh/)
- [vite开发工具](https://cn.vitejs.dev/)
- [vue-ssr官网](https://ssr.vuejs.org/zh/)
- [nuxtjs官网](https://nuxtjs.org/)(实现vuessr,快速搭建平台)


### 使用vue-cli工具


- 安装：`npm i -g @vue/cli`



> vue-cli是什么?
> Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，提供：

- 通过 @vue/cli 搭建交互式的项目脚手架。
- 通过 @vue/cli + @vue/cli-service-global 快速开始零配置原型开发。
一个运行时依赖 (@vue/cli-service)，该依赖：
可升级；
基于 webpack 构建，并带有合理的默认配置；
可以通过项目内的配置文件进行配置；
可以通过插件进行扩展。
一个丰富的官方插件集合，集成了前端生态中最好的工具。
一套完全图形化的创建和管理 Vue.js 项目的用户界面。

> 如何使用?

```bash
//创建一个项目
vue create your-app
//之后按照提示来就可以

vue ui  //使用可视化界面配置项目
```


### 使用vite开发


[Vite](https://github.com/vitejs/vite) 是一个 web 开发构建工具，由于其原生 ES 模块导入方式，可以实现闪电般的冷服务器启动。
通过在终端中运行以下命令，可以使用 Vite 快速构建 Vue 项目。
使用 npm：


```bash
npm init @vitejs/app <project-name>
cd <project-name>
npm install
npm run dev
```


或者 yarn：


```bash
yarn create @vitejs/app <project-name>
cd <project-name>
yarn
yarn dev
```


但是对于vue2需要一个插件,需要在根目录添加一个vite.config.js,并使用插件vite-plugin-vue2(需要自己研究配置)


```bash
const { createVuePlugin } = require('vite-plugin-vue2');

module.exports = {
  plugins: [createVuePlugin()],
};
```

以上就是创建vue项目的注意事项了