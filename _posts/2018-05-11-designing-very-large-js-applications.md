---
title:  "[번역] 아주 거대한 (자바스크립트) 어플리케이션을 디자인하기"
tags: JavaScript Software-Development Software-Design
---

```
Malte Ubl의 Designing very large (JavaScript) applications(https://medium.com/@cramforce/designing-very-large-javascript-applications-6e013a3291a3)의 번역입니다. 
이 글의 모든 권리는 원 저작자에게 있습니다. All rights are reserved to the original author.
```



이 글은 호주 JSConf에서의 내 발표 스크립트를 약간 편집한 것이다. [유투브에서 전체 발표를 볼 수 있다](https://www.youtube.com/watch?v=ZZmUwXEiPm4).

![img](https://cdn-images-1.medium.com/max/1600/1*DqvlkOgHSKmp5Tu1eX5mdw.png)

안녕하십니까. 저는 아주 거대한 자바스크립트 앱을 구축해왔습니다. 이젠 이런 일을 더이상 하지 않기 때문에, 제가 해온 일을 돌아보면서 무엇을 배웠는지 공유할 좋은 타이밍이라고 생각했습니다. 

어제 학회 파티장에서 맥주를 마시며 질문을 하나 받았는데요. "Malte, 왜 당신이 이 주제에 대해 이야기할 만한 자격이 있다고 생각하나요?" 이 질문에 대답하는 것이 실제로 제 발표에 연관이 있다고 생각하기 때문에, 저 자신에 대해 이야기하는 게 익숙하지는 않지만 해보겠습니다. 

저는 구글에서 자바스크립트 프레임워크를 만들었습니다. 그 프레임워크는 Photos, Sites, Plus, Drive, Play, 검색엔진 등 구글이 제공하는 서비스들에 사용되고 있죠. 개중 몇몇 사이트는 꽤 크고, 당신도 아마 몇 개는 써본 경험이 있으실 겁니다.



![img](https://cdn-images-1.medium.com/max/1600/1*v0r4OVf-RXr9ePakdmv5LQ.png)

이 자바스크립트 프레임워크는 오픈소스가 아닙니다. 그 이유는, 이 프레임워크가 React랑 비슷한 때에 나왔고, 제가 "사람들이 선택할 만한 자바스크립트 프레임워크를 또 늘릴 필요가 정말 있을까?"라고 생각했기 때문입니다. 구글은 이미 오픈 소스 자바스크립트 프로젝트를 몇 개 내놓은 상태였고(Angular와 Polymer), 또 하나가 추가되면 사람들이 혼란을 겪으리라 생각했기에, 그냥 우리끼리만 가지고 있자고 결정했습니다. 

하지만 오픈소스가 아니었더라도, 이걸 만든 경험에서 배울 점이 많을 뿐더러 우리가 배운 걸 공유할 가치가 충분히 있다고 생각합니다.



![img](https://cdn-images-1.medium.com/max/1600/1*LL3uYYDMT5uIFRxR_7JxPQ.png)

자, 이제 아주 거대한 앱에 대해, 그리고 그런 앱들이 가지는 공통점에 대해 이야기해봅시다. 우선, 당연히 앱을 개발하는 개발자는 아주 많겠죠. 수십 명일 수도 있고 더 많을 수도 있습니다. 이들은 감정도 있고 다른 사람들과의 사이에 문제도 있을 수 있으며, 이런 점을 당신은 염두에 두어야 합니다.



![img](https://cdn-images-1.medium.com/max/1600/1*WEH24kaBbar8-1gzN_AO3w.png)

팀이 그렇게 크지 않더라도 여러가지 문제가 생길 수 있습니다. 당신이 그 앱을 개발하는 데 꽤 오랜 시간을 투자해왔을 수도 있고, 그 앱을 유지보수하는 첫 번째 사람이 아닐 수도 있고, 모든 컨텍스트를 가지지 않았을 수도 있고, 당신이 완전히 이해하지 못한 무언가가 있을 수도 있고, 팀 내의 누군가는 앱 전반에 대해 이해하지 못하고 있을 수 있습니다. 이런 게 우리가 아주 커다란 앱을 구축할 때 생각해야 할 사항들입니다.



![img](https://cdn-images-1.medium.com/max/1600/1*fzb42X35lNGmkQHhJLhEBQ.png)