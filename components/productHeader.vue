<template>
  <div class="flex space-x-4 px-12 pt-6">
    <div
      class="
        bg-white
        flex
        w-11/12
        items-center
        border border-gray-400
        rounded-full
        shadow-xl
      "
    >
      <input
        id="search"
        v-model="searchString"
        class="
          rounded-l-full
          w-full
          p-2
          text-gray-700
          leading-tight
          focus:outline-none
        "
        type="text"
        placeholder="Enter .."
      />

      <div class="p-2">
        <button
          class="
            bg-blue-500
            text-white
            rounded-full
            px-4
            py-2
            hover:bg-blue-400
            focus:outline-none
            flex
            items-center
            justify-center
          "
          @click="onSearch"
        >
          Search
        </button>
      </div>
    </div>
    <select
      v-model="selectedValue"
      class="
        mt-1
        block
        w-1/12
        py-2
        px-3
        border border-gray-300
        bg-white
        rounded-md
        shadow-sm
        focus:outline-none
        focus:ring-indigo-500
        focus:border-indigo-500
        sm:text-sm
      "
      @change="onCategoryChange"
    >
      <option value="">All</option>
      <option v-for="item in categories" :key="item" :value="item">
        {{ item }}
      </option>
    </select>
  </div>
</template>
<script>
export default {
  name: 'ProductHEader',
  props: {
    categories: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return { selectedValue: null, searchString: '' }
  },
  methods: {
    onSearch() {
      this.$emit('onSearch', this.searchString)
    },
    onCategoryChange() {
      this.$emit('onCategoryChange', this.selectedValue)
    },
  },
}
</script>
<style></style>
