<template>
  <div
    class="
      relative
      h-56
      w-full
      flex
      items-end
      justify-start
      text-left
      bg-cover bg-center
    "
    :style="bgImage(product.image)"
  >
    <div
      class="
        absolute
        top-0
        mt-20
        right-0
        bottom-0
        left-0
        bg-gradient-to-b
        from-transparent
        to-gray-900
      "
    ></div>
    <main
      v-if="product"
      class="
        p-2
        w-full
        text-center
        opacity-70
        bg-black
        flex flex-col
        justify-center
        z-10
      "
    >
      <span
        href="#"
        class="
          text-md
          tracking-tight
          font-medium
          leading-7
          font-regular
          text-white
        "
        >{{ product.name }}
      </span>
      <span
        href="#"
        class="
          text-md
          tracking-tight
          font-medium
          leading-7
          font-regular
          text-white
        "
        >$&nbsp;{{ product.price }}
      </span>
    </main>
  </div>
</template>
<script>
export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    bgImage(image) {
      return 'background-image: url("' + image + '")'
    },
  },
}
</script>
