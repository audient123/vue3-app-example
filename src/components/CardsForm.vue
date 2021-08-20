<template>
  <form class="form" @submit.prevent>
    <h2 class="name-of-form">Добавление товара</h2>
    <label class="name"> Наименование товара
      <input
          v-model.trim="card.title"
          type="text"
          placeholder="Введите наименование товара"
          required
      >
    </label>
    <label class="description"> Описание товара
      <textarea
          class="description-textarea"
          v-model.trim="card.body"
          placeholder="Введите описание товара"
          required
      >
        </textarea>
    </label>
    <label class="link"> Ссылка на товар
      <input
          type="url"
          v-model.trim="card.link"
          placeholder="Введите ссылку"
          required
      >
    </label>
    <label class="price"> Цена товара
      <input
          type="number"
          min="1"
          v-model.number="card.price"
          placeholder="Введите цену"
          required
      >
    </label>
    <button @click="createCard" v-bind:disabled="isDisableComputed">Добавить товар</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      card: {
        title: "",
        body: "",
        link: "",
        price: ""
      }
    }
  },
  methods: {
    createCard() {
      this.card.id = Date.now();
      this.$emit("create", this.card);
      this.card = {
        title: "",
        body: "",
        link: "",
        price: ""
      };
    }
  },
  computed: {
    isDisableComputed() {
      return this.card.title.length <= 0
          || this.card.link.length <= 0
          || this.card.price.length <= 0;
    }
  }
}

</script>

<style scoped>

.form {
  grid-area: form;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 500px;
  width: 332px;
  margin: 32px 32px;
  border-radius: 4px;
  background-color: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.form h2 {
  align-self: flex-start;
  width: 100%;
  padding-bottom: 18px;
  padding-left: 15px;
  padding-top: 5px;
  color: #3F3F3F;
  font-size: 28px;
  line-height: 35px;
  background-color: #FAF9F7;
  box-shadow: 0 2px 5px #FAF9F7;
  /*position: relative;*/ /*this is for the case of using absolute position of the header pseudo-element*/
}

/*option - header visually is not part of the form*/

/*.form h2::before {
  position: absolute;
  top: -17px;
  left: -10px;
  content: "Добавление товара";
  width: 350px;
  height: 75px;
  background-color: #FAF9F7;
  z-index: 15;
  padding-left: 10px;
  padding-top: 11px;
}*/

.form textarea, button {
  margin-top: 10px;
}

.form input, textarea {
  display: block;
}

.form label {
  font-family: "Source Sans Pro", sans-serif;
  position: relative;
  font-size: 11px;
  line-height: 13px;
  margin-top: 16px;
  margin-bottom: 2px;
}

/*red dots*/

label::before {
  content: "";
  display: block;
  position: absolute;
  border-radius: 50%;
  width: 5px;
  height: 5px;
  background-color: #ff5d5d;
  top: 1px;
}

.name::before  {
  left: 109px;
}

/*red dot for description block is not visible*/
.description::before  {
  display: none;
  left: 84px;
}

.link::before  {
  left: 81px;
}

.price::before {
  left: 61px;
}

.form input {
  font-family: "Source Sans Pro", sans-serif;
  border-radius: 4px;
  width: 284px;
  height: 36px;
  padding: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border: none;
  margin-top: 5px;
}

.form input[placeholder] {
  font-size: 13px;
}

.form input:hover {
  border: 1px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.form input:active {
  background-color: #FAF9F7;
  border: 2px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.form input:focus {
  background-color: #efefef;
}

/*removing arrows from the input with type number*/
.form input[type="number"] {
  -moz-appearance: textfield;
}

.form input::-webkit-outer-spin-button,
::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
/*removing arrows from the input with type number*/


.form textarea {
  font-family: "Source Sans Pro", sans-serif;
  font-size: 13px;
  resize: none;
  width: 284px;
  height: 108px;
  border: none;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.form textarea:hover {
  border: 1px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.form textarea:active {
  background-color: #FAF9F7;
  border: 2px solid lightgrey;
  box-shadow: 0 1px 5px #3F3F3F;
}

.form textarea:focus {
  background-color: #efefef;
}

.description-textarea[placeholder] {
  font-size: 13px;
  font-weight: 400;
  padding-left: 10px;
  padding-top: 10px;
}

.form button {
  font-family: "Source Sans Pro", sans-serif;
}

.form button:enabled {
  background-color: #7BAE73;
  border-radius: 10px;
  width: 284px;
  height: 36px;
  color: white;
  font-size: 14px;
  line-height: 14px;
  font-weight: 600;
  margin-top: 20px;
}

.form button:enabled:hover {
  background-color: #66c052;
  box-shadow: 0 3px 10px #3F3F3F;
}

.form button:active {
  background-color: #57c23f;
  border: 2px solid lightgrey;
  box-shadow: 4px 0 15px #3F3F3F;
  color: #3F3F3F;
}

.form button:disabled {
  border: none;
  position: relative;
  border-radius: 10px;
  width: 284px;
  height: 36px;
  background-color: #dedede;
  color: #B4B4B4;
  font-size: 14px;
  line-height: 14px;
  font-weight: 600;
  margin-top: 20px;
}

.form button:disabled:hover::before {
  position: absolute;
  z-index: 10;
  top: -2px;
  left: -2px;
  border-radius: 10px;
  padding-top: 12px;
  content: "Заполните все обязательные поля";
  background-color: #ff5d5d;
  width: 284px;
  height: 26px;
  font-size: 14px;
  color: #eaeaea;
  box-shadow: 2px 2px 5px #3F3F3F;
}

</style>

   