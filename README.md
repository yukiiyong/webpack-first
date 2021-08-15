#### mode
① **development**   将process.env.NODE_ENV的值设为development。   
启用
namedChunksPlugin 和namedModulesPlugin  
② **production**   将process.env.NODE_ENV的值设为production。  
启用
FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, NoEmitOnErrorsPlugin,
ModuleContatenationPlugin, OcurrenceOrderPugin, SideEffectFlagPlugin 和UglifyJsPlugin  

#### 在浏览器查看页面   
###### htmlWepackPlugin  
public/index.html  => dist/index.html

html-webpack-plugin config.template  
增加一个配置文件。业务通过设置true/ false 选出所需功能，再根据配置文件的内容，为每个业务生成相应的html文件  

#### 实时展示效果 
###### webpack-dev-server  
1. 启用quiet后，除了初始启动信息之外任何内容均不显示，意味着来自webpack  的错误或警告在控制台看不见  
2. stats ＂errors-only＂终端仅打印出error，当启用quiet或者是noInfo时，此属性不起作用.  
3. 启用overlay后，编译出错时，会在浏览器窗口全屏输出错误信息，默认关闭  
4. clientLogLevel  当使用内联模式，在浏览器控制台会显示消息  

#### devtool  
将编译后的代码映射回原代码  一般用 cheap-module-eval-source-map   
#### loader处理样式文件
- style-loader 动态创建style标签，将CSS插入到head  
- css-loader 负责处理@import等语句  
- postcss-loader 和autoprefixer 自动生成浏览器兼容性前缀  
- less-loader 负责编译.less文件，将其转化为css  

上述loader顺序从右到左执行:  less- postcss-css -style  

修改优先级顺序 enforce =pre优先执行 post 滞后执行

#### url-loader 
- 资源大小小于limit设定值时，资源转为base64，超过则将图片挎贝到dist目录  
- esModule 为false不解析文件路径    
- 生成的文件的文件名就是文件内容的MD5哈希值并保留所用资源的原始拓展名  
options. name= '[name]_[hash:6]. [ext]'  

#### 处理html中本地图片
###### html-withimg -loader 
使用html-withimgloader 后不能使用vm, ejs模板，
可以不用以上插件并如下引用图片  
```<img src= "<% = require('./thor.jpeg')%>" />```

#### 入口文件
###### entry 
数组表示多个主入口，多个依赖文件一起注入  
#### 出口文件
###### output 
- 控制webpack如何输出编译文件  
- publicPath 一般为cdn地址，cdn文件名加hash

#### 每次打包前清空dist目录 
###### clean-webpack-plugin
- 希望dist目录下某文件不清空cleanOnceBefore Bu