# 接受请求
## 处理器和处理函数
如果开发者，创建一个处理器并将它与服务器进行绑定，一次代替原来正在使用的默认多路复用器。这意味这服务不会再通过URL匹配来将请求路由至不同的处理器
，二十直接使用同一个处理器来处理所有请求，因此，不论浏览器访问什么地址，服务器都返回同样的响应。  
但是我再WEB应用绝大多数使用多路复用器，原因：对某些特殊用的服务器来说，只使用一个处理器也许就可以很好地完成工作量；但是不同URL有不同需求，而不是
一成不变地只返回一种响应。  
### 使用多个处理器
为了使用多个处理器，不通过Server结构的Handler字段指定处理器，而是让服务器使用默认的DefaultServeMux作为处理器，然后通过http.Handle函数将处理器
绑定到DefaultServeMux.Handle函数来源于http包，但它实际上是ServeMux结构的方法：这些函数是为了操作便利而创建的函数，调用它们等同于调
用DefaultServeMux的某个方法。比如这里调用http.Handle实际就是再调用DefaultServeMux的Handle方法。  
### 处理器函数
实际上就是与处理器拥有相同行为的函数：这些函数与ServeHTTP方法拥有相同的签名，即，它们接收ResponseWriter和指向Request结构的指针作为参数。
[详细代码点击](handlefunc.go)处理器函数实现原理：GO语言有一种HandleFunc函数类型，它可以把一个带有正确签名的函数F转换成一个带有方法F的
Handler
### ServeMux和DefaultServeMux
ServeMux是一个HTTP请求多路复用器，它负责接收HTTP请求并根据请求中的URL将请求重定向到正确的处理器。
![通过多路复用器将请求转发给各处理器](mux.jpg)
ServeMux结构包含了一个映射，这个映射会将URL映射至相应的处理器。因为ServeMux结构也实现了ServeHTTP方法，所以他也是一个处理器。
当ServeMux的ServeHTTP方法接收到一个请求的时候，它会在结构的映射里找出与被请求URL最为匹配的URL，然后调用与之相对应的处理器的ServeHTTP方法。  
工作原理如下：  
![多路复用器的工作原理](muxrule.jpg)
