<template>
  <div v-if="totalpages !== 0 && page" class="flex justify-center py-5">
    <div
      class="
        bg-white
        px-4
        py-2
        flex
        items-center
        justify-between
        border-t border-gray-200
        sm:px-6
      "
    >
      <div class="flex items-center justify-between">
        <nav class="relative z-0 flex shadow-sm">
          <button
            :class="[
              start <= 1 ? 'cursor-not-allowed' : '',
              '-ml-px relative inline-flex items-center p-2 rounded-r-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-500 hover:text-gray-400 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150',
            ]"
            aria-label="Previous"
            @click="Previous"
          >
            <ChevronLeftIcon size="2x" />
          </button>
          <div v-for="item in arrr" :key="item.name">
            <a
              :key="item"
              :class="[
                page == item
                  ? 'bg-blue-500 text-white '
                  : 'bg-white text-gray-700 hover:text-gray-500',
                'cursor-pointer md:inline-flex relative items-center px-4 py-3 border border-gray-300 text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150',
              ]"
              @click="changePage(item)"
            >
              {{ item }}
            </a>
          </div>
          <button
            :class="[
              end >= totalpages ? 'cursor-not-allowed' : '',
              '-ml-px relative inline-flex items-center p-2 rounded-r-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-500 hover:text-gray-400 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150',
            ]"
            aria-label="Next"
            @click="Next"
          >
            <ChevronRightIcon size="2x" />
          </button>
        </nav>
      </div>
    </div>
  </div>
</template>
<script>
import { ChevronLeftIcon, ChevronRightIcon } from 'vue-feather-icons'

export default {
  name: 'ProductCard',
  components: { ChevronLeftIcon, ChevronRightIcon },
  props: {
    page: { type: Number, default: 1 },
    totalpages: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      arrr: [1],
      numbersToShow: 4,
    }
  },
  computed: {
    start() {
      return this.arrr[0]
    },
    end() {
      return this.arrr[this.arrr.length - 1]
    },
  },
  watch: {
    totalpages(newVal, oldVal) {
      this.arrr =
        this.totalpages > 4
          ? [
              ...Array?.from(
                Array(this.numbersToShow ? this.numbersToShow : 4),
                (_, i) => i + 1
              ),
            ]
          : [...Array?.from(Array(this.totalpages), (_, i) => i + 1)]
    },
  },

  created() {
    this.arrr =
      this.totalpages > 4
        ? [
            ...Array?.from(
              Array(this.numbersToShow ? this.numbersToShow : 4),
              (_, i) => i + 1
            ),
          ]
        : [...Array?.from(Array(this.totalpages), (_, i) => i + 1)]
  },

  methods: {
    range(from, to, step = 1) {
      const rangee = []
      for (let i = from; i <= to; i += step) {
        rangee.push(i)
      }
      return rangee
    },
    Previous(event) {
      event.preventDefault()
      if (this.start <= 1) return
      if (this.end === this.totalpages) {
        this.right = this.start - 1
      } else {
        this.right = this.right - this.numbersToShow
      }
      const numarr = this.range(this.start - this.numbersToShow, this.right)
      this.arrr = numarr
    },
    Next(event) {
      event.preventDefault()
      if (this.end >= this.totalpages) return
      if (this.right + this.numbersToShow >= this.totalpages) {
        this.right = this.totalpages
      } else {
        this.right = this.right + this.numbersToShow
      }
      const numarr = this.range(this.start + this.numbersToShow, this.right)
      this.arrr = numarr
    },
    changePage(page) {
      this.$emit('changePage', page)
    },
  },
}
</script>
