# <h1>基本知识</h1>
## <h2>基本语法</h2>
### <h3>函数</h3>
```
func 函数名(参数名 参数类型) (返回值列表) {
    函数体
}
```
### <h3>方法</h3>
方法是带有接收者（receiver）的函数，接收者可以是结构体类型或其他自定义类型。方法属于接收者类型，可以通过接收者类型的实例来调用。
```
/ 定义一个结构体
type Rectangle struct {
    Width  float64
    Height float64
}

// 为结构体定义方法
func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}
```

## <h2>基本指令及符号</h2>
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

#### <h4> *http.ListenAndServe* </h4>
用于启动一个 HTTP 服务器并监听指定的地址和端口。它会阻塞当前的执行，直到服务器被关闭或发生致命错误。
```
//函数签名
func ListenAndServe(addr string, handler http.Handler) error
```
参数

* addr：一个字符串，指定服务器监听的地址和端口，例如 ":8080" 表示监听所有网络接口上的 8080 端口。
* handler：一个实现了 http.Handler 接口的处理器，用于处理传入的 HTTP 请求。如果传入 nil，则使用 http.DefaultServeMux 作为默认的请求处理器。

<p>返回值</p>

* 返回一个 error，表示服务器启动过程中或运行过程中发生的错误。

#### <h4> *http.ResponseWriter* </h4>
是一个函数定义，用于处理 HTTP 请求。这个函数通常被用作 HTTP 处理程序（handler），当服务器接收到特定的 HTTP 请求时，会调用这个函数来处理请求。
```
\\接口定义
type ResponseWriter interface {
    Header() Header
    Write([]byte) (int, error)
    WriteHeader(statusCode int)
}
```

{"mux"}包
#### <h4> *mux.Router.HandleFunc* </h4>
mux 包中的 HandleFunc 是 mux.Router 提供的方法，用于注册一个处理函数，并可以指定处理函数只处理特定的 HTTP 方法。mux 路由库提供了更强大的路由功能，如路径参数、查询参数、中间件支持等。
```
\\函数签名
func (r *Router) HandleFunc(path string, f func(http.ResponseWriter, *http.Request)) *Route
```

