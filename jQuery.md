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
