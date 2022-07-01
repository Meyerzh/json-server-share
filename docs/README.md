# JSON Server

> [NPM](https://www.npmjs.com/package/json-server) · [Github](https://github.com/typicode/json-server)


## 快速开始

全局安装 JSON Server
```bash
npm install -g json-server
```
> npm 查看全局安装的包：npm list -g --depth 0

启动服务
```bash
json-server --watch db.json
```
> 执行这个命令会自动在当前目录下创建`db.json`文件


访问接口 http://localhost:3000/

此外，在处理请求时，最好知道：
- 如果您发出 POST、PUT、PATCH 或 DELETE 请求，更改将自动安全地保存到db.json。
- 您的请求正文 JSON 应该是包含对象的，就像 GET 输出一样。（例如{"name": "Foobar"}）
- Id 值是不可变的。
- POST、PUT 或 PATCH 请求应包含Content-Type: application/json在请求正文中使用 JSON 的标头。否则它将返回 2XX 状态码，但不会对数据进行更改。

> 演示用数据 [jsonplaceholder](https://jsonplaceholder.typicode.com/)
## 路由

### 多数据路由
```bash
GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1
```

### 单数据路由
```bash
GET    /profile
POST   /profile
PUT    /profile
PATCH  /profile
```

### 过滤器
使用 `.`访问深层属性。
```bash
GET /posts?title=json-server&author=typicode # 使用`&`多字段联合查询
GET /posts?id=1&id=2
GET /comments?author.name=typicode # 使用 `.`访问深层属性。
```

### 分页
使用_page和可选地_limit对返回的数据进行分页。
```bash
GET /posts?_page=7
GET /posts?_page=7&_limit=20
```
*默认返回10项*

### 排序
添加_sort和_order（默认升序）
```bash
GET /posts?_sort=views&_order=asc
GET /posts/1/comments?_sort=votes&_order=asc
```

对于多个字段，请使用以下格式：

```bash
GET /posts?_sort=user,views&_order=desc,asc
```

### 切片
添加_start和_end或_limit（X-Total-Count响应中包含标头）
```bash
GET /posts?_start=20&_end=30
GET /posts/1/comments?_start=20&_end=30
GET /posts/1/comments?_start=20&_limit=10
```
与 [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 完全相同。
即[_start, _end): 含_start, 不含_end。

### 运算符
添加`_gte`或`_lte`获取范围。(大于、小于)
```bash
GET /posts?views_gte=10&views_lte=20
```

添加`_ne`以排除值。 (非)
```bash
GET /posts?id_ne=1
```

添加`_like`到过滤器（支持正则表达式）
```bash
GET /posts?title_like=server
```

### 全文搜索
使用 `q`
```bash
GET /posts?q=internet
```


### Relationships
<!-- TODO: 不太懂 -->
要包含子资源，请添加_embed
```bash
GET /posts?_embed=comments
GET /posts/1?_embed=comments
```

要包含父资源，请添加_expand
```bash
GET /comments?_expand=post
GET /comments/1?_expand=post
```

获取或创建嵌套资源（默认为一级，添加自定义路由更多）
```bash
GET  /posts/1/comments
POST /posts/1/comments
```

### 数据库
```bash
GET /db
```

### 主页
返回默认索引文件或服务./public目录
```bash
GET /
```


## 附加功能
### 静态文件服务器
您可以使用 JSON Server 为您的 HTML、JS 和 CSS 提供服务，只需创建一个`./public`目录或用于`--static`设置不同的静态文件目录。
```bash
# use ./public
mkdir public
 echo  ' hello world '  > public/index.html
json-server db.json
```

```bash
# use --static
json-server db.json --static ./some-other-dir
```

### 修改端口
您可以使用--port在其他端口上启动JSON服务器.
```bash
json-server --watch db.json --port 3004
```

### 远程模式
您可以加载远程模式。
```bash
json-server http://example.com/file.json
json-server http://jsonplaceholder.typicode.com/db
```

### 生成随机数据
使用JS而不是JSON文件，可以通过编程方式创建数据。
```js
// index.js
module.exports = () => {
  const data = { users: [] }
  // Create 1000 users
  for (let i = 0; i < 1000; i++) {
    data.users.push({ id: i, name: `user${i}` })
  }
  return data
}
```

```bash
json-server index.js
```

> **Tip** 使用 Faker, [Casual](https://github.com/boo1ean/casual), [Chance](https://github.com/chancejs/chancejs) 或 [JSON Schema Faker](https://github.com/json-schema-faker/json-schema-faker)等模块。

### [Mock.js](http://mockjs.com/)
```js

var data = Mock.mock({
    'users|10': [{
        'id|+1': 1,
        'cname': () => Mock.mock('@cname()'),
        'gender|1': ["男", "女"],
        'birthday': () => Random.date('yyyy-MM-dd'),
        'city|1': ["上海市", "江苏省", "浙江省", "安徽省"],
        'motto': () => Mock.mock('@cparagraph(1, 3)'),
        'score': () => Mock.mock('@integer(60, 100)')
    }]
})

// 输出结果
console.log(JSON.stringify(data, null, 4))

// 输出结果
console.log(JSON.stringify(data, null, 4))

```

### HTTPS
在开发中设置 SSL 的方法有很多。一种简单的方法是使用[hotel](https://github.com/typicode/hotel)。

### 添加自定义路由
创建一个`routes.json`文件。注意每个路由都以`/`开始.
```bash
{
  "/api/*": "/$1",
  "/:resource/:id/show": "/:resource/:id",
  "/posts/:category": "/posts?category=:category",
  "/articles\\?id=:id": "/posts/:id"
}
```