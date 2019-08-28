# 处理请求
## 请求和响应
* Request结构
  * URL字段；
  * Header字段；
  * Body字段；
  * Form字段、PostForm字段和MultipartForm字段；
### 请求URL
```
type URL struct{
  Scheme    string
  Opaque    string
  User      *Userinfo
  Host      string
  Path      string
  RawQuery  string
  Fragment  string
  }
```
URL一般格式：`scheme://[userinfo@]host/path[?query][#fragment]`  
scheme之后不带斜线的URL则会被解释为：`sheme:opaque[?query][#fragment]`  
