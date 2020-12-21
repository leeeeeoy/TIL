# CORS

- Cross-Origin Resource Sharing, 교차 출처 리소스 공유
- 출처가 다른 자원에 대한 접근 권한 부여

### 허가 방법

#### Access-Control-Allow-Origin response 헤더를 추가

- \*를 세팅하면 모든 출처에서의 요청 허용 -> 후에 이슈 발생 가능
- 출처를 명시해 주면 해당 출처로부터의 요청은 승인

#### middleware에서의 CORS 추가

- middleware를 통해 CORS 설정
- 헤더 추가, 도메인, 포트, 메소드 등을 설정

### ehco 에서 사용

- echo.Use(middleware.CORS())
- Custom Configuration 가능

```go
e := echo.New()
e.Use(middleware.CORSWithConfig(middleware.CORSConfig{
  AllowOrigins: []string{
      "https://labstack.com",
      "https://labstack.net"
      },
  AllowHeaders: []string{
      echo.HeaderOrigin,
      echo.HeaderContentType,
      echo.HeaderAccept
      },
}))
```

```go
CORSConfig struct {
  Skipper Skipper

  AllowOrigins []string `yaml:"allow_origins"`

  AllowOriginFunc func(origin string) (bool, error) `yaml:"allow_origin_func"`

  AllowMethods []string `yaml:"allow_methods"`

  AllowHeaders []string `yaml:"allow_headers"`

  AllowCredentials bool `yaml:"allow_credentials"`

  ExposeHeaders []string `yaml:"expose_headers"`

  MaxAge int `yaml:"max_age"`
}
```
