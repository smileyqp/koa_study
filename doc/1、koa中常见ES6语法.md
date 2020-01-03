## koa中常见ES6语法

##### let、const块作用域

- let:声明块级作用域的变量
  - 不可重复声明
  - 绑定该块级作用域
  - 不可修改。指的是其存储地址不可以改变，但是其数据结构是可以修改的
  - 不可在其声明之前使用
- const声明块级作用域常量

#### 模板字符串

```shell
var name = 'smileyqp';
console.log(`My name is ${name}`)
```

#### 方法 的简写和属性的简写 		

- 方法的简写

  ```shell
  var name = 'smileyqp';
  var obj = {
  	name		//这里直接简写成name；在之前需要写成 name:name
  }
  ```

- 方法的简写

  ```shell
  //简写后
  var obj = {
  	name:'smileyqp',
  	run(){
  		console.log(`${this.name} is running`)
  	}
  }
  //简写之前
  var obj = {
  	name:'smileyqp',
  	run:function (){
  		console.log(`${this.name} is running`)
  	}
  }
  obj.run();
  ```

#### 箭头函数

```shell
//箭头函数中this指向上下文
setTimeout(()=>{
	console.log('smileyqp')
},1000)
```

#### 外部获取异步方法中的数据（callback||Promise）

```shell
//callback
function getData(callback){
	setTimeout(function(){
		var name = 'smileyqp';
		callback(name);
	},1000);
}
getData(function(data){
	console.log(data);			//smileyqp
})
```

```shell
//Promise
//写法一
var p= new Promise(function(resolve,reject){
	setTimeout(function(){
		var name = 'smileyqp';
		resolve(name);
	},1000);
});
p.then((data)=>{
	console.log(data);	//smileyqp
})

//写法二：
function getData(resolve,reject){
	setTimeout(function(){
		var name = 'smileyqp';
		resolve(name);
	},1000);
}
var p= new Promise(getDate);
p.then((data)=>{
	console.log(data);		//smileyqp
})
```























































