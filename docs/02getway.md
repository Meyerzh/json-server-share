## Get 请求

| Name     | Url               | Description                        |
| -------- | ----------------- | ---------------------------------- |
| 主页     | `GET /`           | 返回默认索引文件或服务./public目录 |
| 数据库   | `GET /db`         |                                    |
| 全文搜索 | `GET /posts?q=秀` |                                    |



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

