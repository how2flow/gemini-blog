## 블로그 포스팅 컨텐츠 작성

- 블로그 생성은 다음의 단계를 거칩니다.
프로젝트의 컨벤션 기반으로 작성되어야 합니다.
한국어로 작성되어야 합니다. (전문 용어는 제외)

jekyll 포스팅은 다음과 같습니다.
포스팅 문서는 yyyy-mm-dd-{name}.md 형식으로 만들어집니다.
post 디렉토리 아래에는 md 파일만 있어야 합니다.
jekyll 구조 상, image나 다른 종류의 파일들은 상위 폴더, 즉 프로젝트 root path의
assets 아래에서 관리되어야 합니다.

./ 트리 구조(예시)는 다음과 같습니다.
```
.
├── 2023
│   ├── 04
│   ├── 05
│   ├── 06
│   ├── 07
│   ├── 08
│   ├── 09
│   ├── 11
│   └── 12
├── 2024
│   ├── 01
│   ├── 02
│   ├── 03
│   ├── 07
│   ├── 08
│   └── 12
├── 2025
│   ├── 03
│   └── 11
├── GEMINI.md
....
```
month 디렉토리까지만 만들고, 그 아래 md 파일을 생성해야 합니다.

../assets/images/posts/ 아래 트리 구조(예시)는 다음과 같습니다.

```
└── posts
    ├── contents
    │   └── vibe-coding
    └── thumbnails
        └── vibe-coding
...
```

1. 키워드를 기반으로 GoogleSearch 도구를 사용하여 키워드를 설명하는 블로그 포스팅에 적합한 썸네일 이미지를 생성합니다. 관련 자료는 3개 이상으로 정리하고,
참고한 웹페이지의 위치는 search 디렉토리에 마크다운 문서를 만들때와 동일하게 현재 시각 기준으로 month까지 하위 디렉토리를 만들고, search.md 문서에 정리합니다.

2. gemini-image-gen 도구를 사용하여 키워드를 설명하는 블로그 포스팅에 적합한 썸네일 이미지를 생성합니다.
- 예시: gemini-image-gen "sunset"
이와 같이 생성된 이미지는 ../assets/images/posts/thumbnails 아래에 "sunset" 디렉토리를 만들고, 그 안에 teaser-sunset.jpg라는 이름으로 저장합니다.

3. search.md 내용을 바탕으로 블로그 포스트 초안을 작성한 뒤, 동일한 규칙으로 하위 디렉토리들을 만들고, draft.md에 작성합니다.
- 글의 구조는 다음과 같습니다.
도입: 독자들의 흥미를 끄는 질문으로 시작
핵심 요약: 가장 중요한 내용 3가지를 요약 및 설명
상세 설명: 각 내용에 대해 구체적인 예시와 함께 상세히 설명
마무리: 이 내용의 의미와 앞으로 미칠 영향에 대한 전망으로 마무리
참고 자료: search.md에서 참고한 자료들을 링크로 제공
GoogleSearch 도구를 사용해야 하며, url도 함께 작성되어야 함

4. draft.md 내용을 바탕으로 최종 블로그 포스트를 작성합니다. jekyll 기반 프로젝트 이므로, 실제 포스팅이 되어야 합니다.
예시로 제시한 것처럼, 생성 날짜 기준으로 연도 디렉토리와 월 디렉토리를 만들고, yyyy-mm-dd-name.md 형식으로 문서를 만듭니다.
예를들어, 2023-04-27-rtos.md 문서를 만든다고 하면, 디렉토리는 2023/04/2023-04-rtos.md 를 작성하면 됩니다.
jekyll 문서 시작은 다음과 같습니다.

```
---
permalink:
title:
excerpt:
header:
  teaser:
categories:
  - 
tags:
  - 
toc: true
---
```

toc는 true 고정이며, 문서에 알맞게 각 속성값을 먼저 채우고 글 작성을 시작합니다. 예를들어, teaser에 sunset thumbnail.jpg를 써야 한다면,
teaser: /assets/images/posts/thumbnails/sunset/teaser-sunset.jpg
이런식으로 채우면 됩니다. permalink는 permalink: /post/sunset 이런식으로 경로를 지정해 주면 됩니다. 경로 지정 시, 연도와 월 디렉토리 정보는 포함하지 않습니다.
적절한 title, excerpt 등을 채우고 나서 내용 작성을 시작합니다.
즉, permalink는 항상 /posts/{name} 값을 가져야 합니다.

6. draft.md 내용을 참고하여 각 문단마다 설명 보충과 이해를 돕기 위한 이미지를 gemini-image-gen 도구를 사용하여 생성합니다. (필요할 경우에만)
해당 이미지들은 /assets/images/post/contents/{name}/.. 아래에 jpg 파일로 저장합니다.
```
<img src="/assets/images/posts/contents/{name}/ai.jpg" alt="ai" width="320" height="240">
```
위와 같은 방식으로 이미지를 본문에 필요한 부분에 추가해 주세요.

7. 중복에 대한 문제..
만약 블로그 포스팅을 할 때, 이름이 중복이 된다면 images의 경우 overwriting이 될 수 있습니다. 이럴 경우, 반드시 사용자에게 경고를 전달하여야 하며
overwriting은 허용될 수 없습니다.

8. 이미지 생성에 대한 문제..
gemini-image-gen 도구를 반드시 사용해야 하며,
이미지 생성이 실패가 되었을 경우, (0kb) 사용자에게 즉시 보고해야 하며, 모든 동작을 중단해야 합니다.
error 보고를 반드시 해야 합니다.

9. 문서 형식에 대한 규칙
문장 최대 길이는 120자를 넘지 않게, 요청 드립니다. jekyll 구조 상 toc가 있기 때문에 너무 길 필요가 없습니다.
줄바꿈은 ```<br>``` html 커멘드로 문서 편집을 하는 사용자도 구조가 잘 보이게끔 편집해주세요.

10. search.md 규칙
google_search 결과에서 vertexaisearch 링크가 아닌, 텍스트 본문에 원본 도메인을 사용.
또한, 본문에 참고자료 기재 시, search.md를 첨부하는 것이 아니라 실제 도메인을 사용할 것.
