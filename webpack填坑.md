# webpack填坑
## path对象
这个`path`是`node`对象

	const path = require('path');
	path.resolve(@string, @string)

**从右向左**读取参数，如果拼出一个**绝对路径**就返回它，否则会**加上**当前文件所在路径
`webpack`官方文档里用的是`join`，但是[人家并不推荐](https://segmentfault.com/q/1010000004820583)，看了一下`resolve`确实比`join`更清晰

## [webpack-merge](https://www.npmjs.com/package/webpack-merge)

一个工程里面的项目页面很多的时候,用`webpack-merge`插件可以少写一些公共配置

	yarn add webpack-merge

	const merge = require('webpack-merge');

	merge.smart(basic,{...option})

`merge`会自动合并数组与对象属性，复写重复的数组元素和属性,[smart merge](https://www.npmjs.com/package/webpack-merge#mergesmartconfiguration--configuration)

### template

	const a = { 
		array :  [ 1, 2 ],
		 object : { prop : 1 } 
	};

	const b = { 
		array : [ 2, 3], 
		object : { prop : 1.1, prop2 : 2}, 
		whatever : 1
	};

	merge.smart( a, b ) 
	
	//返回
	{ 
		array : [ 1, 2, 3 ],
		object : { prop : 1.1, prop2 : 2 },
		whatever : 1
	}

# webpack的配置文件可以使用process.env.NODE_ENV，来设置不同的打包配置

打包命令

	webpack -p 

 相当于 

	webpack --define process.env.NODE_ENV='production'

感觉是在全局环境里定义了一个`process.env.NODE_ENV`变量，值为`production`

 可以直接在所有js文件中使用`process.env.NODE_ENV`来判断`webpack`是否在进行打包。**包括`webpack`的配置文件**。