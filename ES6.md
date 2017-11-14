## ES6

### 1.字符串扩展

​	includes()

​            字符串中是否包含某个（段）字符，返回布尔值

​        startsWith(), 

​            字符串中是否以某个（段）字符开头，返回布尔值

​        endsWith()    

​            字符串中是否以某个（段）字符结尾，返回布尔值

### 3.数值扩展

​	Number.parseInt(), Number.parseFloat()

​        Number.isNaN() -> 里面的内容必须是NaN才会是true，不会用Number去转了

   	 Number.isInteger() 用来判断一个值是否为整数

​	// console.log( Number.parseInt('110',2) ) //NaN

​    	// console.log(Number.isNaN(('a'*1)));

​    	// console.log(Number.isNaN('a'));

​    	// Number.isInteger(25) // true

   	 // Number.isInteger(25.0) // true

​    	// Number.isInteger(25.1) // false

   	 // Number.isInteger("15") // false

​    	// Number.isInteger(true) //false

### 3.数组扩展

entries,拿key和value进行遍历

​        只有拥有遍历接口(Symbol.iterator)才能使用for of循环

​    	这个遍历接口可以返回对象，对象中有一个叫做next的函数

​        这个函数需要返回对象

​        {

​            value:xx,

​            done:布尔值（true:停止遍历，false：可以遍历  ）

​        }

#### 例子

```html
let obj = {name:'hehe',age:18};

    // console.log(Object.keys(obj)); [name,age]//把对象的key值放到一个数组中

    //添加遍历器

    // obj[Symbol.iterator] = function(){

    //     let arr = Object.keys(obj); //拿到对象key值[name,age]

    //     let index = 0;

    //     return {

    //         next(){

    //             //如果添加成立就停止遍历

    //             if(index >= arr.length){

    //                 return {

    //                     value:1,

    //                     done:true

    //                 }

    //             }else{

    //                //继续遍历

    //                 return {

    //                     value:{

    //                         val:obj[arr[index]],//obj[arr[0]] -> obj.name

    //                         key:arr[index++] //arr[0++]  name

    //                     },

    //                     done:false

    //                 }

    //             }

    //         }

    //     }

    // }

    Object.prototype[Symbol.iterator] = function(){

        let index = 0;

        let arr = Object.keys(this);

        let _this = this;

        return {

            next(){

                if(index >= arr.length){

                    return {value:undefined,done:true}

                }else{

            

                    return {

                        value:{

                            val:_this[arr[index]],

                            key:arr[index++]

                        },

                        done:false

                    }

                }  

            }

        }

        // console.log(arr);

    }

    // console.log(obj[Symbol.iterator])

    for(let {val,key} of obj){

        console.log(val,key)

    }
```

### 4.对象扩展

 Object.is():

        判断2个值是否相等
        NaN === NaN  //false
        Object.is(NaN, NaN)   //true
        Object.is({},{})  //flase
        Object.is(+0,-0); //flase
从右往左赋值,浅拷贝

    // let obj = Object.assign({name:'ee'},{name:'hh',age:13},{job:'web'});

### 5.symbol

字符串、数字、布尔值、对象、undefined、null、symbol(唯一)

    */

    // let obj = {
    //     "name":"hehe",
    //     // "name":
    // }
    
    // let s = Symbol();
    // console.log(typeof s);
    
    //放到Symbol的对象，默认会用toString转一下
    // const obj = {
    //     toString() {
    //         return 'abc';
    //     }
    // };
    // const sym = Symbol(obj);
    
    // console.log(sym);// Symbol(abc)


    let s1 = Symbol('foo');
    let s2 = Symbol('foo');
    
    // console.log(s1 == s2) // false
    
    var obj = {
        s1,
        s2
    }
    console.log(obj); //key值可以同名
### 6.set

Set():

            里面的内容不能有重复的
    */
    console.log([... new Set(arr)])
     // console.log([...new Set(arr)]);
原生js的写法

    // for(var i=0;i<arr.length;i++){
    //     for(var j=i+1;j<arr.length;j++){
    //         if(arr[i] == arr[j]){
    //             arr.splice(j,1);
    //             j--;
    //         }
    //     }
    // }
    
    // let obj = {};
    // let arr2 = [];
    // for(var i=0;i<arr.length;i++){
    //     if(!obj[typeof arr[i] + arr[i]]){
    //         obj[typeof arr[i] + arr[i]] = 1;
    //         arr2.push(arr[i]);
    //     }
    // }
    // console.log(arr2);