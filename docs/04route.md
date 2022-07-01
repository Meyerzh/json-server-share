## 添加自定义路由


## 创建路由文件
创建一个`routes.json`文件
```bash
{
  "/api/*": "/$1",
  "/:resource/:id/show": "/:resource/:id",
  "/posts/:category": "/posts?category=:category",
  "/articles\\?id=:id": "/posts/:id"
}
```
> 注意每个路由都以`/`开始.


### Start JSON Server
Start JSON Server with `--routes` option。

  ```bash
  json-server db.json --routes routes.json
  ```

### 访问接口
现在可以使用我们定义好的路由访问接口：

  ```bash
  /api/posts # → /posts
  /api/posts/1  # → /posts/1
  /posts/1/show # → /posts/1
  /posts/javascript # → /posts?category=javascript
  /articles?id=1 # → /posts/1
  ```