## 블로그 문서 작성

- 문서 생성은 다음의 단계를 거칩니다.
프로젝트의 컨벤션 기반으로 작성되어야 합니다.
영어로 작성되어야 합니다.

./ 트리 구조(예시)는 다음과 같습니다.

```
├── linux
├── odroid
├── os
├── pdf
├── peripherals
├── trace32
└── wiringpi
...
```

jekyll collection 이기 때문에 jekyll의 포스팅 규칙에서 자유롭습니다.
기존 컨벤션 기반으로 작성합니다.
특정 주제에 맞는 디렉토리를 만들고 그 아래에 md 파일로 작성합니다.
만약 해당되는 주제가 없다면 디렉토리를 새로 만들고 그 아래에 md 파일을 작성합니다.


../assets/images/documents/ 아래 트리 구조(예시)는 다음과 같습니다.

```
.
├── gic
├── odroid
├── os
├── peripherals
├── trace32
└── wiringpi
...
```

1. 키워드를 기반으로 GoogleSearch 도구를 사용하여 키워드를 설명하는 내용을 search.md 에 작성합니다.
이미지는 사람 친화적으로 보기가 쉬워야 합니다. flowchart나 plantUML 이미지도 좋습니다.

2. gemini-image-gen 도구를 사용하여 설명을 이해하는데 도움을 줄 수 있는 이미지를 생성 해야 합니다.
- 예시: gemini-image-gen "gicv3-its"
이와 같이 생성된 이미지는 ../assets/images/documents/gic/... 아래에 키워드에 맞는 디렉토리에서 , 그 안에 doc-gicv3-its-...png라는 적절한 이름으로 저장합니다.

3. search.md 내용을 바탕으로 documents 초안을 draft.md에 작성합니다.
- 글의 구조는 다음과 같습니다.
개념: 해당 주제의 정의나 설명을 작성
핵심 요약: 가장 중요한 내용 3가지를 요약 및 설명
상세 설명: 각 내용에 대해 구체적인 예시와 함께 상세히 설명
마무리: 마지막으로 중요한 내용을 다시 한번 정리
참고 자료: search.md에서 참고한 자료들을 링크로 제공
GoogleSearch 도구를 사용해야 하며, url도 함께 작성되어야 함

4. draft.md 내용을 바탕으로 문서를 작성합니다.
문서 시작은 다음과 같습니다.

```
---
permalink:
title:
excerpt:
toc: true
---
```

toc는 true 고정이며, 문서에 알맞게 각 속성값을 먼저 채우고 글 작성을 시작합니다.
적절한 title, excerpt 등을 채우고 나서 내용 작성을 시작합니다.
즉, permalink는 항상 /documents/... 값을 가져야 합니다.

6. draft.md 내용을 참고하여 각 문단마다 설명 보충과 이해를 돕기 위한 이미지를 gemini-image-gen 도구를 사용하여 생성합니다. (필요할 경우에만)
해당 이미지들은 /assets/images/documents/{categories}/.. 아래에 jpg 파일로 저장합니다.
{categories}는 /assets/images/documents/ 바로 아래에 있는 디렉토리들 입니다.
```
<img src="/assets/images/documents/{categories}/ai.png" alt="ai" width="320" height="240">
```
위와 같은 방식으로 이미지를 본문에 필요한 부분에 추가해 주세요.

7. 중복에 대한 문제..
작업 중에, path와 이름이 중복이 된다면 images의 경우 overwriting이 될 수 있습니다. 이럴 경우, 반드시 사용자에게 경고를 전달하여야 하며
overwriting은 허용될 수 없습니다.

8. 이미지 생성에 대한 문제..
gemini-image-gen 도구를 반드시 사용해야 하며,
이미지 생성이 실패가 되었을 경우, (0kb) 사용자에게 즉시 보고해야 하며, 모든 동작을 중단해야 합니다.
error 보고를 반드시 해야 합니다.

9. 문서 형식에 대한 규칙
문장 최대 길이는 120자를 넘지 않게, 요청 드립니다. jekyll 구조 상 toc가 있기 때문에 너무 길 필요가 없습니다.
줄바꿈은 ```<br>``` html 커멘드로 문서 편집을 하는 사용자도 구조가 잘 보이게끔 편집해주세요.

10. 용어에 대한 강조
이 프로젝트는 span 을 사용한 용어 강조를 지원하고 있습니다.

사용 예시:
```
Server <span style="{{ site.code }}">Host</span> : ...
```

위와 같이 span을 쓰고, 종료할 때에는 반드시 한 칸을 띄워야 합니다.

11. 키워드가 없을 경우 추가 작업..

이 프로젝트의 root path에는 _pages/documents.md 가 있습니다.
없을 경우에는 List에 추가가 필요하며, Table에도 역시 규칙에 맞게 추가가 필요합니다.

12. 할루시네이션 검사
할루시네이션을 경계해야 합니다. 자신이 찾은 자료가 정말 사실인지, 교차 검증은 필수 이며,
자체 할루시 네이션 검사를 마지막에 한번 더 해야 합니다. 왜냐하면 문서작성은 내용에 오류가 있어서는 안됩니다.
