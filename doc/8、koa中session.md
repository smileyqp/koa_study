## koa中session

- session是另外一种记录客户状态的机制，不同的是cookie保存在客户端浏览器中，session保存在服务器上
- 相对于cookie，session更加安全
- 当浏览器访问服务器并发送第一次请求时候，服务器会创建一个session对象，生成一个类似key、value的键值对；然后将key（cookie）返回到浏览器客户端，浏览器下次访问时候携带cookie(key)找到对应的session(value)。客户信息都保存在session中

#### koa中session的使用

- 安装express-session

  ```shell
  npm install koa-session --save
  ```

- 引入express-session

  ```shell
  const session = require('koa-session')
  ```

- 配置中间件：

  ```shell
  app.keys = ['some secret hurr'];		//cookie的签名
  const CONFIG = {
      key: 'koa:sess', 		//默认为cookie的key；可以不管
      maxAge: 86400000,			//cookie的过期时间，需要设置
      overwrite: true, 		//设置没有效果，可以默认   
      httpOnly: true,             //true表示只有服务器端可以获取
      signed: true,           //签名默认
      rolling: false,         //每次访问都去更新session
      renew: true,            //快要过期时候访问重新设置session
  };
  app.use(session(CONFIG, app));
  ```

- 使用

  ```shell
  //设置值
  ctx.session.username = 'smileyqp';
  //获取值
  ctx.session.username
  ```

  