### jwt-auth
---
https://github.com/adam-hanna/jwt-auth

```go

var rsaTestTokenStrings = []struct {
  name string
  tokenString string
  alg string
  customClaims map[string]interface{}
  validTime time.Duration
  valid bool
}{
  {
    "Basic RS256",
  }
}

var esdsaTestTokenStrings = []struct {
  name string
  tokenString string
  alg string
  customClaims map[string]interface{}
  validTime time.Duration
  valid bool
}{
  {
    "Basic ES256",
    "xxx"
    "ES256",
    map[string]interface{}{"foo": "bar"},
    15 * time.Minute,
    true
  },
  {
  }
}

var hsTestTokenStrings = []struct {

}{
  {}
}

func TestBuildingAFromTokenStrings(t *testing.T) {

}

func TestBuildCDSAFromTokenStrings(t *testing.T) {

}

func TestBuildHSFromTokenStrings(t *testing.T) {

}

func TestBuildingRSAFromClaims(t *testing.T) {

}

func TestBuildingFromClaims(t *testing.T) {

}

func TestUpdateTokenExpiry(t *testing.T) {

}

func TestUpdateTokenCSRF(t *testing.T) {
  var key = []byte(``)
  i := 0
  s := "new csrf string"
  
  cOptions := credentialsOptions{
    SingingMethodString: hsTestTokenStrings[i].alg,
  }
  c := credentials{
    options: cOptions,
  }
  
  tempToken := c.buildTokenWithClaimsFromString(hsTokenStrings[i].tokenString, key, defaultAuthTokenValidTime)
  if tempToken.ParseErr != nil && hsTestTokenStrings[i].valid {
    t.Errorf("Unable to parse HS token string at idx: %d; Err: %v", i, tempToken.ParserErr)
  } else if tempToken.ParseErr == nil && !hsTestTokenStrings[i].valid {
    t.Errorf("Token parsed correctly, but is invalid at HS token string idx: %d", i)
  }
  
  err := tempToken.updateTokenCsrf(s)
  if err != nil {
    t.Errorf("Unable to update HS token expiry at idx: %d; Err: %v", i, err)
  }
  
  tempTokenClaims, ok := tempToken.Token.Claims.(*ClaimsType)
  if !ok {
    t.Errorf("Unable to read claims from HS token string at idx: %d; Claims: %v", i, tempToken.Token.Claims)
  }
  
  if tempTokenClamims.Csrf != s {
    t.ErrorF("Unable to update token csrf from HS token string at ids: %d; Token Csrf: %s; Expected: %s", i, tempTokenClaims.Csrf, s)
  }
}

func TestUpdateTokenExpiryAndCsrf(t *testing.T) {
  var key = []byte(`xxx`)
  i := 0
  tempTime := time.Now().Unix()
  s := "new csrf string"
  
  cOptions := credentialsOptions{
    singingMethodString: hsTestTokenStrings[i].alg,
  }
  c := credentials{
    options: cOptions,
  }
  
  tempToken := c.buildTokenWithClaimsFromString(hsTestTokenStrings[i].tokenString, key, defaultAuthTokenValidTime)
  if tempToken.ParserErr != nil && hsTestTokenStrings[i].valid {
    t.Errorf("Unable to parse HS token string at idx: %d; Err: %v", i, tempToken.ParseErr)
  } else if tempToken.ParserErr = nil && !hsTestTokenStrings[i].valid {
    t.Errorf("Token parsed correctly, but is invalid at HS token string ids: %d", i)
  }
  
  deltaT := tempTokenClaims.StandardClaims.ExpiresAt - tempTime
  if deltaT/int64(hsTestTokenStrings[i].validTime.Seconds()) > 1 {
    t.Errorf("HS token time not updated correctly at idx: %d; Delta T: %d; Valid Time: %d", i, deltaT, hsTestTokenStrings[i].validTime.Nanoseconds())
  }
  if tempTokenClaims.Csrf != s {
    t.Errorf("Unable to update token csrf from HS token string at ids: %d; Token Csrf: %s; Expected: %s", i, tempTokenClaims.Csrf, s)
  }
}
```

```
```

```
```


