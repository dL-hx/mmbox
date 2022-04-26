### 2.1 启用装饰器语法支持(方式1)

``` 
1. 弹射项目底层配置: npm run eject
2. 下载装饰器语法babel 插件: npm install @babel/plugin-proposal-decorators -D
3. 在package.json 文件中加入配置

"babel":{
	"plugins": [
    // ["import", {
    //   "libraryName": "antd",
    //   "libraryDirectory": "es",
    //   "style": "css" // `style: true` 会加载 less 文件
    // }],

    // ↓这里支持装饰器语法配置
    ["@babel/plugin-proposal-decorators", { "legacy": true }]
   
  ]
}
```





### 2.2 启用装饰器语法支持(方式2)

1. npm install react-app-rewired customize-cra @babel/plugin-proposal-decorators --save-dev
2. 在项目根目录下创建 `config-overrides.js` 并加入如下配置




##### `config-overrides.js`

``` js
const { override, addDecoratorsLegacy } = require("customize-cra");
const path = require("path");

module.exports = override(

  addDecoratorsLegacy()  
   
); 
```

最后修改启动配置package.json

```js
 "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react--app-rewired test",
    "eject": "react-scripts eject"
  },
```

### 解决语法警告
  搜索：problems.decorations.enabled     
  搜索："javascript.implicitProjectConfig.experimentalDecorators":true