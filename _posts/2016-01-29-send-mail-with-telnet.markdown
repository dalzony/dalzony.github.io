---
layout: post
title: "[osx] telnet 으로 메일 보내기"
date: "2016-01-29 11:02"
categories: mail
---

## 로컬 to gmail

### 1.stmp 데몬 띄우기

```sh
$ sudo postfix start
=> postfix/postfix-script: starting the Postfix mail system

```

### 2.telnet

```sh
$ telnet localhost 25
=>

Trying ::1...
Connected to localhost.
Escape character is '^]'.
```

### 3.내용쓰기

```sh
helo localhost #내가 누군지 알려줌, 크게 중요하지 않은 듯
mail from: sender-id@localhost
rcpt to: receiver-id@gmail.com
data
from: sender-name<sender-id@localhost>
To: receiver-name<receiver-id@gmail.com>
Subject: Hello~

HELLO!
mail test
.
quit


```

## gmail smtp 에 붙어서 보내기

### 1. mx record 주소 알아내기

```sh
nslookup
> set q=mx
> gmail.com
```

### 2. 조회 후 가장 위의 주소를 택하기

* telnet gmail-smtp-in.l.google.com. 25


## 한글로 보내기

다음 내용을 추가하고, 내용을 `base64`로 인코딩해 붙인다.

```
Content-Type: text/plain
Content-Transfer-Encoding: base64
```

예]

```
helo localhost
mail from: sender-id@localhost
rcpt to: receiver-id@gmail.com
data
from: sender<sender-id@localhost>
To: receiver<receiver-id@gmail.com>
Subject: Hello~
Content-Type: text/plain
Content-Transfer-Encoding: base64

7JWI64WVPz8/Pw0K67Cp6rCR7Iq164uI64ukDQrtlZjsmYDsnKANCkkgYW0gZmluZSB0aHgNCuqzvOygnO2WiOuNlOyXvA0K
.
quit
```

## 기타 (tcp dump)

로컬에서 보낼때와 gmail 에 붙어서 보낼 때 같은 형식으로 보냈지만 gmail smtp서버에 붙으면 에러가 났다.
로컬서버에 붙어서 gmail보낼때의 tcp dump를 보고, 그대로 가져와서 보내보니 성공했다.

```
$ tcpdump -s 0 -n -e -x -A -vvv -r test.pcap | more
```

```
  EHLO local-name.local
  MAIL FROM:<sender-id@localhost.local> SIZE=519
  RCPT TO:<receiver-id@gmail.com>
  DATA
  Received: from localhost (localhost [IPv6:::1])
          by local-name.local (Postfix) with SMTP id 32E3669FC89
          for <receiver-id@gmail.com>; Thu, 28 Jan 2016 18:44:09 +0900 (KST)
  from: sender <sender-id@localhost.local>
  To: receiver<receiver-id@gmail.com>
  Subject: Hello~
  Content-Type: text/plain
  Content-Transfer-Encoding: base64
  Message-Id: <20160128094418.32E3669FC89@local-name.local>
  Date: Thu, 28 Jan 2016 18:44:09 +0900 (KST)

  7JWI64WVPz8/Pw0K67Cp6rCR7Iq164uI64ukDQrtlZjsmYDsnKANCkkgYW0gZmluZSB0aHgNCuqzvOygnO2WiOuNlOyXvA0K
  .
```
