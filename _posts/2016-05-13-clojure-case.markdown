---
layout: post
title: "[clojure] case 구문"
date: "2016-05-13 16:16"
---

case 구문이 올바르게 동작하지 않는다면, 제약조건들을 살펴보지 않았을 수도 있다.

# Clojure - case 구문

`(case e & clauses)`

- case 구문은 clause 내의 test-constant 부분에 나열된 값들이 컴파일 타임에 그 값을 알 수 있어야 한다는 제약이 있다.
  - 따라서 문자열이나 키워드 같은 자기 자신으로 평가되는 값들이 주로 나열된다.
- 일치하는 케이스가 없을 때는 예외 발생


## Example

```clojure
(let [mystr "hello"]
  (case mystr
    "" 0
    "hello" (count mystr)))
;;=> 5

(let [mystr "no match"]
  (case mystr
        "" 0
        "hello" (count mystr)))
;; No matching clause: no match
;;  [Thrown class java.lang.IllegalArgumentException]

(let [mystr "no match"]
  (case mystr
        "" 0
        "hello" (count mystr)
        "default"))
;;=> "default"
```

test-constant 부분 제약 조건이 있기 때문에 다음과 같은 예제에서는 케이스문이 올바르게 동작하지 않는다.

```clojure
(let [mystr 1
      test {:id 1}]
  (case mystr
        (:id test) 1
        "hello" (count mystr)
        "default"))
;;=> "default"  
```
