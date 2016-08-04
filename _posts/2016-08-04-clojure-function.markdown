---
layout: "post"
title: "[clojure] 유용한 함수 repeatedly,constantly"
date: "2016-08-04 14:50"
---

## repeatedly : 함수를 반복

```clojure
(repeatedly f)
(repeatedly n f)
```

repeatedly를 사용하면, 함수를 무한 반복하거나, 정해진 수만큼 반복할 수 있다.<br>
랜덤한 수를 n개 만들일이 생겼을 때 다음과 같이 활용했다.

```clojure
(take 6 (repeatedly #(rand-int 100)))
;; => (88 52 73 43 89 48)

(repeatedly 6 #(rand-int 100))
;; => (46 51 42 7 84 89)
```

## constantly : x를 리턴하는 함수를 리턴

```clojure
(constantly x)
```

항상 같은 숫자를 리턴하는 함수를 만들 때, 매번 정의하기는 좀 귀찮은데 그럴 때 쓰기 좋다.<br>
clojure-docs에 예가 있다.

```clojure
user=> (def boring (constantly 10))
#'user/boring

user=> (boring 1 2 3)
10

user=> (boring)
10

user=> (boring "Is anybody home?")
10

;;--------------------------------------------------
;; A really goofy way to find the size of a collection
user=> (reduce + (map (constantly 1) [:a :b :c]))
3

;; 테스트할 때 특히 많이 쓰인다.
(constantly 1) is often useful when it comes to testing. You can think of it like you would a "stub".
```

- 참고 : [constantly-clojuredocs]

[constantly-clojuredocs]: http://clojuredocs.org/clojure.core/constantly
