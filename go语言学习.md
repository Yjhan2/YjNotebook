# <h1>基本指令</h1>

### <h3>nil</h3>
nil是一个预定义的标识符，表示没有被初始化或没有指向任何有效的值。
```
    var p *int
    fmt.Println(p) // 输出: <nil>
```

### <h3>defer</h3>
defer 是 Go 语言中的一个关键字，用于延迟执行一个函数或方法，直到包含该 defer 语句的函数返回时才执行。defer 语句通常用于确保资源的释放，例如关闭文件、关闭数据库连接、释放锁等。一般用法为：
```
    file, err := os.Open("example.txt")
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    // 确保在函数返回之前关闭文件
    defer file.Close()
```
当有多个defer语句时，按照先入后出原则返回：
```
func main() {
    defer fmt.Println("First defer")
    defer fmt.Println("Second defer")
    defer fmt.Println("Third defer")

    fmt.Println("Function body")
}
```
输出为：
```
Function body
Third defer
Second defer
First defer
```

## <h2>后端工具</h2>

### <h3>{"net/http"}包</h3>
这是 Go 语言标准库中的一个包，用于构建 HTTP 客户端和服务器。它提供了处理 HTTP 请求和响应的功能，包括路由、处理程序、请求方法、状态码等。([net/http包文档](https://pkg.go.dev/net/http))