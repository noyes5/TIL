## JWT

디지털 서명의 용도로 사용. HMAC알고리즘 또는 RSA 알고리즘으로 쓰임.

핵심은 내가 만든 웹토큰이 내가 만든 것임을 확인하는 용도.

클레임의 무결성을 확인할 수 있음.

### 구조

xxxxxx-yyyyy-zzzzzzz

Header - Payload - Signature

#### Header

- 사용할 알고리즘과 타입이 들어있다.

```
{
  "alg": "HS256",
  "typ" : "JWT"
}
```

- JSON은 Base64Url로 인코딩 됨
- Base64Url은 암호화/복호화가 가능

#### Payload

- 핵심이 되는 내용(클레임)이 담겨있음.

등록된 클레임 : 필수는 아니지만 권장되는 클레임.

개인 클레임 : 유저 ID 같은 고유값이 들어감.

```
{
  "sub": "subject",
  "name": "abc",
  "admin": true
}
```

페이로드는 똑같이 Base64Url이 인코딩이 됨.

#### Signature

헤더, 페이로드 모두 Base64Url 로 인코딩 된 다음, 개인 키를 사용하여 서명한 전자서명이 들어있다.

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```