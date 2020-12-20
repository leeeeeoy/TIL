# Handler

- 요청에 따른 비니지스 처리
- 미들웨어와 라우터를 거쳐 데이터를 처리
- String, HTML, JSON, XML, File 등

## Response

### String

```go
func(c echo.Context) error {
  return c.String(http.StatusOK, "Hello, World!")
}
```

- context.String(code int, s string) 형태로 사용

### HTML

```go
func(c echo.Context) error {
  return c.HTML(http.StatusOK, "<strong>Hello, World!</strong>")
}
```

- context.HTML(code int, html string) 형태로 사용

### JSON

```go
// User
type User struct {
  Name  string `json:"name" xml:"name"`
  Email string `json:"email" xml:"email"`
}

// Handler
func(c echo.Context) error {
  u := &User{
    Name:  "Jon",
    Email: "jon@labstack.com",
  }
  return c.JSON(http.StatusOK, u)
//   return c.JSONPretty(http.StatusOK, u, "  ")
}
```

- struct에서 go type을 json 형태로 선언
- pretty도 사용 가능

### Redirect Request

```go
func(c echo.Context) error {
  return c.Redirect(http.StatusMovedPermanently, "<URL>")
}
```

## Request

### Bind Data(JSON)

```go
// User
type User struct {
  Name  string `json:"name" form:"name" query:"name"`
  Email string `json:"email" form:"email" query:"email"`
}

// Handler
func(c echo.Context) (err error) {
  u := new(User)
  if err = c.Bind(u); err != nil {
    return
  }
  return c.JSON(http.StatusOK, u)
}

// Query parameters
func(c echo.Context) error {
	name := c.QueryParam("name")
	return c.String(http.StatusOK, name)
})

// Path parameters
e.GET("/users/:name", func(c echo.Context) error {
	name := c.Param("name")
	return c.String(http.StatusOK, name)
})
```

- go type에 json type 선언
- Query prameter or path parameter 도 가능
