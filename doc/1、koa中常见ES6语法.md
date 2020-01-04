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

- 原型链+对象冒充的组合继承

```shell
function Person(name,age){
	//构造函数中的方法和属性
	this.name = name;
	this.age = age;
	this.run = function(){
		console.log(`${this.name}---${this.age}`)
	}
}
//原型链上的属性和方法
Person.prototype.work = function(){}

function Web(name,age){
	Person.call(this，name,age);		//1、对象冒充继承
}
Web.prototype = new Person();	//2、原型链继承

var web = new Web('smileyqp',16);
```

###### 原型链继承和对象冒充集成的优缺点

- 对象冒充继承：`	Person.call(this，name,age);	`

  - 缺点：

    - 没法继承原型链上的属性和方法

      ```shell
      //例如上面的代码
      web.run();		//smileyqp---16
      
      web.work();			//Not Found；因为这是原型链上的方法，对象冒充的方法不可以继承
      ```

- 原型链继承：`Web.prototype = new Person()`

  - 优点：可以继承原型链上的属性和方法

  - 缺点：实例化的时候没法给父类传参

    ```shell
    Web.prototype = new Person();	
    //实例化的时候没有办法将参数`var web = new Web('smileyqp',16)`中参数传给父类进行实例化
    ```

    

#### ES6中定义一个类（class）

```shell
class Person{
	//构造函数
	constructor(name,age){
		this._name = name;
		this._age = age;
	}
	getName(){
		console.log(this._name)
	}
	setName(name){
		this._name = name;
	}
	getInfo(){
		console.log(`name:${this.name};age:${this.age}`)
	}
}

var p = new Person('smileyqp',20);	//实例化会执行构造函数
p.setName('yqp')
p.getName();	//yqp
p.getInfo();	//name:smileyqp;age:20	这个getInfo方法是继承父类的getInfo方法
```

#### ES6中继承(extends、super)

```shell
class Web extends Person{
	constructor(name,age,sex){
		super(name,age);	//实例化自雷的时候将自雷的数据传递给父类
		this.sex = sex;
	}
	proint(){
		console.log(this.sex)
	};
}
var w = new Web('smileyqp',18,'girl');
w.print();	//girl
```



#### ES6中静态方法

```shell
class Person{
	constructor(name,age,sex){		//构造方法
		this.sex = sex;		//属性
	}
	proint(){		//实例方法
		console.log(this.sex)
	};
	
	//静态方法
	static work(){
	
	}
}
//调用静态方法
Person.work();


//ES6中也可以直接给类绑定一个静态方法
Person.instance = '这是一个实例,这是一个静态方法';

console.log(Person.instance)
```

#### 单例模式

###### 有多个实例的时候构造函数只调用一次

```shell
class Db{
    static getInstance(){       //单例
        if(!Db.instance){
            Db.instance = new Db();
        }
        return Db.instance;
    }
    constructor(){
        console.log('实例化会触发构造函数！')
        this.connect();
    }

    connect(){
        console.log('连接数据库！')
    }
    find(){
        console.log('查询数据库！')
    }
}

//d1会进入构造函数；实例化d2和d3则不会
var d1 = Db.getInstance();
var d2 = Db.getInstance();
var d3 = Db.getInstance();
```



































