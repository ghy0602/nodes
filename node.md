## node

### 1.node 


    node.js       
            俄罗斯人发明的        
            Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。     
        node.js有什么特点？
            1.事件驱动
            2.非阻塞式 I/O 
            3.单线程
    
        深入浅出的nodejs
        了不起的nodejs
         Node.js 的包管理器 npm，是全球最大的开源库生态系统。

### 2

```html
const http = require('http'); //创建一个http的服务器
/*
request:请求（理解为接收客户端发送过来的信息）
response:响应（理解成“发送”给客户端）

listen(端口号)
    当开启一个服务之后需要一直开启，因为用户什么时候访问是不知道的，
    通过listen一直将这个服务开启着，直到有用户来进行访问就执行所需的服务。

进入目录 -> shift + 右键 -> 打开命令窗口
*/

const server = http.createServer(function(request,response){

   //console.log('已经请求服务器了');

   //https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=s&

   response.write('window.baidu.sug({q:"s",p:false,s:["steam","孙 政 才","双世宠妃","搜狗输入法下载","搜狗输入法","顺丰快递单号查询","三国杀","苏宁易购","搜房网","上海天气"]})');

   response.end();

});

server.listen(9090);  

```
    ### 3

    const http = require('http'); //直接下载下来的模块不用路径,如果你引入自己的模块('./httpx')

    const fs = require('fs'); //专门用来操作本地文件

    // http.createServer((req,res)=>{

    //     res.write('hehe');

    //     res.end();

    // }).listen(8888);

    /*

    writeFile:写入文件
        三个参数：
            1.文件名
            2.内容
            3.回调（err）
     */
    
    fs.writeFile('1.txt','hehe',function(err){
    if(err){
        console.log('错误');
    }
    console.log('创建成功了');
    });
### 4

    const http = require('http'); //直接下载下来的模块不用路径,如果你引入自己的模块('./httpx')

    const fs = require('fs'); //专门用来操作本地文件

    // const hh = require('./x.js');

    // http.createServer((req,res)=>{

    //     res.write('hehe');

    //     res.end();

    // }).listen(8888);

    // console.log(hh);

    /*

    readFile:
        第一个参数：
            路径
    
        第二个参数:
            回调函数，
            err ->错误
            
            data -> 数据
       */
    
    fs.readFile('1.txt',function(err, data){
    if(err){
        console.log(err);
    }else{
        console.log(data.toString());
    }
    });

### 5

    const http = require('http'); //直接下载下来的模块不用路径,如果你引入自己的模块('./httpx')

    const fs = require('fs'); //专门用来操作本地文件

    http.createServer((req,res)=>{

    //urlName是前端发送的信息
    let urlName = req.url;
    let na = 'www';
    // console.log(urlName); //  /index.html
    //因为谷歌浏览器会默认给服务器发送一个favicon.ico,如果文件中没有就报错
    if(req.url !== '/favicon.ico'){
        //na + urlName = www/index.html
        fs.readFile(na + urlName,function(err, data){
            if(err){ //如果文件没有读取出来走err
                res.write('404');
            }else{
                //文件读取出来了，data->Buffer格式的，需要使用toString去转一下
                res.write(data.toString());
            }
            res.end();
        });
    }
    }).listen(8888);

### 6.ES6解构

数组的解构，右边是数组，左边一定要是数组


    对象解构：       
    		let {foo} = {foo:1}  -> foo=1
            let {foo:f} = {foo:1}; ->给foo取了个别名叫f，foo就没了，访问就报错

### 7.npm

     npm:   
        是全球最大开源库生态系统（下载器）
          未来要安装的库基本上都可以从npm中去获得 

### 8.复习

	一.启动
	
	写好了一个服务端的js文件之后，要使用node运行，以此来启动服务
	
	打开cmd命令窗口，运行js文件
	
	node js文件 例如：node app.js
	服务端node要遵循一个CommonJS
	1. 一个文件就是一个模块
	2. 每一个模块是的独立的，独立的作用域
	3. 使用模块，要使用require()引入模块
		a. 如果引入的是文件，必须相对或绝对路径
			例如：require('./tools.js')
		b. 使用安装好的第三方模块，不需要写相对路径,自动会到项目根目录下的node_modules搜索
			例如：require('vue')
	
		注意：require返回值引入的那个模块中module.exports的值，默认是一个对象
		4. 暴露模块的API
		把要暴露的api放在module.exports上
	
	5. 模块的分类
		a. 一个文件是一个模块
		b. 一个文件夹是一个模块
			必须在这个文件夹中放入一个描述文件package.json
				在package.json有一个main这一项，规定了文件夹模块的入口js
	
		c. 内置模块，是node提供的
				require('http') http fs path queryString
	
		当使用require('http') 先看下一下内置有没有这个模块，如果有直接返回了。如果没有就找运行的js文件的目录下的node_modules文件夹下的模块
		npm 模块管理器  https://www.npmjs.com/
	下载第三方模块，去npm上下载
	下载：npm install（i） <模块名字>
		安装之后，会在安装的目录下创建文件夹为node_modules
	卸载 : npm uninstall
	更新：npm updata
	
	项目的描述文件：npm init
		会在目录下生成一个package.json 
	
			dependencies:{
				依赖模块
			}
		一般拿到项目没有node_modules，因为这个目录会很大，先安装package.json 中依赖的模块
			npm i




