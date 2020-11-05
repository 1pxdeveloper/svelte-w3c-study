<script>
// let cards = "🍇 🍈 🍉 🍊 🍋 🍌 🍍 🍇 🍈 🍉 🍊 🍋 🍌 🍍".split(" ").map((value, id) => ({
//   id,
//   value,
//   is_closed: true,
// }))

let cards = [
  {
    "id": 0,
    "value": "🍇",
    "is_closed": true
  },
  {
    "id": 1,
    "value": "🍈",
    "is_closed": true
  },
  {
    "id": 2,
    "value": "🍉",
    "is_closed": true
  },
  {
    "id": 3,
    "value": "🍊",
    "is_closed": true
  },
  {
    "id": 4,
    "value": "🍋",
    "is_closed": true
  },
  {
    "id": 5,
    "value": "🍌",
    "is_closed": true
  },
  {
    "id": 6,
    "value": "🍍",
    "is_closed": true
  },
  {
    "id": 7,
    "value": "🍇",
    "is_closed": true
  },
  {
    "id": 8,
    "value": "🍈",
    "is_closed": true
  },
  {
    "id": 9,
    "value": "🍉",
    "is_closed": true
  },
  {
    "id": 10,
    "value": "🍊",
    "is_closed": true
  },
  {
    "id": 11,
    "value": "🍋",
    "is_closed": true
  },
  {
    "id": 12,
    "value": "🍌",
    "is_closed": true
  },
  {
    "id": 13,
    "value": "🍍",
    "is_closed": true
  }
]

let prev = null
let selected_cards = []

const openCard = (card) => {
  // open되어 있으면 skip
  if (!card.is_closed) return

  // 카드를 뒤집음
  card.is_closed = !card.is_closed // @NOTE: Array내 Object를 변경해도 업데이트가 되지 않는다.
  cards = cards // cards를 업데이트 해야 함.

  // 1번째
  if (prev === null) {
    prev = card
    return
  }

  // 2번째 (= 전에 뒤집은 카드가 있는가) => 비지니스 로직

  // 2개가 다르면,
  if (prev.value !== card.value) {

    // 1초뒤 화면 변경 처리 => 둘다 닫기
    setTimeout(() => {
      prev.is_closed = card.is_closed = true
      prev = null // 없던 일로..
      cards = cards
    }, 1000)
  }

  // 2개가 같으면,
  else {

    // 1초뒤 화면 변경 처리 => 둘다 열고 에니메이션 표기
    setTimeout(() => {
      prev.is_closed = card.is_closed = false
      prev.wow = card.wow = true
      prev = null // 없던 일로..
      cards = cards
    }, 1000)
  }
}

cards = cards.slice().sort(() => Math.random() > 0.5 ? 1 : -1)

cards.forEach((card, index) => {
  setTimeout(() => {
    card.is_closed = false
    cards = cards
  }, index * 100)

  setTimeout(() => {
    card.is_closed = true
    cards = cards
  }, index * 100 + (100 * 7))

})
</script>

<main class="layer pack">
  <div class="container hbox wrap">
    {#each cards as card (card.id)}
      <section class="card text-center pack relative cursor-pointer"
               class:card--is-closed={card.is_closed}
               class:card--wow={card.wow}
               on:click={() => openCard(card)}>

        <div class="card__inner layer">
          <div class="card__front layer pack overflow-hidden">
            <span class="pre">{card.value}</span>
          </div>

          <div class="card__back layer overflow-hidden"></div>
        </div>
      </section>
    {/each}
  </div>
</main>

<style>
html {
  background: #f0f0f3;
}

.container {
  width: 1400px;
}

.card {
  font-size: 60px;
  width: 150px;
  height: 226px;
  margin: 16px;
  transition: .5s all;
}

.card__inner {
  transition: .5s all;
  transform-style: preserve-3d;
  border-radius: 8px;
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.1), -10px -10px 10px rgba(255, 255, 255, 0.1);
}

.card:hover .card__inner {
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1), -5px -5px 10px rgba(255, 255, 255, 0.1);
}

.card__front,
.card__back {
  backface-visibility: hidden;
  border-radius: 8px;
}

.card__front {
  background: #f9f9f9;
}

.card__back {
  border: 6px solid #fff;
  background: #ddd;
  transform: rotateY(180deg);
}

.card--is-closed .card__inner {
  transform: rotateY(180deg);
}

.card--wow {
  animation: bounce .5s ease-in-out;
}

@keyframes bounce {
  0% {
    transform: scaleY(1)
  }

  50% {
    transform: scaleY(1.2)
  }

  100% {
    transform: scaleY(1)
  }
}
</style>