---
layout: "post"
title: "리눅스 명령어 : rcp, scp 사용하기"
date: "2016-05-25 20:04"
---

원격 카피 커맨드로 주로 scp를 사용했는데, 어떤 서버에서 scp가 안먹혔다.
알고보니 내가 접속한 서버에는 scp가 있는데 원격에는 scp가 없기 때문이었다.
복사는 해야겠고, scp를 원격에 깔긴 애매하고 그러던중 누군가 scp가 안되니 rcp를 쓰라고 추천을 받았다!

## scp 사용법

```
# 보내기/가져오기
scp <local_file> 계정@서버주소:목적경로
scp 계정@서버주소:서버의파일경로 목적파일명(또는 .)

#r 옵션
scp -r 계정@서버주소:서버경로 목적상위폴더
```

## rcp 사용법

```
rcp [-r] source destination

rcp server:test .
```

## 기타 정리 안된 것

- rsync는 뭐지?
- rcp, scp의 차이
  - rcp = remote copy remote
  - scp = secure copy   

## 참고

참고링크에서 사용법,차이,자동화 등을 살펴볼 수 있을 것 같다.

- [ssh의 모든것]
- [제타위키]

------
[ssh의 모든것]: http://yagi815.tistory.com/598
[제타위키]: http://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_scp_%EC%82%AC%EC%9A%A9%EB%B2%95
