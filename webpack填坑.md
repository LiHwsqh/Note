#webpack填坑
##path对象

	const path = require('path');

这个`path`是`node`对象

	path.resolve([...path])
**从右向左**读取参数，如果拼出一个**绝对路径**就返回它，否则会**加上**当前文件所在路径
官方文档里用的就是它，但是[人家并不推荐](https://segmentfault.com/q/1010000004820583)

下面的`join`感觉比`resolve`更可控。

	path.join([...path])

##Config merge
[装个插件](https://www.npmjs.com/package/webpack-merge)

	yarn add webpack-merge
引用

	const webpackMerge = require('webpack-merge');
`config.js`里这样写
```javascript
	module.exports = webpackMerge.smart(basic,{
	    context: currentDirPath,
	    entry: {
	        teacher: './teacher.js',
	        student: './student.js',
	        school: './school.js',
	    },
	    output: {
	        path: path.join(currentDirPath,'/dist'),
	    }
	});
```
`merge`是自动复写的，配置属性内的属性也会[smart merge](https://www.npmjs.com/package/webpack-merge#mergesmartconfiguration--configuration)（自动添加&复写）