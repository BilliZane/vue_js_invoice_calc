<template>
  <div class="invoice-form" @submit.prevent="addProduct">
    <div class="container">
      <form class="invoice-form__body">
        <div class="invoice-form__wrap">
          <input
            type="text"
            class="invoice-form__item"
            placeholder="Product name"
            v-model="name"
            required
          />
          <input
            type="number"
            class="invoice-form__item"
            placeholder="Price"
            v-model="price"
            required
          />
          <input
            type="number"
            class="invoice-form__item"
            placeholder="Qta"
            v-model="qta"
            required
          />
        </div>
        <button class="invoice-form__button">Add</button>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  props: ['newId'],
  emits: ['add-product'],
  data() {
    return {
      name: '',
      price: null,
      qta: null,
    }
  },
  methods: {
    addProduct() {
      if (!this.qta) {
        this.qta = 1
      }

      let newProduct = {
        id: this.newId,
        name: this.name,
        price: this.price,
        qta: this.qta,
        isChecked: false,
      }

      this.$emit('add-product', newProduct)

      this.name = ''
      this.price = ''
      this.qta = ''
    },
  },
}
</script>
<style lang="scss" scoped>
.invoice-form {
  font-family: 'Comfortaa', sans-serif;
  font-weight: 600;
  &__wrap {
    display: flex;
    align-items: center;
    width: 100%;
    @media (max-width: 450px) {
      justify-content: space-between;
      flex-wrap: wrap;
    }
  }
  &__body {
    display: flex;
    align-items: center;
    @media (max-width: 450px) {
      flex-direction: column;
      flex-wrap: wrap;
    }
  }
  &__item {
    border: solid 1px #5a5a5a;
    width: 100%;
    margin-right: 24px;
    padding: 5px;
    font-family: 'Comfortaa', sans-serif;
    @media (max-width: 450px) {
      margin-right: 0;
    }
    &:nth-child(1) {
      max-width: 300px;
      @media (max-width: 450px) {
        min-width: 100%;
        margin-right: 0;
        margin-bottom: 10px;
      }
    }
    &:nth-child(2) {
      max-width: 70px;
      @media (max-width: 450px) {
        flex: 0 1 49%;
        max-width: none;
      }
    }
    &:nth-child(3) {
      max-width: 70px;
      @media (max-width: 450px) {
        flex: 0 1 49%;
        max-width: none;
      }
    }
  }
  &__button {
    display: inline-block;
    padding: 8px 20px;
    background: #5a5a5a;
    color: #fff;
    text-align: center;
    transition: background 400ms;
    &:hover {
      cursor: pointer;
      background: #888;
    }
    @media (max-width: 450px) {
      min-width: 100%;
      margin-top: 10px;
    }
  }
  &__errors {
    padding-top: 15px;
    color: red;
  }
}
</style>
