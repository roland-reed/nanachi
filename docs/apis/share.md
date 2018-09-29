# 分享

## onShareAppMessage(Object)

在 Page 中定义 onShareAppMessage 函数，设置该页面的分享信息。

- 每个 Page 页面的右上角菜单中默认会显示“分享”按钮，重写了 onShareAppMessage 函数，只是自定义分享内容
- 用户点击分享按钮的时候会调用（`<button>` 组件 open-type="share"）
- 此事件需要 return 一个 Object，用于自定义分享内容。

> 注意：只有定义了此事件处理函数，右上角菜单才会显示“转发”按钮

**Object 参数说明**

| 参数       | 类型   | 说明                                                                                     | 支持平台 |
| ---------- | ------ | ---------------------------------------------------------------------------------------- | -------- |
| from       | string | 转发事件来源。`button`：页面内转发按钮；`menu`：右上角转发菜单                           | 都支持   |
| target     | Object | 如果 `from` 值是 `button`，则 `target` 是触发这次转发事件的 `button`，否则为 `undefined` | 都支持   |
| webViewUrl | String | 页面中包含`<web-view>`组件时，返回当前`<web-view>`的 url                                 | 微信     |

此事件需要 return 一个 Object，用于自定义转发内容，返回内容如下：

**自定义转发内容**

| 字段     | 是否必须 | 说明                                                                                                        | 支持平台 |
| -------- | -------- | ----------------------------------------------------------------------------------------------------------- | -------- |
| title    | 是       | 自定义分享标题                                                                                              | 都支持   |
| path     | 是       | 转发路径 必须是以 / 开头的完整路径                                                                          | 都支持   |
| imageUrl | 否       | 自定义图片路径，可以是本地文件路径、代码包文件路径或者网络图片路径。支持 PNG 及 JPG。显示图片长宽比是 5:4。 | 都支持   |
| desc     | 否       | 自定义分享描述最大长度 140 个字                                                                             | 支付宝   |
| content  | 否       | 自定义吱口令文案，最多 28 个字符                                                                            | 支付宝   |
| bgImgUrl | 否       | 自定义分享二维码的背景图，建议大小 750\*1350                                                                | 支付宝   |
| success  | 否       | 分享成功后回调                                                                                              | 支付宝   |
| fail     | 否       | 分享失败后回调                                                                                              | 支付宝   |

 示例代码：

```javascript
onShareAppMessage(res) {
    if (res.from === 'button') {
      // 来自页面内转发按钮
      console.log(res.target);
    }
    return {
      title: '小程序示例',
      desc: '小程序官方示例Demo，展示已支持的接口能力及组件。',
      path: 'pages/images/index'
    };
  }
```


## hideShareMenu(Object object)

隐藏转发按钮

**参数**

Object object

| 属性     | 类型     | 是否必须 | 说明                                             | 支持平台 |
| -------- | -------- | -------- | ------------------------------------------------ | -------- |
| success  | function | 否       | 接口调用成功的回调函数                           | 都支持   |
| fail     | function | 否       | 接口调用失败的回调函数                           | 都支持   |
| complete | function | 否       | 接口调用结束的回调函数（调用成功、失败都会执行） | 都支持   |