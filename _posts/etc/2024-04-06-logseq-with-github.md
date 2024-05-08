--- 
title : "Logseq Github와 연동시키기"

categories : 
  - Blog
tags :
  - etc
  - Blog
 
date : 2024-04-06
last-modified-date : 2024-04-08
---

전체적인 과정은 아래 영상을 참조하여 진행하였다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/c2HrdSOoVD8?si=N52Z6eqNsexzZxc9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

우선 Git을 설치하고 GIthub 계정이 있어야 한다.

개인적으로 사용하려면 Gitlab을 사용해도 되는데, 그냥 Github Repository를 올릴 때 Private로 해도 된다.

아무튼 Git (필요하다면 Github Desktop 버전도 설치해도 된다.) 를 설치하고,

[Logseq-Git-Sync-101](https://github.com/CharlesChiuGit/Logseq-Git-Sync-101) 페이지에 가서 관련 도움 파일들도 다운받자.

(위 영상 찍은 분의 관련 깃허브 레포지토리.)

아무튼 이렇게 준비하면, 영상에서는 Git을 Get하고, 이걸 설정해서 자동으로 업로드되게 하였다.

업로드할 위치인 Github Repository도 Create해 주고 (영상의 2분 22초부터)

Git Commit을 수행하여 Github와 연결한다.

이후 Github readme.md 파일을 만들어 레포지토리의 기본 틀을 만들고

.gitignore 파일도 생성해 준다.

이후 Logseq 폴더와도 연결해 준다...

---

이정도가 내가 이해하고 시행한 부분인데 제대로 하려면 더 확인해봐야 할 것 같다 ㅡㅡ

나도 가끔씩 github의 private repository를 만들어서 logseq의 파일을 업로드 해 주고 있다.

자동으로 업로드되게 할 수 있는데, 나는 이걸 Obsidian과도 연동하고 싶기도 하고, 

자동 업로드를 하려면 네트워크 부담도 좀 해결해야 할 것 같아서... 수동으로 가끔 Push 해 주고 있다.

사실 Logseq와 Obsidian을 둘 다 사용하는데, 이걸 어떻게 활용하면 좋을지도 계속 고민이다.

md파일 용량이 많지 않아서 다행이라는 생각이 든다


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
