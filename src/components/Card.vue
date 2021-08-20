<template>
  <div class="card">
    <div class="card-content">
      <img width="332" height="200" src="../assets/img/img.png" alt="фото товара">
      <h3>{{ card.title }}</h3>
      <p>{{ card.body }}</p>
      <b>{{ card.price }} руб.</b>
    </div>
    <div class="delete-button">
      <button @click="$emit('remove', card)"></button>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    card: {
      type: Object,
      required: true
    }
  }
}

</script>

<style scoped>

.card {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 332px;
  height: 423px;
  border-radius: 6px 6px 0 0;
  color: #3F3F3F;
  margin: 5px 5px 15px 5px;
  background-color: #FFFEFB;
  z-index: 0;
}

.card:hover {
  transition: 200ms;
  box-shadow: 0 1px 5px #3F3F3F;
  cursor: pointer;
}

.card:hover button {
  background-color: #ff6c6c;
  display: block;
}

.card button {
  display: none;
  position: absolute;
  left: 305px;
  bottom: 395px;
  width: 35px;
  height: 35px;
  border-radius: 25%;
  z-index: 1;
  border: none;
  background: no-repeat center url(../assets/img/trash.svg) #FF8484;
  background-size: 16px;
}

.card button:hover {
  background-color: #ff5d5d;
  box-shadow: 0 1px 5px #3F3F3F;
  transform: scale(1.1);
  transition: 100ms;
  cursor: pointer;
}

.card button:active {
  background-color: #983232;
}

.card-content h3 {
  margin-left: 16px;
  margin-top: 16px;
  font-size: 20px;
  font-weight: 600;
  line-height: 25px;
  background-color: #FFFEFB;;
}

.card-content p {
  max-height: 100px;
  min-height: 50px;
  margin: 16px 16px 0 18px;
  font-size: 18px;
  font-weight: 400;
  line-height: 20px;
  overflow: hidden;
  background-color: #FFFEFB;
}

.card-content b {
  margin-left: 16px;
  margin-bottom: 24px;
  margin-top: 22px;
  display: block;
  font-size: 24px;
  font-weight: 600;
  overflow: hidden;
  background-color: #FFFEFB;
}

.card-content img {
  border-radius: 6px 6px 0 0;
  display: block;
  width: 332px;
  height: 200px;
}

</style>