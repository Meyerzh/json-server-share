# mock.js
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
```