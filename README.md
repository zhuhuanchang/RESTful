### 目录
- [查询列表](#gets)
- [查询详情](#get)
- [修改数据](#edit)
- [新增数据](#add)
- [删除数据](#delete)
- [用户登录](#login)
- [用户登出](#logout)


---


### RESTful风格设计介绍
参数 | 说明
---|---
token | 令牌/密钥，服务端用于识别用户身份信息
pageSize | 一页个数
currentPage | 当前页数
result | 返回结果是否成功
errCode | 状态码
message | 提示信息
data | 返回的数据


状态码 | 说明
---|---
200 | 服务器成功返回用户请求的数据
400 | 用户发出的请求有错误，服务器没有进行新建或修改数据的操作
401 | 表示用户没有权限（令牌token、用户名、密码错误）
404 | 用户发出的请求针对的是不存在的记录，服务器没有进行操作


- token在用户登录接口成功后返回存在客户端（浏览器）缓存中，后续请求接口都要把token放在请求头（Headers）里发送给服务端
- 用户登录/注册/修改密码，密码统一用md5加密发送
---

<a id = "gets"></a>
#### 查询列表：
method | url
---|---
get | https://www.example.com/api/table?pageSize=10&currentPage=1
###### 返回
```js
{
      "result": true,
      "currentPage": 1,
      "pageSize": 10,
      "errCode": 200,
      "data": [
        {
          "id": 1,
          "name": "zhc",
          "age": 20
        },
        {
          "id": 2,
          "name": "zhc2",
          "age": 21
        }
      ]
    }
```

---

<a id = "get"></a>
#### 查询详情：
method | url
---|---
get | https://www.example.com/api/table?id=1
###### 返回
```js
成功
{
      "result": true,
      "errCode": 200,
      "data": {
          "id": 1,
          "name": "zhc",
          "age": 20
        }
    }

失败
{
      "result": false,
      "errCode": 404,
      "message":"请求数据不存在"
    }
```

---

<a id = "add"></a>
#### 新增数据：
method | url
---|---
post | https://www.example.com/api/table
###### 请求参数
```js
{
    "name": "zhc",
    "age": 20,
    }
```
###### 返回
```js
{
    "result": true,
    "errCode": 200,
    }
```

---

<a id = "edit"></a>
#### 修改数据：
method | url
---|---
put | https://www.example.com/api/table
###### 请求参数
```js
{
    "id":1,
    "name": "zhc",
    "age": 20,
    }
```
###### 返回
```js
{
    "result": true,
    "errCode": 200,
    }
```

---

<a id = "delete"></a>
#### 删除数据：
method | url
---|---
delete | https://www.example.com/api/table?id=1
###### 返回
```js
{
    "result": true,
    "errCode": 200,
    }
```

---

<a id = "login"></a>
#### 用户登录：
method | url
---|---
post | https://www.example.com/api/login
###### 请求参数
```js
{
    "userName":"admin",
    "password": "123456",//密码统一用md5加密发送
    }
```
###### 返回
```js
{
    "result": true,
    "errCode": 200,
    "data":{
        "name":"管理员",
        "photo":'http://www.example.com/images/photo.jpg',
        "token":'132dsadfew54f',
        "id":1
    }
    }
```

---

<a id = "logout"></a>
#### 用户登出：
method | url
---|---
post | https://www.example.com/api/logout
###### 返回
```js
{
    "result": true,
    "errCode": 200,
    }
```

---

