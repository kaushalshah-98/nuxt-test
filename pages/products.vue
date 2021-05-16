<template>
  <div>
    <div class="">
      <ProductHeader
        :categories="categories"
        @onSearch="onSearch"
        @onCategoryChange="onCategoryChange"
      />
    </div>
    <div v-if="loading"><Loader /></div>
    <div v-if="products">
      <ProductList :products="productsToShow" />
      <div class="mt-4">
        <Pagination
          :totalpages="totalpages"
          :page="page"
          @changePage="changePage"
        />
      </div>
    </div>
    <!-- <div class="container">
      <div>
        <h1 class="title">Products</h1>
      </div>
    </div> -->
  </div>
</template>

<script>
import ProductHeader from '../components/productHeader'
import ProductList from '../components/productList'
import Loader from '../components/loader'
import Pagination from '../components/pagination'

export default {
  name: 'Products',
  components: {
    ProductHeader,
    ProductList,
    Loader,
    Pagination,
  },
  data() {
    return {
      loading: false,
      products: [],
      searchQuery: null,
      selectedCategory: null,
      categories: [],
      page: 1,
      totalpages: 1,
    }
  },
  computed: {
    productsToShow() {
      if (this.searchQuery && this.selectedCategory) {
        const result = this.products.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(' ')
            .every((v) => item.name.toLowerCase().includes(v))
        })
        return result.filter((i) => i.category === this.selectedCategory)
      } else if (this.searchQuery) {
        return this.products.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(' ')
            .every((v) => item.name.toLowerCase().includes(v))
        })
      } else if (this.selectedCategory) {
        return this.products.filter((i) => i.category === this.selectedCategory)
      } else {
        return this.products
      }
    },
  },
  created() {
    this.getData()
  },
  methods: {
    async getData(query = '') {
      this.loading = true
      const res = await this.$axios.$get(`/api/products${query}`)
      if (res.data) {
        this.products = res.data
        this.totalpages = Math.ceil(res.total / 10)
        res.data.map((i) =>
          !this.categories.includes(i.category)
            ? this.categories.push(i.category)
            : null
        )
      }
      this.loading = false
    },
    onSearch(searchString) {
      this.searchQuery = searchString
    },
    onCategoryChange(category) {
      this.selectedCategory = category
    },
    changePage(selectedPage) {
      this.page = selectedPage
      this.getData(`?page=${selectedPage}`)
    },
  },
}
</script>

<style>
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
</style>
