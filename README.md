# 3주차 - 컴포넌트를 이용하여 페이지를 만들어보자.
 
## 학습목표

- Atomic Design System을 이해한다.
- OCP 원칙을 이해한다.
- Svelte의 props를 이해한다 (+class props)
- Svelte의 slot을 이해한다
- Svelte에서 #if block 사용법을 익힌다.
- 컴포넌트 시스템을 이해하고 조립식으로 페이지를 작성한다.
- Routify를 이용하여 svelte에서 라우트 기반의 SPA를 작성한다.


## Atomic Design System

- atoms, molecule, organisms, templates, pages
- (디자인의 구성요소를 원자 → 분자 → 유기체 → 템플릿 → 페이지 등으로 구성하여 조립해서 디자인하자는 철학)
- 원래는 UX디자이너를 위한 철학이었으나 이게 유명해지며 개발쪽에서도 차용하고자하는 움직임이 생겼다.
- 개발자와 디자이너간의 생각의 틀을 비슷하게 만들어서 생각의 갭을 좁히는데 아주 유용함
- Atomic design is not a linear process, but rather a mental model to help us 
- think of our user interfaces as both a cohesive whole and a collection of parts at the same time.
- => (개발자랑 디자이너가 각자 저렇게 폴더를 만들어두기만 하는걸로도 생각이 달라진다.)
- https://bradfrost.com/blog/post/atomic-web-design/
- https://simsimjae.tistory.com/392
- https://github.com/danilowoz/react-atomic-design
- https://youtu.be/Yi-A20x2dcA



## OCP (Open Close Principle)

- SOLID 설계 원칙 중 하나 - "좋은 컴포넌트는 확장에 열려 있고 수정에 닫혀 있어야 한다."
- 언제나 요구사항과 디자인은 활용은 변하고 삭제되고 추가되고 예외에 생겨난다.

- 수정편 - 전반에 걸친 수정사항이 생겼을때
1) 변한 부분만 수정하면 되는가? - COOL
2) 기존에 만들었던 걸 전부 수정해야 하는가? → BAD
3) 설계가 변경되어 다 다시 수정해야 하는가? → WORST
ex) Input Field에 기본적으로 X 버튼 기능을 추가하고 싶어요!
1) 변한 부분만 수정하면 되는가? - 이미 컴포넌트로 만들어져 있어서 Input.svelte 컴포넌트 파일에만 기능을 추가하면 됨.
2) 기존에 만들었던 걸 전부 수정해야 하는가? - 기존 input을 찾아 바꾸기로 변환하면 적용 가능
3) 설계가 변경되어 다 다시 수정해야 하는가? →  전에 만들었던 모든 HTML을 찾아서 수작업으로 특정 element를 추가하는 등의 작업을 해야함.

- 확장편 - 기존과 많은 것을 공유하나 일부만 다르게 만들어야 될때 - ex) Input Field에 기본적으로 X 버튼 기능을 선택적으로 추가 하고 싶어요
- 확장의 경우 기존 컴포넌트의 베리에이션인지, 타 atom과의 조합일지 고민이 필요함. (이게 이 컴포넌트에 포함되는게 맞아?)
- bad example) button에 text를 변경할수 있게 하기 위해 <Button text="저장"/> 처럼 만들어 둠.
- 요구사항 - 아이콘이 있는 버튼이 필요해요 → 대응 불가, 컴포넌트 스펙 변경
- <Button icon="icon-save" text="저장"/>
- 요구사항2 - 아이콘이 상단에 있는 디자인도 생김
- <Button icon="icon-save" icon-position="top" text="저장"/> → Bad 설계 (사용시 주의 사항이 늘어남. 아이콘이 버튼의 주요 기능이 아님에도 기본 스펙이 되어버림)
- Maybe good? → <Button><icon-save/>저장</Button> → Button을 컨네이터 형태의 컴포넌트로 설계했더라면 아이콘만 추가해줬을수도 있다.

- *근데 언제나 그렇듯 정답은 없고 균형점 어딘가를 타협하고 만족해야 함.*
- *"Write less Do more" is Always Best!*


## 개발시 컴포넌트 규칙 (CSS 편)

- atom는 자기 자신의 margin과 position을 가져서는 안된다.
- molecule, organisms 만이 atom등의 하위 계층에 레이아웃을 지정할 수 있고 역시 자기자신의 레이아웃은 가급적 금지한다.
- (토스트 팝업이나, FAB, Sidebar drawer 처럼 레이아웃 자체가 Identity인 경우에만 예외)


## 실전 코딩편 - 하지만 실전에서는 어떨까? 이론과 현실은 다른 법 
 - (이론을 공부해도 현실로 오면 달라짐 저만의 작성 요령을 공유 합니다.)

- 일단 그냥 하드 코딩을 한다.
- 작성하다보면 필연적으로 복붙을 하는 경우가 생긴다. (그게 1줄 짜리 input일지라도...)
- 이때 wrap하고,
- atoms, molecule, organisms 중 어느 폴더에 갈지 고민 하고 이름을 짓는다.
- 변하는 내용을 class, prop, slot중에서 택하고 replace
- 앞으로는 이제 만든 컴포넌트만 쓴다.
- 반복


## 이런것도 컴포넌트가 되요

- 1줄짜리 인라인 컴포넌트 <input class="input" type="text"> → <Input/>
- wrapping 컴포넌트 <Password> → <Input type="password"/>
- 레이아웃 Wapper <PopupLayout> ... </PopupLayout>
- 테마 Wapper <DarkTheme> ... </DarkTheme>
- 간격
- if block <MobileOnly>...</MobileOnly> → {#if isMobile#} <slot/> 

- Form Element, input, button → <Button> <Input> : 디자인 적용 및 wrapping을 위해
- A, Img, Svg 등 기본 → 링크 기능도 확장이 가능하고(새고로침 없는 페이지 이동, 스크롤 위치 유지 등), Img는 데이터가 없을때 처리나, lazyLoading 혹인 점진적 로딩, 스켈레톤 loading image 등 추가 기능이 가능하다. 


## 공유하고 싶은 이야기

- 마크업, 그리고 컴포넌트를 설계하고 작성하고 페이지로 만드는 과정은 저보다 훨씬 더 전문가의 관점에서 더 많은 경험과 해법이 있을꺼라고 생각합니다.

- 반면 뭔가 더 나은 해결책이 있을 것 같은 찜찜한 작업 방식이나 해당 분야의 고질적인 문제가 여전히 산재할 수도 있을거라 생각합니다.

- (가령, 디자이너와 기획자와 프론트 엔드 개발자 사이의 변화 대응에 대한 프로세스와 커뮤니케이션 문제는 왜 항상 생기는 걸까?)

- (왜 프론트 개발자가 마테리얼 UI를 썼는데 모양이 이상하게 나올까? 왜 부트스트랩을 썼는데 디자인이 안될까? 등)

- Functional CSS나, Atomic Design, Svelte 등이 이 문제들을 다 해결을 못할지라도 결국은 더 나은 시스템이나 프레임워크, 아키텍쳐등이 저 전보다 나은 개발환경을 만들어 줄 꺼라고 생각합니다.

- 해서 저는 저대로 계속 새로운 트렌드를 공유할테니 저희 셀 내부에서도 끊임없는 문제제기와 소통을 통해서 지금껏 없던 창의적인 해법이 나오기를 기대합니다 (웃음)



## Routify

- Snowpack에서 아직 Routify가 지원이 안되네요. 보류합니다.
- https://routify.dev/
- svelte는 SPA 기반에서는 파일 기반의 공식 Route 라이브러리가 없음.
- Sapper - svelte의 SSR버전 + 라우터 포함 (공식)
- Routify는 이 sapper의 방식을 기반으로 하여 SPA에서 사용하는 라우터
- SSR vs SPA?
- Install - https://routify.dev/guide/installation/install-to-existing-project


## svelte-routing
- https://www.npmjs.com/package/svelte-routing



---


# 두번째 과제 - 짝 맞추기 기억력 게임
- 짝 맞추기 기억력 게임을 만들자 - 예시) https://codepen.io/jstarnate/full/QoagLr

## 학습목표
- view를 Array와 Object로 생각하기
- Array - https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/Arrays
- Object - https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Basics

- svelte에서 Array와 Object를 이용해서 rendering 하는 법을 배운다.
- svelte #each를 익힌다.
- https://svelte.dev/tutorial/each-blocks
- https://svelte.dev/docs#each
- svelte에서 Array의 변경을 업데이트 하기 위한 방법을 이해하자
- 타이머 2탄, setTimeout - setInterval의 1회성 버전
- [고급] javascript Array Method 익히기
- split, map, sort 등...


## 생각해볼 문제

state → render를 하기 위해서 state의 형태는 어떻게 생겼을까?
(혹은 반대로 HTML를 먼저 그려보고 어느 영역의 data가 state로 올라가야 할까?)
어떠한 사용자 액션이 있는가?
state를 변경하기 위한 조건은 1) 어떤 액션 2) 어떤 조건이 있는가?


## 도전과제

1) 퀄리티를 높여봅시다! (기획이든 디자인이든 뭐든 간에 공개할 수준으로!!)
2) 난이도를 조절하기 위해 카드의 개수와 배치를 바꿀 수 있게 만들어 봅시다 (생성, 디자인)
2-1) 난이도를 선택해서 플레이 할 수 있도록 해 봅시다


## 라이브 코딩 (요약)

1. 요구사항을 state - view - action으로 분리 해서 생각하는 작업
2. 마크업 개발자니 view를 통해서 state를 추려내는게 더 쉬울것
3. 일단 view부터 만들어 보자. (대강 카드 만든다)
4. 컨트롤 c + v 
5. 이걸 하면 반복임. 이런 반복을 담당하는 state의 type을 javascript에서 array라고 부름 [1,2,3] 혹은 ["a","b","c"]
6. svelte에서는 each를 통해 반복을 binding함
7. 배열의 내용에 따라 달라지는 걸 보여줌
8. 뒤집어진 카드는 어떻게?
9. 카드 하나를 Object로 만듬
10. Object는 연관된 데이터를 하나로 가지는 거
11. card.text card.is_closed
12. 바인딩을 수정함
13. view와 state는 끝
14. action은? 카드를 선택 => 뒤집음  card.is_closed = false
15. 카드를 두번째 선택 - 비교해서 같으면 OK 아니면 다시 둘을 돌려놓음
16. (숨겨진 시나리오) 이미 오픈된 카드 선택하면?
17. state => action + state => new state : 비지니스 로직이라고 부름(기획서의 언어를 비지니스 로직으로 푸는게 개발자의 능력)
18. setTimeout()을 이용해 적당한 view표현

