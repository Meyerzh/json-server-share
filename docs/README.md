# JSON Server

> [NPM](https://www.npmjs.com/package/json-server) · [Github](https://github.com/typicode/json-server)
[slides-export.pdf](/slides-export.pdf)

## 安装

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


访问地址 http://localhost:3000/

此外，在处理请求时，最好知道：
- 如果您发出 POST、PUT、PATCH 或 DELETE 请求，更改将自动安全地保存到db.json。
- 您的请求正文 JSON 应该是包含对象的，就像 GET 输出一样。（例如{"name": "Foobar"}）
- Id 值是不可变的。
- POST、PUT 或 PATCH 请求应包含Content-Type: application/json在请求正文中使用 JSON 的标头。否则它将返回 2XX 状态码，但不会对数据进行更改。

> 演示用数据 [jsonplaceholder](https://jsonplaceholder.typicode.com/)