# 簡易な HTTP サーバ

単に GET リクエストのみを受け付けるサーバ機能であれば数行のコーディングで実現できる。

```go
package main

import (
	"io"
	"net/http"
)

func infoHandler(w http.ResponseWriter, req *http.Request) {
	io.WriteString(w, "Hello, Go Server!")
}

func main() {
	http.HandleFunc("/info", infoHandler)
	http.ListenAndServe(":8080", nil)
}
```
