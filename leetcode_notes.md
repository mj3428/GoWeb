# 力扣刷题笔记
1. 题3，for range循环其实是遍历一个映射，所以大多数的for range会补上一个_符号（空白标识符blank identifer），用于忽略键值。
`for _, i := range map{}map值或者其他可迭代变量`且在map不声明的情况，循环字符串到时候，i其实是一个字节byte类型，一般为ascii码。
另外,你也可以在初声明时，[256]int{},这里256其实也是字符对应byte后的ascii码，最大为256，其实就是隐含表示映射为[string]int{}。  
2. 题4，`make(slice, len, cap)`make创建初始slice，后面为长度和容量，而容量cap是指数组left的起始到数组末尾的长度值，不是下标取值处。  
3. 题6，bytes.buffer{}其实是创建一个纯字符串，可以用于拼接，速度比slice快很多。也比strings.Join快很多。  
4. 题7，涉及计算，用math包，math.MaxInt32还能限制int的字节存储设置，来查看内存的溢出。
5. 题8，当字符串转换成byte之后
```
import (
	"fmt"
)

func main() {
	//s := []string{"abcd"}
	s := "01234a 56789"
	for _, i := range []byte(s){
	    i -= '0'//这里‘0’其实ASCII码0的其实位置,相减之后空格从32变为240
	    fmt.Println(int(i))
	}
}
输出结果：0 1 2 3 4 49 240 5 6 7 8 9
```

