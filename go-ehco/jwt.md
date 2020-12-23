# JWT

- Json Web Token
- Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Token
- 토큰 자체를 정보로 사용하는 방식 (Self-Contained)
- Header.Payload.Signature 구조

### 처리 단계

1. 애플리케이션 실행
2. 사용자에게 해당 토큰이 존재하는 지 확인, 있을 경우 허가
3. 없을 경우 JWT 발행 및 전송
4. 사용자가 Token을 받아서 저장
5. 후에 데이터 요청을 할때 Token과 함께 요청

### 구조

#### Header

```
{
    "alg": "HS256",
    "typ": JWT
}
```

- Signature를 해싱하기 위한 알고리즘 지정
- typ: 토큰의 타입을 지정
- alg: 알고리즘 방식을 지정

#### Payload

```
{
    "iss": "jinho.shin",
    "iat": "1586364327"
}
```

- 토근에서 사용할 정보의 조각들 (Claim)
- 등록된 클레임: 토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터
- 공개 클레임: 사용자 정의 클레임, 공개용 정보를 위해 사용
- 비공개 클레임: 서버와 클라이언트 사이에 임의로 지정한 정보 저장

#### Signature

- 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드

#### echo에서 구현

```go
package main

import (
	"net/http"
	"time"

	"github.com/dgrijalva/jwt-go"
	"github.com/labstack/echo/v4"
	"github.com/labstack/echo/v4/middleware"
)

func login(c echo.Context) error {
	username := c.FormValue("username")
	password := c.FormValue("password")

	// Throws unauthorized error
	if username != "yoel" || password != "123" {
		return echo.ErrUnauthorized
	}

	// Create token
	token := jwt.New(jwt.SigningMethodHS256)

	// Set claims
	claims := token.Claims.(jwt.MapClaims)
	claims["name"] = "Leeeeeoy"
	claims["admin"] = true
	claims["exp"] = time.Now().Add(time.Hour * 72).Unix()

	// Generate encoded token and send it as response.
	t, err := token.SignedString([]byte("secret"))
	if err != nil {
		return err
	}

	return c.JSON(http.StatusOK, map[string]string{
		"token": t,
	})
}

func accessible(c echo.Context) error {
	return c.String(http.StatusOK, "Accessible")
}

func restricted(c echo.Context) error {
	user := c.Get("user").(*jwt.Token)
	claims := user.Claims.(jwt.MapClaims)
	name := claims["name"].(string)
	return c.String(http.StatusOK, "Welcome "+name+"!")
}

func main() {
	e := echo.New()

	// Middleware
	e.Use(middleware.Logger())
	e.Use(middleware.Recover())

	// Login route
	e.POST("/login", login)

	// Unauthenticated route
	e.GET("/", accessible)

	// Restricted group
	r := e.Group("/restricted")
	r.Use(middleware.JWT([]byte("secret")))
	r.GET("", restricted)

	e.Logger.Fatal(e.Start(":1323"))
}
```
