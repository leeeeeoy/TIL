# Routing

- HTTP method, path, handler를 결정
- Echo.Any(path string, h Handler) 형태로 사용

### 사용예시

```go
// Handler
func hello(c echo.Context) error {
  	return c.String(http.StatusOK, "Hello, World!")
}

// Route
e.GET("/hello", hello)
```

- Http method 종류와 경로, 그리고 핸들러를 넣어서 사용

### Route Naming

```go
route := e.POST("/users", func(c echo.Context) error {
})
route.Name = "create-user"

// or using the inline syntax
e.GET("/users/:id", func(c echo.Context) error {
}).Name = "get-user"
```

- 해당 라우터에 이름을 붙일 수 있음
