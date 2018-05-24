# env 值的获取

`if (process.env.NODE_ENV === 'dev') {
    // dev
} else {
    // build
}`

`"cross-env BUILD_EVN='sit' gulp"`

// 通过node的process模块来取得npm run 的关键字

例如：`var ENV = process.env.NODE_ENV`

更多的node模块如下：

[node的api](http://nodejs.cn/api/process.html/)

