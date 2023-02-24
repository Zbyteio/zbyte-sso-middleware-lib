# How to use this package

1. Install the package
	
	`go get github.com/Zbyteio/zbyte-sso-middleware-lib`

2. Use the new keycloak access token verification as follows
```go
srv.GET("/a", func(ctx *gin.Context) {
  access_token := ctx.GetHeader("Authorization")
	isValid, err := middleware.MiddlewareHandler.verifyOffline(access_token, "https://appdev.zbyte.io/keycloak-poc/")
	if err != nil {
		ctx.JSON(http.StatusBadRequest, gin.H{
			"error" : err.Error(),
		})
		return
	}
	ctx.JSON(http.StatusAccepted, isValid)
})
```