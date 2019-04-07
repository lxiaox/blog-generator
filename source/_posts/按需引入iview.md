---
title: 按需引入iview
date: 2019-04-07 12:40:56
tags: （V）iview
---
### 1、安装iview
`$ npm install iview --save`

### 2、借助插件 babel-plugin-import可以实现按需加载组件，减少文件体积。首先安装，并在文件 .babelrc 中配置：


	```
	npm install babel-plugin-import --save-dev
	
	// .babelrc
	{
	  "plugins": [["import", {
	    "libraryName": "iview",
	    "libraryDirectory": "src/components"
	  }]]
	}
	
	```

## 记录.babelrc:

	```
	{
	  "presets": [
	    ["env", {
	      "modules": false,
	      "targets": {
	        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
	      }
	    }],
	    "stage-2"
	  ],

	  // 注意：plugins中是数组嵌套数组

	  "plugins": ["transform-vue-jsx", "transform-runtime", ["import", {
	    "libraryName": "iview",
	    "libraryDirectory": "src/components"
	  }]],
	  "env": {
	    "test": {
	      "presets": ["env", "stage-2"],
	      "plugins": ["transform-vue-jsx", "transform-es2015-modules-commonjs", "dynamic-import-node"]
	    }
	  }
	}
	
	```

### 3、一般在main.js中引入

	```
	// import  iView from 'iview'	//全部引入
	import  {Tabs, TabPane} from 'iview'
	import 'iview/dist/styles/iview.css'
	
	// Vue.use(iView)
	Vue.component('Tabs', Tabs)
	Vue.component('TabPane', TabPane)
	```

#### 使用：

	```
	// 直接在某一文件中加入
	<Tabs value="name1">
	    <TabPane label="标签一" name="name1">标签一的内容</TabPane>
	    <TabPane label="标签二" name="name2">标签二的内容</TabPane>
	    <TabPane label="标签三" name="name3">标签三的内容</TabPane>
	    </Tabs>
	```