Go Laravel Session
========================

<a href="https://travis-ci.org/chekun/golaravelsession"><img src="https://api.travis-ci.org/chekun/golaravelsession.svg?branch=master&style=flat-square" alt="Build Status"></a>

使用Golang从Laravel的cookie中读取SessionID以及解析php-serialize过的内容。

### 功能点

- 解析SessionID (暂只支持Laravel默认的`AES-256-CBC`加密方式)
- 解析php-serialize的Session数据内容

### 使用场景

- WebSocket授权
- 其它

### 例子

- GetSessionID

```go
cookie := "eyJpdiI6IjVrTVVDSmlyb1FtN2NrbmlOTllOUkE9PSIsInZhbHVlIjoiUU9pbCtMTjhQQnQyamJ6ZE5qenVWanhuZktUcjBkOUVsWU5ibkhlWHJyc25DNnZYQlRrOWlFd01ObVJwam1yVUtNcGRUanV1aEJIWHBsYXNiZytNenc9PSIsIm1hYyI6ImMzYzVmMGE1NWY5ZjEzMzRjOTVkN2FlZGY2YzZhNDExOTVhZjUzMjYzZmE3OTE1ODIwYWYzNmY5ODQzYjIwOGEifQ=="
key := "base64:qsDvCdhT+JPXEBD3ys/XraOXVNpshsyElzJmtgnBqEI="

sessionID, _ := GetSessionID(cookie, key)
fmt.Println(sessionID)
//produces: RYodG5AekDidQCVLvs4fQIRAPSwarZV26U4shNVX
```

- ParseSessionData

this is just wrapper usage of package 
[`github.com/yvasiyarov/php_session_decoder/php_serialize`](https://github.com/yvasiyarov/php_session_decoder/tree/master/php_serialize)

```go
sessionData := `a:5:{s:6:"_token";s:40:"eE5gVNqGSn6wneCJAzhtTMulPFwvOfDyZRSoVStA";s:3:"url";a:0:{}s:9:"_previous";a:1:{s:3:"url";s:29:"https://test.dev";}s:6:"_flash";a:2:{s:3:"old";a:0:{}s:3:"new";a:0:{}}s:52:"login_admin_59ba36addc2b2f9401580f014c7f58ea4e30989d";i:1;}`
session, _ := ParseSessionData(sessionData)
fmt.Println(session["_token"].(string))
```

