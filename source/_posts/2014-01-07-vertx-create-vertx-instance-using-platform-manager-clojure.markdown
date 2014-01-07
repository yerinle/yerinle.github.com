---
layout: post
title: "Vertx: Create vertx instance using Platform Manager (clojure)"
date: 2014-01-07 18:38
comments: true
categories: [vertx, clojure]
---

*Setup project as described in [previous post](http://yerinle.github.io/blog/2013/12/24/vertx-leiningen-plugin-for-vertx-developlment-clojure/)*

*open a terminal window, run lein repl*
```
lein repl
```

*import the platform locator*
``` clojure
(import 'org.vertx.java.platform.PlatformLocator)
```

*create instance of platform manager*
``` clojure
(def pm (.createPlatformManager PlatformLocator/factory))
```

*require vertx.embed and then set vertx instance atom*
``` clojure
(require '[vertx.embed :as embed])
(embed/set-vertx! (.vertx pm))
```

now you can start a server, for example to start a http server do the following<br/>
import the http namespace
``` clojure
  (require '[vertx.http :as http]))
```

*declare a request handler*
``` clojure
  (defn req-handler [req]
  (-> (http/server-response req)
      (http/add-header "Content-Type" "text/html; charset=UTF-8")
      (http/end "<html><body><h4>It's working!</h4></body></html>")))
```

*start server using the handler and assign it to a variable server*
```
(def server (-> (http/server)
    (http/on-request req-handler)
    (http/listen 8080 "localhost")))
```