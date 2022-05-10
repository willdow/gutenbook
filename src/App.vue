<template>
  <div>
    <nav class="bg-gray-800">
      <div class="w-full max-w-screen-xl px-4 mx-auto sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <img class="w-8 h-8" src="/img/logos/swam.svg" alt="Logo" />
            </div>
            <div class="flex justify-between">
              <div class="block">
                <div class="flex items-baseline ml-10">
                  <router-link
                    v-for="(link, i) in links"
                    :key="i"
                    v-slot="{ navigate, href, isExactActive }"
                    :to="link.to"
                    custom
                  >
                    <a
                      :href="href"
                      class="px-3 py-2 text-sm font-medium rounded-md"
                      :class="[
                        isExactActive
                          ? 'bg-gray-900 text-white focus:bg-gray-700 focus:text-white focus:outline-none'
                          : 'text-gray-300 hover:bg-gray-700 hover:text-white focus:bg-gray-700 focus:text-white focus:outline-none',
                        i > 0 && 'ml-4'
                      ]"
                      @click="navigate"
                      >{{ link.text }}</a
                    >
                  </router-link>
                </div>
              </div>
            </div>
          </div>
          <!-- Search section -->
          <div class="flex">
            <div class="flex justify-center flex-1 lg:justify-end">
              <div class="w-full px-2">
                <label for="book" class="sr-only">Search</label>
                <div
                  class="relative text-indigo-200 focus-within:text-gray-400"
                >
                  <input
                    id="book"
                    v-model="searchText"
                    type="text"
                    name="book"
                    placeholder="Search something..."
                    class="block w-full py-2 pl-3 pr-3 leading-5 text-indigo-100 placeholder-indigo-200 bg-indigo-400 bg-opacity-25 border border-transparent rounded-md focus:bg-white focus:text-gray-900 focus:placeholder-gray-400 focus:outline-none focus:ring-0 sm:text-sm"
                  />
                  <!-- @keyup.enter="submit()" -->
                </div>
              </div>
            </div>
            <router-link
              class="px-3 py-2 text-sm font-medium rounded-md cursor-pointer"
              :to="{
                name: 'Search',
                query: { q: searchText, page: 1, limit: limit }
              }"
            >
              <svg
                class="w-5 h-5 text-white"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                aria-hidden="true"
              >
                <path
                  fill-rule="evenodd"
                  d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                  clip-rule="evenodd"
                />
              </svg>
            </router-link>
          </div>
        </div>
      </div>
    </nav>

    <main class="max-w-screen-xl px-6 mx-auto lg:px-8">
      <router-view />
    </main>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  data: () => ({
    showMenu: false,
    showProfileMenu: false,
    links: [
      {
        text: "Gutenberg",
        to: "/"
      },
      {
        text: "Popular",
        to: "/popular"
      },
      {
        text: "Language",
        to: "/languages"
      },
      {
        text: "Random",
        to: "/random"
      },
      {
        text: "About",
        to: "/about"
      }
    ],
    searchText: ""
  }),
  computed: {
    limit() {
      return this.$store.state.limit;
    }
  },
  methods: {
    // submit() {
    //   return this.$router.push({
    //     name: "Search",
    //     params: { q: this.searchText, page: 1, limit: this.limit }
    //   });
    // }
  }
});
</script>
