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





#### 原生JS中的类、静态方法、继承

##### ES5中的实例方法和静态方法

```shell
function Person(name,age){
	//构造函数中的方法和属性
	this.name = name;
	this.age = age;
	this.run = function(){
		console.log(`${this.name}---${this.age}`)
	}
}

//原型链上的属性和方法；可以被多个实例共享
Person.prototype.sex = 'boy';
Person.prototype.work = function(){
	console.log(`${this.name}---${this.age}---${this.sex}`)
}

//静态方法
Person.setName = function(){
	console.log('static function')
}

//实例方法是通过实例化来调用的；静态方法是通过类名直接调用
var p = new Person('smileyqp',18);
p.run();
p.work()

Person.setName();	//执行静态方法
```

#### ES5中的继承

```shell

```















































