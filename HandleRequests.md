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
### FORM字段
通过调用Request结构提供的 方法，用户可以将URL、主体或者以上两者记录的数据提取到该结构的Form、PostForm和MultipartForm字段当中。
跟我们平常通过POST请求获取到的数据一样，存储在这些字段里面的数据也是以键值对形式表示的。使用Request结构的方法获取表单数据的一般步骤：
- 调用ParseForm方法或者ParseMultipartForm方法，对请求进行语法分析。  
- 根据步骤1调用的方法，访问响应的Form字段、PostForm字段或MultipartForm字段。[点击查看代码](Form.go)
