# GO与WEB应用
## URI
RFC3986定义了URL中的保留字符以及非保留字符，所有保留字符都需要进行URL编码：URL编码会把保留字符转换成该字符再ASCII编码中对应的字节值
（byte value），接着吧这个字节值表示为一个两位长的十六进制数字，最后再在这个十六进制数字的前面加上一个百分号（%）。  
*比如：* 空格再ASCII编码中的字节值为32，也就是十六进制中的20.因此经过URL编码处理的空格就成了20%，URL中所有空格都会被替换成这个值。  
## HTTP/2
HTTP/2是一种二进制协议：二进制表示不仅能够让HTTP/2的语法分析变得更为高效，还能够让协议变得更为紧凑和健壮；但与此同时，对那些习惯了使用HTTP
1.X的开发者来说，他们将无法再通过telnet等应用程序直接发送HTTP/2报文来进行调试。  
## WEB应用的各个组成部分
1. 通过HTTP协议，以HTTP请求报文的形式获得客户端输入；  
2. 对HTTP请求报文进行处理，并执行必要的操作；  
3. 生成HTML，并以HTTP响应报文的形式将其返回给客户端。  
为了完成这些任务，WEB应用被分成了处理器(handler)和模板引擎(template engine)这两个部分。  
* 关于模板引擎  
通过HTTP响应报文回传给客户端的HTML是有模板(template)转换而成的，模板里面可能会包含HTML，但也可能不会，而模板引擎则通过模板和数据来生成
最终的HTML。正如之前所说，模板引擎是经由早期的SSI技术演变而来的且可分为静态模板和动态模板。   
 * 静态模板是一些夹杂着占位符的HTML，静态模板引擎通过将静态模板中的占位符替换成相应的数据来生成最终的HTML，这种做法和SSI技术的概念非常相似
   因为静态模板通常不包含任何逻辑代码，或只包含少量逻辑代码，所以也成为无逻辑模板。CTemplate和Mustache都属于静态模板引擎。  
 * 动态模板除了包含HTML和占位符之外，还包含一些编程语言结构。比如条件语句，迭代语句和变量。JSP/ASP/ERM都属于动态模板引擎。  
