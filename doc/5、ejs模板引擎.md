## ejs模板引擎

` npm install koa-views --save`

`npm install ejs --save`

```shell
var views = require('koa-views');

//配置模板引擎
//app.use('views',{map:{html:'ejs'}})
//两种方法配置模板引擎都可以，上面一种是html结尾；下面一种是ejs结尾
app.use(views('views',{
    extension:'ejs'
}))

router.get('/',async(ctx)=>{
    console.log('/')
    await ctx.render('index')
})
```

```shell
//后台数据前端模板引擎渲染
router.get('/',async(ctx)=>{
    console.log('/')
    let title = 'hello ejs'
    await ctx.render('index',{title:title});        //将title传到前端渲染
})

//前端直接嵌入代码使用
<%=title%>
```

```shell
//可以在中间件中配置一个全局的数据;任何ctx中都可以获取的到
app.use(async(ctx,next) => {
	ctx.state.userinfo = 'smileyqp';
	await next();
})
```

