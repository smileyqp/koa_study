## async和await（ES7）

async是异步的简写；await可以认为是async wait的简写

- async用于声明一个function是异步的

```shell
async function getData(){
	return 'smileyyqp';
}
console.log(getData());		//返回一个Promise；异步方法
```

- await用于等待一个异步方法执行完成

#### 如何获取异步方法中的数据

- 方法一：类似回调的方法

```shell
async function getData(){
	return 'smileyyqp';
}

var p = getData();
p.then((data)=>{
	console.log(data);
})
```

- 方法二：await
  - awit是等待异步方法执行完成，可以获取异步方法李慕安的数据，但是必须的用在异步方法里面

```shell
async function getData(){
	return 'smileyqp';
}

async function test(){
	var d = await getData();
	console.log(d)
}
```

#### await阻塞的功能(将异步转换成同步)

```shell
async function getData(){
	console.log(2)
	return 'smileyqp';
}

async function test(){
	console.log(1)
	var d = await getData();
	console.log(d)
	console.log(3)
}
test();
//1 2 3
```

#### 获取异步方法中的数据（返回Promise的方法）

```shell
function getData(){
	return new Promise((resolve,reject)=>{
		setTimeout(()=>{
			var username = 'smileyqp';
			resolve(username);
		},1000)
	});
}
//方法二（New）：
async function test(){
	var data = await getData();
	console.log(data)
}
//方法一（Old）：
var p = getData();
p.then(function(data){
	console.log(data)
})
```

