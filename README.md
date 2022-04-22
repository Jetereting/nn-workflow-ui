# nn-workflow-ui 前端工作流
![前端工作流](https://github.com/Jetereting/nn-workflow-ui/blob/main/doc/img/workflow-ui.png)

* 插件源码地址 https://codeup.aliyun.com/ninuo/smartDistrictOffice/nn-workflow-ui
* 后端源码地址 https://codeup.aliyun.com/ninuo/smartDistrictOffice/go-workflow
* 后端Docker地址 https://hub.docker.com/repository/docker/jetereting/go-workflow

## 使用方式
1、首先通过npm安装：
```shell
npm install nn-workflow-ui --save
```
2、全局定义组件(否则会报循环引用)：
main.js中
```js
import Node from 'nn-workflow-ui/src/components/Generator/node'
Vue.component('Node', Node)
```
3、在使用的地方：
```
<template>
  <div>
    <workflow
      :data="data"
      @ok="ok"
    />
  </div>
</template>
<script>
import workflow from 'workflow-ui/src/components/Generator'
import 'workflow-ui/lib/workflow-ui.css'
export default {
  components: {
    workflow
  },
  data () {
    return {
      data: {
        title: '请假',
        node: {
          name: '发起人',
          type: 'start',
          nodeId: 'sid-startevent',
        }
      }
    }
  },
  methods: {
    ok (data) {
      console.log(data)
    }
  }
}
</script>
```

## 开发方式

```
vue.config.js:10 修改为： entry: 'src/main.js', 发布前再改回为： entry: 'src/index.js',
npm i
npm run serve
```

如果有：Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: 报错
> 可以 修改
> node_modules/@babel/helper-compilation-targets/package.json:48
> 修改为："exports": {".": "./lib/index.js"},
















