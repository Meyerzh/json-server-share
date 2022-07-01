# Mock.js
> http://mockjs.com/
```js

var data = Mock.mock({
    'users|3': [{
        'id|+1': 1,
        'cname': ()=>Mock.mock('@cname()'),
        'gender|1': ["男", "女"],
        'birthday': ()=>Random.date('yyyy-MM-dd'),
        'city|1': ["上海市", "江苏省", "浙江省", "安徽省"],
        'motto': ()=>Mock.mock('@cparagraph(1, 3)'),
        'favsubject|2': {
            'math': {
                "name":"数学",
                "score": ()=>Mock.mock('@integer(60, 100)'),
            },
            'chinese': {
                "name":"语文",
                "score": ()=>Mock.mock('@integer(60, 100)'),
            },
            'english': {
                "name":"英语",
                "score": ()=>Mock.mock('@integer(60, 100)'),
            },
            'pe': {
                "name":"体育",
                "score": ()=>Mock.mock('@integer(60, 100)'),
            },
        }
    }]
})

// 输出结果
console.log(JSON.stringify(data, null, 4))


```
