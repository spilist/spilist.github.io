---
title: 더 나은 데이터 테이블 디자인을 위해
tags: ["UX", "Product Design", "Data Science", "UI", "Design"]
---

[원문 링크](https://uxdesign.cc/design-better-data-tables-4ecc99d23356)

성공적인 데이터 테이블 UI의 요소들에 대해, 어떤 기능들이 어떨 때 필요한지 보여주는 글을 요약 정리했다.

---

### 고정시키기

- 위아래로 스크롤할 때 최상단 헤더를 고정시켜서 컨텍스트를 언제나 제공한다.![img](https://cdn-images-1.medium.com/max/1600/1*kXEEaxvKP_9xRT0HuqScTQ.gif)
- 마찬가지로, 데이터가 너무 많아서 좌우로 스크롤해야 할 때, identifier 열을 고정시킨 채 스크롤되게 한다. 추가로, identifier가 아니더라도 유저가 비교하며 볼 수 있도록 원하는 열을 고정시키게도 할 수 있다.![img](https://cdn-images-1.medium.com/max/1600/1*Mp9kJSIlLyn5qjX-vD56iA.gif)

### 보이는 정보를 조절하기

- 열의 폭을 유저가 조절할 수 있게 하면 축약된 정보도 쉽게 볼 수 있다.![img](https://cdn-images-1.medium.com/max/1600/1*3Mjvd1N9OlQC-aMWXEVtBQ.gif)

- 행별로 내림/오름차순 정렬 기능과 identifiable한 행에 대한 필터링 기능이 있으면 유저가 원하는 종류의 데이터를 더 쉽게 볼 수 있다. 아예 각 행별로 유저가 필터를 커스터마이즈해서 추가하게 만들 수도 있다.![img](https://cdn-images-1.medium.com/max/1600/1*ViE5_uxbbU6LEfnV8GrQtA.jpeg)

  ![img](https://cdn-images-1.medium.com/max/1600/1*TKej8krSFjNDHoN43tOTkg.gif)
  ![img](https://cdn-images-1.medium.com/max/1600/1*TJJAdrX7xwlhuyLBmD37pg.jpeg)

- 필터와 비슷하게, 데이터셋이 너무 많아 필터링이 불충분한 경우에는 각 행에서 검색이 가능하게 만들 수 있다.![img](https://cdn-images-1.medium.com/max/1600/1*jnENY_7hvq7iYlXayoQV3w.jpeg)

- 어떤 행을 보여줄지, 어떤 순서로 보여줄지를 유저가 커스터마이즈하게 할 수 있다. 이런 설정은 유저별 preset이나 preference 등으로 저장해두는 게 좋다.![img](https://cdn-images-1.medium.com/max/1600/1*0NZs7HZtRrB_TukLjxInIQ.jpeg)

### 컨텍스트에 맞는 행 스타일

- 유저가 빠르게 데이터를 훑어볼 수 있도록 행의 스타일을 조절하는 게 좋다.![img](https://cdn-images-1.medium.com/max/1600/1*yDwqntdUINCNJJTV7BXKzQ.gif)
- 행의 상하 패딩(=display density)을 조절할 수 있게 하면 많은 데이터셋을 훑어보기 쉬워진다.![img](https://cdn-images-1.medium.com/max/1600/1*68Gj3oI6z0ssNSqX3sSQbw.gif)
- 데이터 갯수가 적다면 stripe 스타일이나 행 사이의 border를 없애서 시각적 노이즈를 줄여라.
- stripe 스타일을 적용하면 좌우로 긴 데이터를 봐야 할 때 유저가 같은 행에 있다는 걸 확인시켜줄 수 있다. 주의할 점은, 데이터 갯수가 적으면 유저가 stripe 처리된 것을 강조 처리된 것으로 착각할 수 있다는 것이다.

### 행 갯수 제한

- 데이터 갯수가 많으면, 한 번에 보여주는 행 갯수를 제한하고 페이지네이션을 제공하는 게 좋다. 이 때, 추가 기능으로 유저가 한 페이지의 행 갯수를 조절하게 할 수도 있다.![img](https://cdn-images-1.medium.com/max/1600/1*yLNoP3bNRc37jHn28Mqucg.jpeg)
- 페이지네이션 대신 무한 스크롤을 적용할 수도 있으며, 둘 중 무엇이 더 유용한지는 서비스의 컨텍스트에 따라 다르다.

### 컨텍스트를 유지시키기

- 행에 hover했을 때 해당 행에서 할 수 있는 액션들을 보여주면 똑같은 UI가 반복됨으로 인한 인지적 부하가 줄어들 수 있다. 반면, 이렇게 하면 hover하기 전까지 어떤 액션들이 가능한지 유저가 알 수 없다는 반대급부가 있다.![img](https://cdn-images-1.medium.com/max/1600/1*dCPE8gp5tbaVouGODN5bRQ.gif)

- 인라인으로 각 행의 데이터를 수정할 수 있다면 유저가 개별 행의 디테일 페이지로 들어갈 필요가 없어 편하다. 이 때 어떤 행이 수정되고 있는지 명확히 강조할 필요가 있다.![img](https://cdn-images-1.medium.com/max/1600/1*Sy9hS1AMycj5Uzo4VvckmQ.gif)

- 행을 클릭했을 때, 그 화면에서 행을 확장하여 자세한 정보를 보여줄 수 있다.![img](https://cdn-images-1.medium.com/max/1600/1*0E1UPRzvK4gaV8sZEwOxLQ.gif)

- 비슷하게, 클릭된 행에 대한 quick view가 뜨게 할 수도 있다. 물론 모달로도 가능하다. 모달은 quick view에 비해 더 해당 디테일 화면에 집중하게 하고, 디테일 정보를 보기보다는 CTA를 하는 데 더 적합하다는 점 정도가 다르다.![img](https://cdn-images-1.medium.com/max/1600/1*NSGIPqQ5nnFhunR8Osiunw.gif)

  ![img](https://cdn-images-1.medium.com/max/1600/1*Tt2x8SRugOlJQNsMdidF_g.gif)

- 비슷하지만 또 다른 방법은, 행이 클릭되면 테이블 모드에서 디테일 모드로 전환되어 데이터를 보게 할 수도 있다. 이런 경우는 오버레이를 쓰지 않고 디테일 모드에서 다른 행의 정보를 쉽게 볼 수 있게 하는 게 좋다.![img](https://cdn-images-1.medium.com/max/1600/1*HAkPMgQhO-0kFgh-ITT5qA.gif)

- 여러 개의 모달을 띄워서 유저가 비교할 수 있게 하는 방법도 있다. 모달이 뜰 때 오버레이를 사용하지 않고, 적당한 크기로 유저가 이동 가능하게 만들면 된다.![img](https://cdn-images-1.medium.com/max/1600/1*Bu6hCcWjrXR0k_F5jEJO8g.gif)

### 테이블 데이터 시각화

- 테이블 위쪽에 한눈에 볼 수 있도록, 요약된 정보를 시각화해서 제공하면 유저가 패턴을 파악하고 인사이트를 얻기 쉬워진다.![img](https://cdn-images-1.medium.com/max/1600/1*xhD2-Xa-jn1ve-jT0PLKTw.jpeg)