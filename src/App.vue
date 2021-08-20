<template>
  <div class="container">
    <cards-form
        @create="createCard"
    ></cards-form>
    <cards-list
        :cards="sortedCards"
        @remove="removeCard"
        v-model="selectedSort"
        :options="sortOptions"
    ></cards-list>
  </div>
</template>

<script>
import CardsForm from "@/components/CardsForm";
import CardsList from "@/components/CardsList";

export default {
  components: {
    CardsForm, CardsList,
  },
  data() {
    return {
      cards: [
        {
          id: 1,
          title: "Первый товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 10000
        },
        {
          id: 2,
          title: "Второй товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 20000
        },
        {
          id: 3,
          title: "Третий товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 30000
        },
        {
          id: 4,
          title: "Четвертый товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 50000
        },
        {
          id: 5,
          title: "Пятый товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 40000
        },
        {
          id: 6,
          title: "Шестой товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 60000
        },
        {
          id: 7,
          title: "Седьмой товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 70000
        },
        {
          id: 8,
          title: "Восьмой товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 80000
        },
        {
          id: 9,
          title: "Девятый товар",
          body: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.",
          price: 90000
        }
      ],
      selectedSort: "",
      sortOptions: [
        {value: "title", name: "По названию"},
        {value: "priceMinMax", name: "По возрастанию цены"},
        {value: "priceMaxMin", name: "По убыванию цены"}
      ],
      /*properties beneath is for correct work of actions with localStorage*/
      savedCards: "",
      returnedCards: "",
      copyOfCards: "",
      anotherCopyOfCards: ""
    }
  },
  methods: {
    createCard(card) {
      this.cards.push(card);
    },
    removeCard(card) {
      this.cards = this.cards.filter(c => c.id !== card.id)
    },

  },
  computed: {
    sortedCards() {
      //ascending sort
      if (this.selectedSort === "priceMinMax") {
        for (let i = 0; i < this.cards.length; i++) {
          for (let j = i; j < this.cards.length; j++) {
            if (Number(this.cards[i].price) > Number(this.cards[j].price)) {
              let temp = this.cards[i];
              this.cards[i] = this.cards[j];
              this.cards[j] = temp;
            }
          }
        }
        return [...this.cards];
        //descending sort
      } else if (this.selectedSort === "priceMaxMin") {
        for (let i = 0; i < this.cards.length; i++) {
          for (let j = i; j < this.cards.length; j++) {
            if (Number(this.cards[i].price) < Number(this.cards[j].price)) {
              let temp = this.cards[i];
              this.cards[i] = this.cards[j];
              this.cards[j] = temp;
            }
          }
        }
        return [...this.cards];
        //title sort
      } else {
        return [...this.cards].sort((card1, card2) => {
          return card1[this.selectedSort]?.localeCompare(card2[this.selectedSort])
        })
      }
    }
  },
  mounted() {
    //here is a lot of number two in comparisons because after deleting all elements in array there are still two symbols [ ]

    //first open of the app
    if (!localStorage.myKey) {
      this.copyOfCards = this.cards.slice();
      this.savedCards = JSON.stringify(this.copyOfCards);
      localStorage.setItem("myKey", this.savedCards);
    }
    if (localStorage.myKey.length !== 2) {
      this.anotherCopyOfCards = this.cards.slice();
      this.returnedCards = JSON.parse(localStorage.getItem("myKey"));
      this.cards = this.returnedCards;
    }
  },
  updated() {
    this.savedCards = JSON.stringify(this.cards);
    localStorage.setItem("myKey", this.savedCards);
    if (localStorage.myKey.length === 2) { // when there is no elements on the page left this condition works out
      this.cards = this.anotherCopyOfCards;
    }
  }
}

</script>

<style>

@font-face {
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 400;
  font-display: auto;
  src: local("Source Sans Pro"),
  url('./fonts/sourcesanspro/SourceSansPro-Regular.ttf') format("truetype");
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Source Sans Pro", sans-serif;
  background-color: #FAF9F7;
}

.container {
  display: grid;
  grid-template-areas: "form . . sort-button"
                       "form content content content"
                       "form content content content"
                       "form content content content";
}

</style>