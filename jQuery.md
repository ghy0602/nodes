## jQuery

### 1.选择器

     只要你会css，就会JQ的选择器  
       $();
        fn();
    
        function $(){}
    
        # -> id选择器
        . -> class选择器
       / console.log($('#box'))
        // console.log($('.li1'))
    
        // console.log($('input[type="button"]')); //属性选择器
    
        // console.log($('input[type!="button"]')); //属性过滤选择器
    
        // $('li[class^="li1"]').css('background','red');//li1 || li1-开头的
### 2.nth-of-type

$("span:nth-of-type(2)").css('background','red');

### 3.伪类选择器

伪类选择器：

        odd奇数：1,3,5,7,9  js计数从0开始（看上去是偶数）
        even偶数:0,2,4,6,8  js计数从0开始（看上去是奇数）
        eq(下标)找指定范围的元素
    
    */
      // $('li:odd').css({background:'red'})
      // $('li:even').css({background:'yellow'})
      // $('li:eq(2)').css({background:'green'})
    
    /*
       gt(num)  大于num的元素（不包含num）
       lt(num)  小于num的元素（不包含num）
    */  
      $('li:gt(2)').css({background:'yellow'});
      // $('li:lt(3)').css({background:'pink'});
      // console.log($('li'));
### 4.看看是否动态

//如果只获取一次，那么是静态的

    var li = $('li');
    for(var i=0;i<li.length;i++){
      $('#ul').append(li[i]);
    }
### 5.checked

// ***重点***

    // console.log($('input:checked').eq(0))//JQ对象
    //console.log($('input:checked')[0])//原生对象
    
    /*
      如果你要使用jq的方法，那么必须保证，前面那个对象是JQ对象
    
      JQ对象转原生对象使用下标即可
      原生对象转JQ对象用$()包一下即可
### 6.属性操作

    innerHTML   ->  html()
    style.css/cssText    ->  css()
    innerText   ->  text()
    value  ->  val()
    
    attr 属性 -> getAttribute + setAttribute
    
    removeAttr 删除行间属性
    $('#box').html('78910jQk');
         $('#box').html('<p>pppp</p>'); //写操作
    
        console.log($('#box').html()) //读操作
    
      // $('#box').text('<p>pppp</p>');//专门获取文本的
    
      // $('input').val('呵呵');
      css:
          一个参数
            (1)字符串是获取
            (2)对象（批量设置）
    
          两个参数是设置
### 7.点击选择

    checked = true/false
    prop:专门用来操作表单元素属性的（比如:checked）。
    因为直接使用attr('checked')为undefined
​		例子

	$('input[type="button"]').click(()=>{
	  	let inputs = $('input[type="checkbox"]');  
	  for(var i=0;i<inputs.length;i++){
	  	if(inputs.eq(i).prop('checked')){
	  		inputs.eq(i).prop('checked',false)
	  	}else{
	  		inputs.eq(i).prop('checked',true)
	  	}
	  }
	   })
### 8.each

    JQ.each():  
      JQ的循环,里面有个回调函数
      function (i,e){}  ,i->index  e->element
      */
    
      $('li').each((i,e)=>{
      //console.log(e); //原生对象
    $(e).click(function(){
      $('li').eq(i).css({
        background:'red'
      });
      // $(this).css({
      //   background:'red'
      // })
    });
      });
  ### 9.DOM

      DOM:
      文档对象模型
      根据document提供的API，赋予开发者操作页面的能力。
       第一个元素  first()
      最后一个元素  last()
      兄弟元素 
        next
        prev
        siblings
      增、删、改、查
      父级
      子级
      / $('li').last().css('background','red') //first()
      //$('li').eq(0).css('background','red');
    
      // $('li').eq(0).next().css('background','red')
      // $('li').last().prev().css('background','green');
      $('li').eq(0).siblings().css('background','yellow');
   ### 10.index

    添加class  
      addClass()
    删除class
      removeClass()
    
    找到当前元素所在的位置（在父级同级兄弟元素中的位置）
    JQ.index(可以选填范围)
### 11.隐藏

    hide:隐藏  -> display:none
    show:显示  -> display:block

### 12.closest

    closest():  
      closest会首先检查当前元素是否匹配，如果匹配则直接返回元素本身
      如果不匹配则向上查找父元素，一层一层往上，直到找到匹配选择器的元素。
      如果什么都没找到则返回一个空的jQuery对象。
      */
     $('#p2').closest('.a').css('background','red');
  ### 13.find

    //$('#ul').children().css('background','red');
    (1):
      获取元素的方式，会先找li再去找#ul2，那么性能会差很多
    代码缓存：
      先使用find把大模块缓存起来，然后从这个代码块下去获取，节省性能
      //$('#ul2 li').css('background','red');  //(1)
    
      let ul2 = ('#ul2');
    
      $ul2.find('p').css('background','red')


 ### 14.增删改    


        创建元素： 
         	$('标签')
        插入元素：
            append()  最后添加
    
            插入什么东西.insertBefore.要插入到哪个前面
    
            父级.prepend(插入的元素) -> 结果添加到第一个上
    
        删除：
            $(xx).remove(); 
  			例子

     $('#txt').keyup(function(ev){   
        if(ev.keyCode == 13){
            let $li = $(`<li>${$('#txt').val()}</li>`);
            //$('ul').append($li);
            // $li.insertBefore('li:first');
            $('ul').prepend($li);
            $('#txt').val('');
        }
    });
    
    $('ul').on('click','li',function(){
        $(this).remove();
    });

### 15.sizzle

sizzle是选择器，JQ中集成了它

console.log(Sizzle('#box'));//Array(1){0:div#box,1:length:1}

### 16.JQ架构

    无new化操作    
        因为打算在使用jQuery的时候不在外面new，我们使用了
        在jQuery函数内部new，但是出现了一个问题，递归！
    
        问题：
            如何才能做到既能够在内部new，又不递归？
            如何才能做到在内部new还能使用jQuery实例化对象的方法？
    回答：
            只要不new jQuery本身就不会递归,
            那么找一个炮灰来new,只要让炮灰拥有jQuery的
            属性或者方法，是不是new 炮灰就等同于new jQuery

    (function(global,factory){    
        "use strict"
        factory(global);
    })(typeof window !== 'undefined'?window:this,function(window,noGlobal){
        function jQuery(selector){
    
            return new fn(selector);
    
        };
        jQuery.prototype = {
    
            constructor:jQuery,
    
            css:function(){
                console.log(123);
            }
    
        }
    
        let fn = jQuery.prototype.paohui = function(selector){
            
        }
    
        fn.prototype = jQuery.prototype;
    
        window.$ = window.jQuery = jQuery;
    });
    
    function jQuery(){
        alert(1)
    }
    
    // let v = new jQuery('#box');
    
    let v = $('#box');
    
    // console.log(jQuery);
    v.css();    
1. ### 17.函数覆盖       

2.     预解析：        
               c = function c(){
               };
               window.c
       
           逐行解读代码:
               到了第27行，赋值10
          alert(c);
       window.c = 10;
       function c(){
       
       };
       alert(c)//10 ,不会是函数        

### 18.undefined的问题

    在低版本浏览器中undefined是可以为变量的    
        如果需要使用到undefined，并且undefined之前已经被赋值了
        那么undefined无效。
    */
    var undefined = 10;
    var a;
    
    alert(a == undefined);//低版本false    高版本true
### 19.jQ获取宽高

        width()
        height()
        innerWidth/innerHeight  (包含padding,不包含border)
        outerWidth/outerHeight(包含padding,包含border)
    
        outerWidth可以支持margin 在第二个参数上加true
    */
       console.log($('#box').width());
    
    // console.log($('#box').innerWidth());
    
    // console.log($('#box').innerWidth());
    
    console.log($('#box').outerWidth(400,true));
### 20.jQ距离

    	offset().left / top  : 绝对位置    
        position().left / top : 相对于定位父级的距离
        $(document).scrollTop/scrollLeft 滚动的距离
        document.onclick = function(){
           console.log( $(document).scrollTop() );
        };
        
        console.log($('#box').offset().top)
        console.log($(document).scrollTop())
### 21.按需加载

    let li = ('li'); 
    $(document).scroll(ljz);
    ljz();
    function ljz(){
        $li.each(function(i,e){
            if($(e).offset().top <= $(window).innerHeight() + $(document).scrollTop() && $(e).find('img').attr('_src')){
                $(e).find('img').attr('src', $(e).find('img').attr('_src') );
                $(e).find('img').removeAttr('_src');
                $(e).find('img').css({opacity:1});
            }
    
        });
    } 
### 22.事件

    jQ中的事件都是事件绑定，所有的事件都是基于on()    
        click()
        mouseover()
        mouseout()
    当div1绑定的时候，点一次就绑定一次div2的事件
            点几次div1，就绑定几次div2，所以触发div2的时候会触发若干次。
            
            off() 解除绑定,在哪个元素上解除就在那个元素后添加。
    $('#div1').on('click',function(){   
       console.log(111111);
       $('#div2').off().click(function(){
            alert('我是div2');
        });
    
    });
    $('#div2').off().click(function(){
            alert('我是div2222222');
        });
    $('#div1').on('click.hehe',data,function(ev){	
    	console.log(ev)
        console.log(ev.data);
    });
    
    $('#div1').on('click.点击',function(ev){
        console.log(11234567);
    });
    
    $('#div2').on('click',function(ev){
        $('#div1').trigger('click.hehe');
    });
    
       $('#div2').on('click',function(ev){
           $('#div1').off('click.点击');
       });    
​			例子：选型卡

    let btns = ('input');
    
      let divs = ('div');
    
      $btns.on('click',{data:[11111,2222,3333]},function(ev){
    
    $btns.removeClass('active');
    $(this).addClass('active');
    $divs.text(ev.data.data[$(this).index('input')]);
     });
 			例子：拖拽

    $('#div1').mousedown(function(ev){    
        // console.log(ev);
        let disX = ev.clientX - $(this).offset().left;
        let disY = ev.clientY - $(this).offset().top;
    
        $(document).mousemove(function(ev){
            $('#div1').css({
                left : ev.clientX - disX,
                top : ev.clientY - disY
            });
        });
    
        $(document).mouseup(function(){
            $(document).off();
        });
        return false;
    });
### 23.运动

    slow","normal", or "fast"
    jQ中的运动都基于 animate()
    delay() 延迟
    $('button').click(function(){
    
    //    $('#div1').hide('fast');
    
    //    $('#div1').toggle(500);  //宽高透明度
    
    //     $('#div1').slideDown(500);//?????????????
    
    //     $('#div1').slideToggle(800); //改变高度
    
    // $('#div1').fadeToggle(800); //透明度
    $('#div1').animate({
        width:300,
    },500).delay(1000).animate({
        height:600,
    });
     });
### 24.运动问题    


    队列概念：   
       JQ中的运动都是按照队列来排列的
       1,2, [3,4,5]	
    	小技巧：
            如果会多次触发运动，那么在运动前加 stop(true,true) 
        2个true的时候，立即完成上次一次任务，然后开始本次任务
       $('button').click(function(){
    
         $('#div1').stop(true,true).toggle(500);  //宽高透明度
    
      });
    


 

 