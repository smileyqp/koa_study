## koa中间件

- 中间件就是匹配路由之前或者匹配路由完成的一系列操作我们将其成为中间件
- koa中的中间件的功能包括：
  - 执行任何代码
  - 修改请求和响应对象
  - 中介请求响应循环
  - 调用栈中的下一个中间件
  - 中间件通过next()来实现，没有next参数那么就匹配上一个路由就不会往下匹配

#### koa中中间件可以分为以下几种

- ##### 应用级中间件

  ```shell
  //应用级中间件：匹配路由之前做的一系列操作
  /**
   * koa中间件：
   * 1、两个参数表示匹配某个路由
   * 2、一个参数表示匹配所有路由
   */
  
   //匹配所有路由
  app.use(async(ctx,next)=> {
      console.log(new Date());
      await next();      //表示当前路由匹配完成之后继续向下匹配；如果没有next()那么不会往下匹配
  })
  ```

- ##### 路由级中间件

  ```shell
  //二：路由级中间件：匹配到路由之后继续匹配
  
  router.get('/new',async(ctx,next)=>{
      console.log('news')
      await next();
  })
  router.get('/new',async(ctx,next)=>{
      ctx.body = 'new';
  })
  ```

  

- 错误处理中间件

  ```shell
  
  ```

  