## koa路由

`npm install --save koa-router`安装路由

```shell
var Koa = require('koa');
var app = new Koa();

//引入和实例化路由
var router = require('koa-router')();

//ctx是指上下文context；包含了request和response等信息
//配置路由
router.get('/',async(ctx)=>{
    ctx.body = 'hello';
})

router.get('/news',async(ctx)=>{
    ctx.body = 'news';
})

router.get('/details',async(ctx)=>{ 
    ctx.body = 'details';
})

//启动路由
app
    .use(router.routes())
    .use(router.allowedMethods())       
    //官方建议配置；因为这个是当没有设置享有的时候会根据ctx.status设置响应头


app.listen(3001)
```

```shell
//配置路由也可以这样写
router.get('/',async(ctx)=>{
    ctx.body = 'hello';
}).get('/news',async(ctx)=>{
    ctx.body = 'news';
})
```

#### 获取get传值

##### 在koa2中GET传值通过request接受，但是接受方法有两种：query和querystring	

- query:返回的是格式化好的参数对象
- querystring：返回的是请求字符串

```shell
/**
 * 获取get传值
 * http://localhost:3001/details?aid=123
 */
router.get('/details',async(ctx)=>{
    console.log(ctx.query)      //{ aid: '123' }获取的是对象（推荐）
    console.log(ctx.querystring)    //aid=123   获取的是一个字符串
    console.log(ctx.request.query)      //同上获取query对象
    console.log(ctx.request.querystring)    //同上获取query的字符串

    console.log(ctx.request)    //获取请求相关信息

    //获取url地址
    console.log(ctx.url)
    console.log(ctx.request.url)
    
    ctx.body = 'details';
})
```

#### 动态路由

```shell
/**
 * 动态路由
 * http://localhost:3001/news/23/90
 */
router.get('/news/:aid/:cid',async(ctx)=>{
    console.log(ctx.params) //获取动态路由的返回值{ aid: '23',cid:90 }
    ctx.body = 'news';
})
```

