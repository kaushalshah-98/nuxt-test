<template>
  <div as="nav" class="bg-gray-800">
    <div class="mx-auto px-2 sm:px-6 lg:px-8">
      <div class="relative flex items-center justify-between h-16">
        <div
          class="
            flex-1 flex
            items-center
            justify-center
            sm:items-stretch
            sm:justify-start
          "
        >
          <!-- <div class="flex-shrink-0 flex items-center">
            <img
              class="block lg:hidden h-8 w-auto"
              src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg"
              alt="Workflow"
            />
            <img
              class="hidden lg:block h-8 w-auto"
              src="https://tailwindui.com/img/logos/workflow-logo-indigo-500-mark-white-text.svg"
              alt="Workflow"
            />
          </div> -->
          <div class="hidden sm:block sm:ml-6">
            <div class="flex space-x-4">
              <div v-for="item in navigation" :key="item.name">
                <NuxtLink
                  :to="item.href"
                  :class="[
                    item.current
                      ? 'bg-gray-900 text-white'
                      : 'bg-gray-900 text-white',
                    'px-3 py-2 rounded-md text-sm font-medium',
                  ]"
                  :aria-current="item.current ? 'page' : undefined"
                  @click="onClick(item)"
                  >{{ item.name }}</NuxtLink
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="sm:hidden">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <div v-for="item in navigation" :key="item.name">
          <NuxtLink
            :to="item.href"
            :class="[
              item.current
                ? 'bg-gray-900 text-white'
                : 'bg-gray-900 text-white',
              'px-3 py-2 rounded-md text-sm font-medium',
            ]"
            :aria-current="item.current ? 'page' : undefined"
            @click="onClick(item)"
            >{{ item.name }}</NuxtLink
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
  components: {},
  data() {
    return {
      navigation: [
        { name: 'Home', href: '/', current: true },
        { name: 'Products', href: '/products', current: false },
      ],
    }
  },
  methods: {
    onClick(item) {
      this.navigation = this.navigation.map((i) => (i.current = false))
      this.navigation = this.navigation.map((i) =>
        i.name === item.name ? (i.current = true) : null
      )
    },
  },
}
</script>
