---
layout: "post"
title: "[clojure] lein-exec 으로 쉘 스크립트 처럼 써보기"
date: "2016-07-19 14:14"
---

https://github.com/kumarshantanu/lein-exec

dependency
        (use '[leiningen.exec :only (deps)])
        (deps '[[re-rand "0.1.0"]])
이렇게 사용
        (use '[leiningen.exec :only (deps)])
        (deps '[[re-rand "0.1.0"]])

        (require '[re-rand :refer :all])
