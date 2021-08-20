<template>
  <select v-model="modelValue" @change="changeOption" class="sort-button">
    <option disabled value="">Сортировка</option>
    <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
    >
      {{ option.name }}
    </option>
  </select>
  <div class="cards">
    <transition-group name="card-list">
    <card
        v-for="card in cards"
        :card="card"
        :key="card.id"
        @remove="$emit('remove', card)"
    ></card>
    </transition-group>
  </div>
</template>

<script>
import Card from "@/components/Card";

export default {
  components: {Card},
  props: {
    cards: {
      type: Array,
      required: true,
    },
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>

<style scoped>

.cards {
  grid-area: content;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  margin-top: 20px;
  margin-right: 15px;
}

.sort-button {
  font-family: "Source Sans Pro", sans-serif;
  grid-area: sort-button;
  margin-top: 32px;
  margin-right: 16px;
  width: 121px;
  height: 36px;
  border: none;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding-left: 10px;
  padding-right: 5px;
  border-radius: 4px;
  font-size: 13px;
  line-height: 15px;
  color: #B4B4B4;
}

.sort-button:hover {
  border: 1px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.sort-button:active {
  background-color: #FAF9F7;
  border: 2px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.sort-button option {
  border: none;
  background-color: #3F3F3F;
}

/*animation*/

.card-list-item {
  display: inline-block;
  margin-right: 10px;
}

.card-list-enter-active,
.card-list-leave-active {
  transition: all 1s ease;
}

.card-list-enter-from,
.card-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.card-list-move {
  transition: transform 0.8s ease;
}

</style>

   