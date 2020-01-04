## nodejs操作mongodb数据库

- 安装mongodb

  ```shell
  npm install mongodb --save
  ```

- 引入mongodb下面的MongoClient

  ```shell
  const MongoClient = require('mongodb').MongoClient;
  ```

- 定义数据库连接地址以及配置数据库koa数据库的名称

  ```shell
  // Connection URL
  const url = 'mongodb://localhost:27017';
  
  // Database Name
  const dbName = 'myproject';
  ```

- nodejs连接数据库

```shell
// Create a new MongoClient
const client = new MongoClient(url);

// Use connect method to connect to the Server
client.connect(function(err) {
  assert.equal(null, err);
  console.log("Connected successfully to server");

  const db = client.db(dbName);

  client.close();
});

```

- 操作数据库