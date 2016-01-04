---
layout: post
title:  "Jekyll - rouge로 코드 highlighting"
date:   2016-01-02 15:08:33
categories: jekyll
---
[jekyll-templates] 설명을 보고, `pygments`를 설치해야만, 코드를 표현할 수 있다고 생각했다.
하지만, pygments는 계속 실패했고...

```sh
Configuration file: /${repo_dir}/dalzony.github.io/_config.yml
            Source: /${repo_dir}/dalzony.github.io
       Destination: /${repo_dir}/dalzony.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Dependency Error: Yikes! It looks like you don't have pygments or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- pygments' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
  Liquid Exception: pygments in ${repo_dir}/dalzony.github.io/_posts/2016-01-03-highlighting.md
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    pygments
```

여기저기서 알려주는 다음과 같은 짓을 해봤지만 역시나 실패였다.

```sh
$ gem install pygments.rb
$ sudo easy_install Pygments
$ ... 기억안나는 삽질들, Jekyll재설치 등등
```

결국 블로그를 또 몇 달동안 방치하는 사태로 이어졌다.

## 해결 - rouge

왜 그랬는지 모를 pygments에 대한 집착을 버리고 [Run Jekyll On Windows] 를 보다가 rouge를 사용하기로 했다.
한방에 해결!

`_coufig.yml`에 `highlighter: rouge`로 바꾸기만 하면 따로 할 일도 없다.

끗


[Jekyll-templates]: http://jekyllrb.com/docs/templates/#code-snippet-highlighting
[Run Jekyll On Windows]: http://jekyll-windows.juthilo.com/
