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
### MultipartForm字段
为了取得multipart/form-data编码的表单数据，我们需要用到Request结构的ParseMultipartForm方法和MultipartForm字段，而不再使用ParseForm
方法和Form字段，不过ParseMultipartForm方法在需要时也会自行调用ParseForm方法。PostForm只会返回表单键值对而不会返回URL键值对。  
Formvalue方法和PostFormValue方法都会在需要时自动取调用ParseMultipartForm方法，因此用户并不需要手动调用ParseMultipartForm方法，但这里
也有一个需要注意的地方，如果你将表单的enctype设置成了multipart/form-data，让后尝试通过FormValue方法或者PostFormValue方法来获取键的值，
那么即使这两个方法使用了ParseMultipartForm方法，你也不会得到任何结果。因为过FormValue方法和PostFormValue方法分别对应Form字段和PostForm
字段，表单使用multipart/form-data编码时，表单数据将被存储到MultipartForm字段而不是以上两个字段中。  

|字段|需要调用的方法或需要访问的字段|URL|表单|URL编码|Multipart编码|
| :--- | :--- | :--- | :--- | :--- | :--- |
|Form|ParseForm方法|√|√|√|——|
|PostForm|Form字段|——|√|√|——|
|MultipartForm|ParseMultipartForm方法|——|√|——|√|
|FormValue|无|√|√|√|——|
|PostFormValue|无|——|√|√|——|

### ResponseeWriter
ServeHTTP函数的两个参数传递的都是引用而不是值——虽然ResponseWriter看上去像是一个值，但实际却是一个带有结构指针的接口。ResponseWriter
接口拥有以下三个方法：
- Write;
- WriteHeader;
- Header;
