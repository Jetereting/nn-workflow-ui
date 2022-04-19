# 插件开发方式：
1.如果有：Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: 报错 可以 修改 
node_modules/@babel/helper-compilation-targets/package.json:48 修改为："exports": {".": "./lib/index.js"},

2.开发时修改：
vue.config.js:10 修改为：
entry: 'src/main.js',
发布前再改回为：
entry: 'src/index.js',


插件源码地址 https://github.com/Jianguoqd/ninuo-workflow.git

workflow-ui 前端工作流 UI
![image](https://github.com/Jianguoqd/ninuo-workflow/blob/main/doc/img/workflow-ui.png)

1、首先通过npm安装： npm install workflow-ui --save

（注意：新版本插件未生效的话，试试npm update命令，或者workflow-ui版本并删除node_modules重新下载）

2、全局定义组件(否则会报循环引用)：
main.js中

import Node from 'workflow-ui/src/components/Generator/node'
Vue.component('Node', Node)

3、在使用的地方：










