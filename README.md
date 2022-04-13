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










