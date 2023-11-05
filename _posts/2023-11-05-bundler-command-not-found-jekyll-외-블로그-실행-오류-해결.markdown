---
layout: post
title: bundler command not found jekyll 외 블로그 실행 오류 해결
# date: 2017-09-12 13:32:20 +0900
date: 2023-11-05 22:42:20 +0900
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2023-11-05.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [jekyll, bundler]
---
사실 블로그를 처음 개설한 곳은 회사였다. 
업무를 마치고 1-2시간 정도 개인 공부를 할 때가 있는데, 

이제 기록을 하지 않으면 안 되겠다... 라는 생각을 깊이 하기도 했고, 
나의 성장을 위해서였다. :)

집에서 개인 컴퓨터에 clone 을 받고.. 

```zsh
bundle exec jekyll serve
```

를 실행했는데...?
<br><br>

![first error]({{site.baseurl}}/assets/img/11-05-missing-jem.png)

이 오류가 떴다. **bundle install** 후에는 
<br><br>

![second error]({{site.baseurl}}/assets/img/11-05-bundler.png)

이 오류까지 뱉었다. **직감적으로 뭔가 충돌하고 있음을 느꼈다.** ㅎ;; 
<br><br><br>
## rbenv 버전을 다르게 깔아서 그런가... ?
우선 버전을 다르게 깔았던 기억이 떠올랐다. 회사에선 2버전 대로 깔았었고,

집에선 3버전 대로 깔았는데, 이 부분에서 문제가 생겼나- 하고 재설치, 

업데이트 적용까지 했으나 감감무소식.. 
여전히 저 오류를 내뱉었다. 
<br><br>


## 해결법

```zsh
rm -rf Gemfile.lock
bundle update
```

이렇게만 해주면 끝! 
bundle exec jekyll serve 로 로컬에서 서버 띄우는 데 문제 없다. :)

<br><br><br>

**참고링크: [https://github.com/rubygems/bundler/issues/6784](https://github.com/rubygems/bundler/issues/6784)**



