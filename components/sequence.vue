<template>
  <div v-if="arrr && arrr.length > 0">
    <div v-for="item in arrr" :key="item.name" class="flex p-2">
      <button
        :key="item"
        :style="[
          page === item
            ? 'bg-blue-500 text-white '
            : 'bg-white text-gray-700 hover:text-gray-500',
          'hidden md:inline-flex -ml-px relative items-center px-4 py-2 border border-gray-300 text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150',
        ]"
        @click="handlePageChange(item)"
      >
        {{ item }}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'SequenceGenerator',
  props: {
    arrr: {
      type: Array,
      default: () => {},
    },
    page: {
      type: Number,
      default: 1,
    },
  },
  methods: {
    handlePageChange(page) {
      this.$emit('changePage', page)
    },
  },
}
</script>
