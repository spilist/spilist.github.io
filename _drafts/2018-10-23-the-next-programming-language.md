---
title: "[번역]당신이 꼭 배워야 하는 프로그래밍 언어"
tags: ["Software Development", "Programming Language"]
---

원문: [The Next Programming Language You Should Learn](http://leohetsch.com/the-next-programming-language-you-should-learn/) by [Leonard Hetsch](https://twitter.com/leo_hetsch)

---

프로그래머 여러분, 안녕하세요.

당신이 이 글을 읽으려고 클릭한 몇 가지 이유를 추측해보죠.

어쩌면 당신의 다음 커리어를 성공으로 이끌어줄, 6개월만 배워도 모두가 당신을 고용하고 싶어할 만한 그런 멋진 언어를 찾길 희망하며 이 글을 클릭했을지도 모르겠네요. 아니면 "최고의" 프로그래밍 언어를 논하는 또다른 낚시글에 그저 화가 나서, 글 맨 끝으로 스크롤하여 저를 비난할 준비를 마쳤을수도 있겠군요. 또는 그냥 당신의 뉴스피드에 나타난 이 글이 뭔지 궁금해서, 새로운 언어 하나 배워볼까 해서 클릭했으려나요.

음, 실망시켜드려 죄송합니다. 저는 모든 벤치마크에서 최고점을 받아 AWS에서 월 10달러로 사용자 10억을 감당하는 플랫폼을 만들 수 있는 그런 갓 나온 최고 성능의 어메이징한 프로그래밍 언어를 소개하려는 게, 아닙니다.

이미 인터넷에는 이 주제에 대한 [십수개의 Quora 쓰레드](https://www.quora.com/search?q=which+programming+language+should+I+learn)와 [Medium 포스트](https://medium.com/search?q=choose%20programming%20language)가 있고, [구글](https://www.google.co.uk/search?q=which+programming+language+should+i+learn&oq=which+programm&aqs=chrome.1.69i57j0l3j69i60j0.2230j0j7&sourceid=chrome&ie=UTF-8)에는 말할 것도 없죠. 대신 저는, 더 나은 프로그래머가 되기 위해 배워야만 할 궁극의 언어(들)을 찾는 이 영원한 여정에 대한 제 의견을 말씀드리고자 합니다. 사실은 이 여정이 위험한 이유에 대해서도요.

새 집에서 쓸 침대를 하나 사서 설치한다고 가정해 봅시다. IKEA에서 수많은 침대를 본 당신은 혼란에 빠졌습니다. 이전에 한 번도 가구를 직접 설치해본 적이 없었기 때문이죠(아니면 저처럼 가구 설치에 젬병이거나요). 나무로 된 멋진 일제 킹사이즈 침대를 마침내 고르긴 했지만, 어떤 도구를 사용해서 설치할지는 전혀 감이 오지 않는군요.

그래서 당신은 가까운 판매원에게 가서, 침대 설치에 쓸 단 하나의 궁극 도구가 뭐냐고 물어봅니다.

잠깐, 뭐라고요? 당연히 이런 걸 물어보지 않겠죠. 확실히는 모르겠지만, 나사와 스크류드라이버, 렌치, 어쩌면 드릴 정도가 필요할 거라고 생각합니다. 하지만 확실히 알 수 있는 건, 단 하나의 도구만으로는 원하는 대로 설치를 할 수 없으리라는 사실이죠. 그리고 만약 판매원이 200달러짜리 마법의 올인원 도구를 팔려고 들지 않는 한, 그도 당신에게 같은 말을 해줄 겁니다.

소프트웨어에서도 마찬가지입니다. 모든 것보다 우월한 단 하나의 도구, 단 하나의 언어, 단 하나의 플랫폼 따위는 존재하지 않습니다. 어떤 제대로 된 언어로도 당신이 원하는 걸 만들 수 있고, 그거면 충분합니다. 그러고 나서 당신이 원하는 것이 속도냐, 확장성이냐, 성능이냐 등에 따라 더 나은 옵션을 선택할 수 있겠죠. 초기 단계 스타트업에게는 아주 좋은 기술 선택이, 수백만 사용자로 스케일해야 하는 회사에게는 끔찍한 선택이 될 수 있습니다.

네, 맞습니다. PHP로 Wordpress 웹사이트만 만들어서도 아무 걱정 없이 먹고살 수 있습니다. Java 하나만 평생 쓰더라도 일자리 걱정은 없을 겁니다. Ruby, Python, Javascript, 또는 당신이 원하는 다른 무언가를 사용할 수도 있습니다. 이 언어들로 무언가를 만들어서 당신이 원하는 바를 성취할 수 있다면 그 모두가 좋은 선택입니다.

사실 당신이 집중하기로 선택한 기술 하나 때문에 다음 일자리를 찾지 못하게 될 가능성은 매우 낮습니다. 유일한 예외는 당신이 고른 언어가 매우 좁은 사용처에서만 쓰이거나, 시대에 뒤떨어진 경우입니다(물론 이 경우에도, 여전히 [Fortran 프로그래머를 찾는 곳](https://www.indeed.com/q-Fortran-jobs.html)이 있는 것 같군요).

그러나 저는 이런 고민이 아주 일반적이며 우리 모두가 때로 이 고민에 빠져들게 된다는 걸 인정합니다. 심지어 저조차도, 최근까지도 이런 고민을 합니다. 요즘 인기를 끄는 이 새로운 언어에 시간을 쏟아야 할까? 아니면 내가 좀 더 "진지한" 프로그래머로 보일 만한 이 언어를 선택해야 할까? 이런 고민은 평범한 것입니다. 고민은 인간의 것이니까요. 그리고, 우리의 일이 사실상 컴퓨터에게 속삭이는 것에 비슷한 만큼, 우리 모두는 아직 인간입니다. (*And, as close as our job is to whisper to the ears of computers, we are all still humans.* - 번역이 어려워서 원문을 포함)

인력시장에서 개발자 구인난은 실존합니다. 아마 앞으로 몇년간은 그대로겠죠. 소프트웨어 엔지니어를 찾고 고용하는 일은 무척 어렵습니다. 하지만 진짜 어려운 일은 아주 훌륭한 소프트웨어 엔지니어를 찾는 것이죠. 몇몇 플랫폼이 좀 더 거대한 커뮤니티를 갖고있긴 하나, 이 말은 프로그래밍 언어에 상관없이 사실입니다.

저는 10여년 전 HTML, CSS, Javascript와 PHP로 제 첫번째 웹사이트를 만들었습니다. 

I started playing with HTML, CSS, Javascript and PHP building my first websites about ten years ago. Hell, I even had no idea at that time it was something I could find a job and build a career with. I later discovered Ruby and fell in love with it (and I still do), and I also learned to use Node.js. I learned to build iOS apps with Objective-C (did not fell in love this time, but still built a few apps with it). I discovered Go and fell in love again. More recently, I’ve been playing with Elixir and Clojure. As of today, I’m following an online Erlang course, and I enjoy it because it opens up my mind to a whole new way of programming that I was used to. This is refreshing.