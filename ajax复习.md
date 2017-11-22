## ajax复习

### 1.完整的URL

				search 查询数据 发送给服务端
				hash 不发送给服务端 定位本页面资源
				
				
				let xhr = new XMLHttpRequest();
	
			let url = '127.0.0.1/miaov/1.php'
	
			xhr.open('get',url,true);
	
			xhr.onload = function (){
				// ajax请求回来后触发这个事件	
			}

### 2.同步异步

			// 异步的  不会立马得到结果，而是在未来的某个时刻得到结果
			// 同步 立马要得到结果,在进行之后的操作

### 3.localstorage数据持久化

			// localStorage 全局的对象
			/*
				setItem(key,value)
				getItem(key)   没有取到返回null
				removeItem(key)				
			*/
			let num = localStorage.getItem('abc');
				let list = localStorage.getItem('list');
	
				console.log(JSON.parse(list));
	
	
				let a = num || 10;
				document.onclick = function (){
					a++;
					console.log(a);	
	
					localStorage.setItem('abc',a);
					// 存的是对象，都会转成字符串
					localStorage.setItem('list',JSON.stringify({num:a}))
					localStorage.setItem('list',JSON.stringify([{num:a}]))
				}
