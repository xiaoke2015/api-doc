# api-doc
前后端约定的接口规范

前后端开发的时候，前端一般会通过api发请求给后端来获取数据或者是用来对数据进行一些增删改查，那么前端在开发的时候就需要注意和后端的开发人员约定好接口协议

## 接口命名 

发请求，首先得知道路径也就是相应的 { host }：{ version }/{ moudle }/{ name } 

常用的登陆的路径会写成这个样

```
http://192/168.1.101:8090/v1/user/login
```

## 接口类型
1. get 请求通常是用来获取数据的
2. post 请求通常用来创建或者是提交的

## 接口公共参数

*注意：接口请求时一定要在Header里加 Accept: application/json，否则返回结果不是json*

api相关的公共参数都是通过Header发送的

- app-version App自定义版本
- sys-version 系统版本
- device-type 平台类型：android、ios
- device-id 设备号
- device-token 友盟设备唯一号
- token 用户登录之后获取的凭据
- model 设备信息，iPhone X之类的
- timestamp 时间戳
- nonce 32位随机数
- sign 签名

## sign签名算法
1. 排序，按照key 对参数进行字典升序排列，除sign不参与签名所有公共参数都需要参与签名
2. 拼接字符串，排序好的请求参数, 格式化成 k=v，然后用"&"拼接在一起。注意不包括sign参数，v为原始值而非url编码后的值。
3. 生成签名，md5('k=v&k1=v1&k2=v2appkey');

## 接口返回示例

- 返回成功示例
```JSON
{
  "code": 200,
  "message": "请求成功",
  "payload": {
    "list": []
  }
}
```

- 返回失败示例
```JSON
{
  "code": 4001,
  "message": "请求失败"
}
```
