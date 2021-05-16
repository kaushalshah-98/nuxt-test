<template>
  <div class="max-w-screen-xl mx-auto p-5 sm:p-10 md:p-16">
    <div
      class="
        grid
        xl:grid-cols-4
        lg:grid-cols-4
        md:grid-cols-3
        sm:grid-cols-2
        xs:grid-cols-1
        gap-10
      "
    >
      <div v-for="item in products" :key="item.id">
        <ProductCard :product="item" />
      </div>
    </div>
  </div>
</template>
<script>
import ProductCard from '../components/card'

export default {
  name: 'ProductList',
  components: {
    ProductCard,
  },
  props: {
    products: {
      type: Array,
      default: () => [],
    },
  },
}
</script>
