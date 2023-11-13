## 语言基础

```
新老两种模式
- go module
- go path
```



```
常用基础转
	strconv
		~.Itoa
		~.Atoi
		~.ParseInt(data, base, bitsize)
		~.ParseFloat(~)
	int()

高级带进制转换
	strconv.FormatXxx
```

```
高维护性输出
msg := Sprintf("")


高性能输出
var builder strings.Builder
builder.WriteString("")
...
res := buider.String()

```

```
%v 值
%#v 类型+值
%T 类型

%ns 宽度为n，数据原样输出
```

```
strings
	.Contains(str, substr)
	.Count(str, substr)
	.Split(str, sep)
	.HasPrefix(str, prefix)
	.HasSuffix(str, suffix)
	.Index(str, substr) 查找字串位置
	.Replace(str, old, new, n)
	.ToLower(str)
	.ToUppper(str)
	 
```

![image-20231109122059901](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20231109122059901.png)

```
集合类型
	数组
	列表
	map
	slice
```

