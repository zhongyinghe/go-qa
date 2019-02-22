1、如何遍历字符串中的每个字符
```
for _, c := range string {
  ch := fmt.Sprintf("%c",c)
}
//错误的形式有:
string[i]//这样的形式容易得乱码
```

2、在把时间戳这样的数据放入json,然后从json中把它读取出来，则它会转为科学计数法，现在如何把科学计数法转为字符串呢?
```
fmt.Sprintf("%.0f", 科学计数法变量)
```

3、如何获取字符串的长度
```
- 使用 bytes.Count() 统计
- 使用 strings.Count() 统计
- 将字符串转换为 []rune 后调用 len 函数进行统计
- 使用 utf8.RuneCountInString() 统计
```
具体代码:
```
str:="HelloWord"
l1:=len([]rune(str))
l2:=bytes.Count([]byte(str),nil)-1)
l3:=strings.Count(str,"")-1
l4:=utf8.RuneCountInString(str)
fmt.Println(l1)
fmt.Println(l2)
fmt.Println(l3)
fmt.Println(l4)
//结果都是: 9
```
推荐使用:
```
utf8.RuneCountInString(str)
```
因为:
```
str := "Hello, 世界"
fmt.Println("bytes =", len(str)) //bytes = 13
fmt.Println("runes =", utf8.RuneCountInString(str)) // runes = 9
```
