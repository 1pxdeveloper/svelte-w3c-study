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

