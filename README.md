
# 目录
> 更新时间: 2018-09-05
- [查询列表](#gets)
- [查询详情](#get)
- [修改数据](#edit)
- [新增数据](#add)
- [删除数据](#delete)
- [用户登录](#login)
- [用户登出](#logout)
- [获取导航菜单](#getMenuList)


---


# RESTful接口风格介绍
参数 | 说明
---|---
token | 令牌/密钥，服务端用于识别用户身份信息
result | 返回结果是否成功
message | 提示信息
total | 数据总数
curPage | 当前页数
pageSize | 一页个数
data | 返回的数据


http状态码 | 说明
---|---
200 | 服务器成功返回用户请求的数据
400 | 用户发出的请求有错误，服务器没有进行新建或修改数据的操作
401 | 表示用户没有权限（令牌token、用户名、密码错误）
403 | 表示用户得到授权（与401错误相对），但是访问是被禁止的
404 | 用户发出的请求针对的是不存在的记录，服务器没有进行操作

### 注意事项
- 根据http状态码来做错误捕捉和查询失败/登录超时等交互。
- 接口url分析：```https://www.example.com/api/table ```  服务器域名/api/数据表名
- token在用户登录接口成功后返回存在客户端（浏览器）缓存中，后续请求接口都要把token放在请求头（Headers）里发送给服务端
- 用户登录/注册/修改密码，密码统一用md5加密发送
- IOS端需要调用的接口，接口数据要避免使用键为```id```字段，它是IOS开发的关键词，可以用```ID```或```Id```来代替。

---

<a id = "gets"></a>
# 查询列表
**请求方式：** GET

**请求地址**：```https://www.example.com/api/table?pageSize=10&curPage=1```

**返回结果：**
```js
{
      "result": true,
      "message":'',
      "total":2,
      "curPage": 1,
      "pageSize": 10,
      "data": [{
          "id": 1,
          "name": "zhc",
          "age": 20
        },
        {
          "id": 2,
          "name": "zhc2",
          "age": 21
     }]
}
```

---

<a id = "get"></a>
# 查询详情
**请求方式：** GET

**请求地址**：```https://www.example.com/api/table/1```

**返回结果：**
```js
成功
{
      "result": true,
      "message":'',
      "total":'',
      "curPage": '',
      "pageSize": '',
      "data": {
          "id": 1,
          "name": "zhc",
          "age": 20
        }
}

失败
{     "result": false,
      "message":'请求数据不存在',
      "total":'',
      "curPage": '',
      "pageSize": '',
      "data":{}
}
```

---

<a id = "add"></a>
# 新增数据
**请求方式：** POST

**请求地址**：```https://www.example.com/api/table```

**请求参数：**
```js
{
    "name": "zhc",
    "age": 20,
}
```
**返回结果：**
```js
{   
      "result": true,
      "message":'',
      "total":'',
      "curPage": '',
      "pageSize": '',
      "data":{}
}
```

---

<a id = "edit"></a>
# 修改数据
**请求方式：** PUT

**请求地址**：```https://www.example.com/api/table```

**请求参数：**
```js
{
    "id":1,
    "name": "zhc",
    "age": 20,
}
```
**返回结果：**
```js
{
      "result": true,
      "message":'',
      "total":'',
      "curPage": '',
      "pageSize": '',
      "data":{}
}
```

---

<a id = "delete"></a>
# 删除数据
**请求方式：** DELETE

**请求地址**：```https://www.example.com/api/table/1```

**返回结果：**
```js
{
      "result": true,
      "message":'',
      "total":'',
      "curPage": '',
      "pageSize": '',
      "data":{}
}
```

---

<a id = "login"></a>
# 用户登录
**请求方式：** POST

**请求地址**：```https://www.example.com/api/login```

**请求参数：**
```js
{
    "userName":"admin",
    "password": "123456",//密码统一用md5加密发送
}
```
**返回结果：**
```js
{
    "result": true,
    "message":'',
    "total":'',
    "curPage": '',
    "pageSize": '',
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
# 用户登出

**请求方式：** POST

**请求地址**：```https://www.example.com/api/logout```

**返回结果：**
```js
{
    "result": true,
    "message":'',
    "total":'',
    "curPage": '',
    "pageSize": '',
    "data":{}
}
```

---
<a id = "getMenuList"></a>
# 获取导航菜单
> 获取导航菜单也是获取用户权限接口，决定用户能访问的菜单栏目

**请求方式：** GET

**请求地址**：```https://www.example.com/api/getMenuList?userId=1```

**返回结果：**
```js
{
    "result": true,
    "message":'',
    "total":'',
    "curPage": '',
    "pageSize": '',
    "data":[{
        'icon':'i-icon-home',//菜单图标
        'path':'/home',//菜单跳转地址或路由跳装地址
        'title':'首页',//菜单名称
        },{
        'icon':'i-icon-menu',
        'path':'/menu',
        'title':'菜单栏目',
    }]
}
```

---

