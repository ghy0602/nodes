## ajax

### 	1.ajax

     AJAX：       
            Asynchronous JavaScript and XML（异步JavaScript和XML)
            JSON
    
                '[]'  '{}'
            当下的数据格式不再只有XML了，还有JSON
            后端吐的所有的数据都是字符串。
    
            '[]' '{}'
    
            前后端的数据交互的。----> 获取数据
    
            优点:
                可以提高系统性能，优化用户界面，基本不跳转
    
            安装集成环境:
                后端的文件必须运行在服务器上，***文件夹必须不能是中文，尽量文件名也英文。
    		localhost/2017-10-23/xx.html
            ajax并不难，****难点是在数据处理上面
### 	2.ajax的数据请求方式

           **** 1.url是谁？
            2.要给后端传什么？
            3.成功了以后数据长什么样子？*******
        ajax({
            url:'php/get.php',
            data:{
                user:userId.value
            },
            success:function(data){
                //'xxx(用户名可以注册)'
                data.replace(/(\((\D+)\))/,function($0,$1,$2){
                    // console.log($2);
                    data = $2;
                });
    
                switch(data){
                    case '用户名可以注册':
                        userId.className = 'ok';
                    break;
                    case '用户名已经被注册了':
                        userId.className = 'error';
                    break;
                    default:
                        userId.className = 'error';
                    break;
                }
            }
        });
    }
### 	3.ajax的原理

    userId.onblur = function(){   
       /*
        打电话流程:
           1. 买个电话
           2. 输入对方的电话号码  010            
           3. 点击发送按钮
           4. 等待接听
           5. 通话
           ajax的交互模型:
                1.创建一个ajax对象
                2.填写地址
                3.发送给服务器
                4.等待
                5.通话
       */
    	var ajax = new XMLHttpRequest; //创建一个ajax对象
    	//填写地址。
        ajax.open('get','php/get.php?user='+userId.value,true);
    	//发送给服务器
        ajax.send();
        //等待
        ajax.onload = function(){
            //通话
            console.log(ajax.responseText);
        }
    }
### 	4.ajax的post

     userId.onblur = function(){   
        var ajax = new XMLHttpRequest; //创建一个ajax对象
        //填写地址。
        ajax.open('post','php/post.php',true);
        ajax.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        //发送给服务器
        ajax.send('user='+userId.value);
        //等待
        ajax.onload = function(){
            //通话
            console.log(ajax.responseText);
        }
    }
### 	6.post与get

      get方式（安全性不是太高的，体积较小的）：     
           通过地址栏进行数据的传输。.php?user=leo&password=123456
            ?user=leo&password=12345（open('get',url+字段拼接)）
            相对不安全
            体积较小，具体能传输多少，跟浏览器限制有关系
            在写中文的时候，IE下会把中文转成URI编码，会引起报错。
            通过encodeURI(转一下);


        post（跟用户信息相关的、较大体积的）
            服务器进行传输(拼接的字段要在send中)
            理论上来说是没有大小限制的（后端会做限制）
            相对就安全一些
            在send前加请求头
            ajax.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
### 	7.UPI码

    let str = '%E4%B8%8E';
    console.log(decodeURI(str));  //码转中文
    console.log(encodeURI('与'))//把中文转成URI码

### 8.同步异步

    同步:       
           前面的没有执行完，后面的不会执行，一直等待
     异步：
            不用等待前面执行完，后面的代码依然执行
   ### 9.兼容                     


    IE9以上才支持ajax的onload事件
    ajax.onreadystatechange兼容
    	有五步：       
             0-4
             ***0是监控不到的 ，到了第五步说明完成
            0 － （未初始化）还没有调用send()方法 
            1 － （载入）已调用send()方法，正在发送请求 
            2 － （载入完成）send()方法执行完成，已经接收到全部响应内容 
            3 － （交互）正在解析响应内容 
            4 － （完成）响应内容解析完成，可以在客户端调用了   
    
            onreadystatechange 每当完成一步就执行一次 
    
            如果把onreadystatechange放在send之前，那么可以监听到第2步，
            但是意义不大，因为4之前的步骤，前端都拿不到数据，只有第五步的时候
            前端才能有数据。
    
            ajax.readyState查看当前到了第几步。
    
            200-207 成功的范围
            5字开头一定是后端的问题
    ajax.onreadystatechange = function(){       
           // alert(ajax.responseText);
            if(ajax.readyState === 4){
                //alert(ajax.responseText);
                if(ajax.status >= 200 && ajax.status <= 207){
                    alert(ajax.status);
                }else{
                    alert('失败');
                }
                
            }
        }
### 10.序列化操作

​      对象转字符串：

    
    //    name=hh&age=18&sex=人妖  
       var o = {
           name:'hh',
           age:18,
           sex:'人妖'
       } 
       var arr = [];
       for(var attr in o){
       	console.log(attr)
           arr.push(attr + '=' + o[attr]);
       }
    	console.log(arr)
       console.log(arr.join('&'));
​	字符串转对象

	var str = 'name=hh&age=18&sex=人妖';
	var arr = str.split('&');
	var o = {};
	arr.forEach((e)=>{
	    var a2 = e.split('=');
	    console.log(a2)
	    o[a2[0]] = a2[1];
	    console.log(o[a2[0]])
	});
	
	console.log(o);
### 11.eval

       eval();     
            把能够运行js运行
            容易被注入病毒，不过都在用。
### ajax的封装函数

    function ajax(json){
    //默认的配置
    var settings = {
        url:'',
        method:'get',
        success:function(){},
        fail:function(){},
        data:{},
        dataType:'json'
    }
    
    //有配置走配置，没配置走默认
    for(var attr in json){
        settings[attr] = json[attr]; 
    }
    
    //序列化操作，把对象转成字符串，可以去看第6个课件
    var arr = [];
    for(var attr in settings.data){
        arr.push(attr + '=' + settings.data[attr]);
    }
    settings.data = arr.join('&');
    var ajax = new XMLHttpRequest;
    // console.log(settings.data);
    if(settings.method === 'get'){
        ajax.open('get',settings.url+'?'+settings.data,true);
        ajax.send();
    }else if(settings.method === 'post'){
        ajax.open('post',settings.url,true);
        ajax.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
        ajax.send(settings.data);
    }
    ajax.onreadystatechange = function(){
        //4代表完成
        if(ajax.readyState === 4){
            //200-207之前算成功
            if(ajax.status >= 200 && ajax.status <= 207){
                //说明我要json
                if(settings.dataType === 'json'){
                    var d = ajax.responseText;
                    //eval('('+ new Function('','return'+ d)() +')')
                    settings.success(new Function('','return'+ d)());
                }else if(settings.dataType === 'xml'){
                    settings.success(ajax.responseXML);
                }else if(settings.dataType === 'str'){
                    settings.success(ajax.responseText);
                }
                
            }else{
                settings.fail(ajax.status);
            }
        }
    }
}