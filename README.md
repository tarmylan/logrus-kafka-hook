```go
package main

import (
    log "github.com/Sirupsen/logrus"
    kafkahook "github.com/tarmylan/logrus-kafka-hook"
)

func main() {
    addrs := []string{"172.16.10.222:9092", "172.16.10.223:9092", "172.16.10.224:9092"}

    hook, err := kafkahook.NewHook(addrs, "game", "logrus-hook")
    if err != nil {
        log.Fatal(err)
    }   

    log.SetFormatter(&log.JSONFormatter{})
    log.AddHook(hook)

    log.WithFields(log.Fields{
        "foo":    "bar",
        "number": 100,
    }).Infoln("I am kafkahook")
}
```
