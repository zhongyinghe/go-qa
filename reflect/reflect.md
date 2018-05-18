1、Elem()该怎么使用?
```
答:在使用Elem()时要使用指针的形式,如:
v := xxx
reflect.TypeOf(&v).Elem()
reflect.ValueOf(&v).Elem()
这里的v必须要取地址:&v,否则会报错
reflect.TypeOf(v).Elem() //报错
reflect.ValueOf(v).Elem() //报错
```
注意区别
```
a := 100
t := reflect.TypeOf(&a).Elem() //这个输出的是变量的类型 int
v := reflect.ValueOf(&a).Elem()//这个输出的是变量的值 100
```
