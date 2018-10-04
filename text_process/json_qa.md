1、问题:使用go语言,把时间戳转为json,然后把json数据,转为map;时间戳变科学计数法<br>
`希望`:在读取数据时,时间戳能够正常<br>
`解决方法一`:
```go
func DecodeJSON(strJson string, i interface{}) error {
	d := json.NewDecoder(bytes.NewReader([]byte(strJson)))
	d.UseNumber()
	return d.Decode(i)
}
```
`解决方法二(推荐)`:
```go
var data = `{"id": 12423434, "Name": "Fernando"}`
var m map[string]interface{}
ReadJSON(data, &m)
fmt.Println(m)

id := m["id"]
fmt.Println(id)

var y int = int(id.(float64))//关键就在这里
fmt.Println(y)
func ReadJSON(strJson string, i interface{}) error {
	return json.Unmarshal([]byte(strJson), i)
}
```
2、json字符串的数据类型要一致，否则解析会失败，如
```
`[{"sku":4250627,"buyNum":1},{"sku":4244907,"buyNum":1},{"sku":4229722,"buyNum":1}]`
```
和
```
`[{"sku":"4250627","buyNum":1},{"sku":"4244907","buyNum":1},{"sku":4229722,"buyNum":1}]`
```
下面这个解析会失败的,注意它们的区别sku是否有""
