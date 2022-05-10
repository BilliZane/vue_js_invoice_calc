<template>
  <div class="container">
    <h1 class="app-title">Vue Invoice Calc</h1>
  </div>
  <InvoiceForm :newId="products.length + 1" @add-product="add" />
  <InvoiceTable
    :products="products"
    @change-status="changeStatus"
    @delete-products="deleteProducts"
  />
</template>

<script>
import InvoiceForm from '@/components/InvoiceForm'
import InvoiceTable from '@/components/InvoiceTable'
export default {
  components: {InvoiceForm, InvoiceTable},
  name: 'App',
  mounted() {
    document.title = 'Vue Invoice Calc'

    if (!localStorage.getItem('products')) {
      JSON.stringify(localStorage.setItem('products', []))
    } else {
      this.products = JSON.parse(localStorage.getItem('products'))
    }
  },
  data() {
    return {
      products: [],
    }
  },
  methods: {
    add(product) {
      this.products.push(product)
      localStorage.setItem('products', JSON.stringify(this.products))
    },
    changeStatus(idx) {
      this.products[idx].isChecked = !this.products[idx].isChecked
    },
    deleteProducts() {
      this.products = this.filteredProducts
      localStorage.setItem(
        'products',
        JSON.stringify(this.filteredProducts)
      )
    },
  },
  computed: {
    filteredProducts() {
      return this.products.filter((prod) => !prod.isChecked)
    },
  },
}
</script>

<style lang="scss" scoped>
.app-title {
  text-align: left;
  padding: 20px 0;
  font-family: 'Comfortaa', sans-serif;
  font-size: 26px;
  line-height: 30px;
  @media (max-width: 450px) {
    text-align: center;
  }
}
</style>
