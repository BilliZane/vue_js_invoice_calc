<template>
  <div class="container">
    <div class="add-product" v-if="!products.length">
      Add at least one product, please.
    </div>
    <div class="table" v-if="products.length">
      <table>
        <tr class="table__header">
          <th></th>
          <th>Product name</th>
          <th>Price</th>
          <th>Qta</th>
        </tr>
        <tr v-for="(product, idx) in products" :key="product.id">
          <td class="table__check-wrap">
            <label class="checkbox__wrap">
              <input type="checkbox" @click="changeStatus(idx)" />
              <span class="checkmark"></span>
            </label>
          </td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.qta }}</td>
        </tr>
      </table>
    </div>
    <div class="table__footer" v-if="products.length">
      <button class="table__delete" @click="deleteProducts">
        Delete
      </button>
      <div class="table__total">
        Total: <span>${{ productsTotal }}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['products'],
  emits: ['delete-products', 'change-status'],
  methods: {
    changeStatus(idx) {
      this.$emit('change-status', idx)
    },
    deleteProducts() {
      this.$emit('delete-products')
    },
  },
  computed: {
    productsTotal() {
      let sum = 0
      for (let i = 0; i < this.products.length; i++) {
        sum += this.products[i].price
      }
      return sum
    },
  },
}
</script>
<style lang="scss" scoped>
.add-product {
  padding: 10px;
  color: red;
  font-family: 'Comfortaa', sans-serif;
  font-weight: 600;
  font-size: 16px;
  margin-top: 15px;
}
.table {
  padding: 15px 0;
  font-family: 'Comfortaa', sans-serif;
  font-size: 16px;
  &__header {
    background: #ccc;
    border-bottom: solid 1px #5a5a5a;
    font-weight: 600;
  }
  &__check-wrap {
    position: relative;
    padding: 0;
    margin: 0;
    text-align: center;
  }
  &__footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-family: 'Comfortaa', sans-serif;
  }

  &__delete {
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
  }
  &__total {
    font-weight: 700;
  }
}
table {
  border-collapse: collapse;
  border-spacing: 0;
  width: 100%;
  border: solid 1px #5a5a5a;
}
th,
td {
  text-align: left;
  padding: 16px;
  border-left: solid 1px #5a5a5a;
}

tr:nth-child(even) {
  background-color: #eee;
}

/* checkbox*/

.checkbox__wrap {
  position: absolute;
  top: 32%;
  left: 32%;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;

  @media (max-width: 450px) {
    top: 32%;
    left: 22%;
  }
}

/* Hide the browser's default checkbox */
.checkbox__wrap input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 18px;
  width: 18px;
  background-color: #eee;
  border: solid 1px #5a5a5a;

  transition: background-color 400ms;
}

/* On mouse-over, add a grey background color */
.checkbox__wrap:hover input ~ .checkmark {
  background-color: transparent;
}

/* When the checkbox is checked, add a blue background */
.checkbox__wrap input:checked ~ .checkmark {
  background-color: none;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: '';
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.checkbox__wrap input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.checkbox__wrap .checkmark:after {
  left: 5px;
  top: 1px;
  width: 3px;
  height: 10px;
  border: solid #5a5a5a;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
