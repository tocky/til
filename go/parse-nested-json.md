# ネスト構造の JSON を Request Body から構造体に入れる

以下のコードは、GCP (Google Cloud Platform) の GAE (Google App Engine) 上で動作するもので、Cloud PubSub からの Push を受け付ける想定となっている。ただの検証用コードなので実際には注意すべき点はたくさんある。

Cloud PubSub では Push 配信と Pull 配信とがあるが、GAE 上のワーカーでは Push による動作が好ましいようだ。配信に関しては[オフィシャルドキュメント](https://cloud.google.com/pubsub/docs/subscriber)を参考にすると良い。

```go
package worker

import (
	"net/http"

	"github.com/labstack/echo"
	"google.golang.org/appengine"
	"google.golang.org/appengine/log"

	"encoding/json"
	"io/ioutil"
)

func init() {
	e.POST("/push", handlerPushPost)
}

type (
	PubSubPush struct {
		Subscription string  `json:"subscription"`
		Message      Message `json:"message"`
	}

	Message struct {
		Data        string            `json:"data"`
		MessageID   string            `json:"message_id"`
		PublishTime string            `json:"publish_time"`
		Attributes  map[string]string `json:"attributes"`
	}
)

func handlerPushPost(c echo.Context) error {
	ctx := appengine.NewContext(c.Request())

	body, err := ioutil.ReadAll(c.Request().Body)
	if err != nil {
		log.Errorf(ctx, "Bad Request: %v", err)
		return echo.NewHTTPError(http.StatusOK, "Bad Request")
	}

	log.Infof(ctx, string(body))

	var p PubSubPush
	err = json.Unmarshal([]byte(body), &p)
	if err != nil {
		log.Errorf(ctx, "Bad Request: %v", err)
		return echo.NewHTTPError(http.StatusOK, "Bad Request")
	}

	log.Infof(ctx, "Struct is %v", p)
	log.Infof(ctx, "subscription:        %v", p.Subscription)
	log.Infof(ctx, "message.data:        %v", p.Message.Data)
	log.Infof(ctx, "message.message_id:  %v", p.Message.MessageID)
	log.Infof(ctx, "message.publis_time: %v", p.Message.PublishTime)

	for k, v := range p.Message.Attributes {
		log.Infof(ctx, "message.attributes.%s: %v", k, v)
	}

	return c.String(http.StatusOK, "")
}
```

---

## 参考

- [GoでJSONをパースするときに考えることになるアレこれ - Qiita](http://qiita.com/taizo/items/97106858c6c1b5c8d06a)
- [Handling JSON Post Request in Go - Stack Overflow](http://stackoverflow.com/questions/15672556/handling-json-post-request-in-go)
- [loops - Iterating over all the keys of a Golang map - Stack Overflow](http://stackoverflow.com/questions/1841443/iterating-over-all-the-keys-of-a-golang-map)
