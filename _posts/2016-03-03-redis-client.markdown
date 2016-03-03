---
layout: post
title: "[clojure] - redis-client 테스트"
date: "2016-03-03 16:00"
---

`redis client clojure`로 검색하면 다음과 같이 [carmine-github] 최상단에 나온다.

![2016-03-03 4 02 17](https://cloud.githubusercontent.com/assets/562341/13486985/6acac470-e159-11e5-9300-e44d59954782.png)

[레디스 페이지]에서도  carmine을 공식으로 적어둔 듯하다. 그리고 다음과 같이 설명을 적어놨는데.
wcar는 뭐고.. 옵션은 어떤식으로 적어야하지;


```
(def server1-conn {:pool {<opts>} :spec {<opts>}}) ; See `wcar` docstring for opts
(defmacro wcar* [& body] `(car/wcar server1-conn ~@body))
```

마음이 복잡해서 새로운 클라이언트를 찾아봤다.
[clj-redis]를 사용해보니, 별다른 설정없이도 바로 테스트 가능하다.
본격적으로 써야하면 carmine을 살펴봐야겠다.

## [clj-redis] 사용해보기

한켠에 redis를 켜고(?)

![2016-03-03 4 05 26](https://cloud.githubusercontent.com/assets/562341/13487033/d31e781e-e159-11e5-80b7-a52c667619ca.png)

다음과같이 테스트 해보면 끗

```
(require '[clj-redis.client :as redis])

(def db (redis/init))

(redis/ping db)
=> "PONG"

(redis/set db "foo" "BAR")
=> "OK"

(redis/get db "foo")
=> "BAR"
```

[carmine-github]: https://github.com/ptaoussanis/carmine
[레디스 페이지]: http://redis.io/clients#clojure
[clj-redis]: https://github.com/mmcgrana/clj-redis
