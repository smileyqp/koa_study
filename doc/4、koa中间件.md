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

- ##### 错误处理中间件

  ```shell
  //三：错误处理中间件
  app.use(async(ctx,next)=>{
    console.log('这是一个错误处理中间件')
      next();
      if(ctx.status == 404){
          ctx.status = 404;
          ctx.body = '页面找不到'
      }else{
          console.log(ctx.url)
      }
  })
  ```
  
  > 注意：执行方式是先console出`这是一个错误处理中间件`；然后继续往下匹配路由执行next()的操作；最后执行完返回执行判断`ctx.status==404`里面的

- ##### 第三方中间件

#### koaz中间件的执行流程（洋葱模型图）

```shell
 //匹配所有路由
app.use(async(ctx,next)=> {
    console.log(new Date());
    console.log('1、这是第一个中间件')
    await next();      
    console.log('5、这是第一个中间件的next下面')
})

app.use(async(ctx,next)=>{
    console.log('2、这是第二个中间件')
    console.log('这是一个错误处理中间件')
    next();
    console.log('4、这是第二个中间件的next下面')
})

router.get('/test',async(ctx,next)=>{
    console.log('3、匹配到test路由')
    ctx.body = 'test';
})

//访问`http://localhost:3002/test`
//执行结果
1、这是第一个中间件
2、这是第二个中间件
3、匹配到test路由
4、这是第二个中间件的next下面
5、这是第一个中间件的next下面
```

