# Middleware

- 메인 로직의 핸들러(컨트롤러) 앞, 뒤로 추가적인 일을 담당
- 각 핸들러의 전처리 or 후처리를 담당
- 경우에 따라선 미들웨어 스킵 가능
- Http 요청이 들어왔을 때 전반적인 처리 단계

1. 라우트 이전 미들웨어
2. 라우팅
3. 라우트 이후 미들웨어
4. 핸들러 호출
5. 로직 응답 처리

## Root Level

- 모든 핸들러가 수행하는 미들웨어
- Before router와 After router로 나눌 수 있음

### Before router

: ehco.Pre()<br/>
-> 어떤 핸들러로 가는지 결정되지 않았기에 path관련 api 사용에는 제약이 생김

- HTTPSRedirect
- HTTPSWWWRedirect
- WWWRedirect
- NonWWWRedirect
- AddTrailingSlash
- RemoveTrailingSlash
- MethodOverride
- Rewrite

### After router

: ehco.Use()
-> 비지니스 스러운 작업(인증, 리소스 공유 등)을 처리하는 용도

- BodyLimit
- Logger
- Gzip
- Recover
- BasicAuth
- JWTAuth
- Secure
- CORS
- Static

## Group Level

: ehco.Group()

- 특정 주소이 하위패스에만 추가로 미들웨어를 적용하기 위함
- admin이나 단일 컴포넌트에 경우?

## Route Level

: echo.GET("/", <Handler>, <Middleware...>)

- 특정 라우터에만 미들웨어를 적용할 경우
