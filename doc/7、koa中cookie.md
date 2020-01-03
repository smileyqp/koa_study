## koa中cookie

- cookie保存在浏览器客户端
- 可以让我们用同一个浏览器访问同一个域名的时候实现数据共享

#### cookie可以用在哪些地方

- 保存用户信息（http是无状态的）
- 浏览历史记录
- 猜你喜欢
- 一定时长免登陆
- 多个页面数据传值
- 实现购物车功能

#### koa中cookie的使用

- koa中设置cookie的值

  ```shell
  ctx.cookies.set(name,value,[options])
  ```

  - options中的参数有
    - maxAge:一个数字表示从Date.now()得到的毫秒数
    - expires:cookie过期的date
    - path：cookie的路径，默认是`/`
    - domain:cookie域名;默认不要设置，默认是当前域下面的所有页面都可以访问
    - secure：安全cookie，默认`false`设置成`true`表示只有`http`可以访问；`.baidu.com`默认baidu的二级域名都可以访问
    - httpOnly:是否知识服务器可以访问cookie；默认是true
    - overwrite:布尔值；表示是否可以覆盖之前设置的同名cookie，默认是`false`;如果是`true`在同一个请求中设置相同名称的所哟与cookie（不管路径或者域）是否再次设置此cookie时从Setcookie标头中过滤掉

- koa中获取cookie的值

  ```shell
  ctx.cookie.get('smileyqp')		//传入的参数是cookie的name
  ```

  > 注意：koa中没法直接设置中文cookie，可以将其转成base64字符串
  >
  > ```shell
  > //转成base64字符串
  > console.log(new Buffer('smileyq').toString('base64'))
  > 
  > var basestr = new Buffer('smileyq').toString('base64');
  > //还原base64字符串
  > console.log(new Buffer(basestr,'base64').toString())
  > ```

