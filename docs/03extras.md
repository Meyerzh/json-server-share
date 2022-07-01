# 附加功能
## 静态文件服务器
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

## 修改端口
您可以使用--port在其他端口上启动JSON服务器.
```bash
json-server --watch db.json --port 3004
```

## 远程模式
您可以加载远程模式。
```bash
json-server http://example.com/file.json
json-server http://jsonplaceholder.typicode.com/db
```

## 生成随机数据
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

> **Tip** 使用 Faker, [Casual](https://github.com/boo1ean/casual), [Chance](https://github.com/chancejs/chancejs) 或 [JSON Schema Faker](https://github.com/json-schema-faker/json-schema-faker)等模块。[Mock.js](http://mockjs.com/)


## HTTPS
在开发中设置 SSL 的方法有很多。一种简单的方法是使用[hotel](https://github.com/typicode/hotel)。
