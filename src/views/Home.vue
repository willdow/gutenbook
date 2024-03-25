<template>
  <div class="relative overflow-hidden bg-white">
    <div class="mx-auto max-w-7xl">
      <div
        class="relative z-10 bg-white pb-8 pt-1 sm:pb-14 lg:w-full lg:max-w-2xl"
      >
        <main
          class="mx-auto mt-10 max-w-7xl px-4 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28"
        >
          <div class="sm:text-center lg:text-left">
            <h1
              class="text-4xl font-extrabold tracking-tight text-gray-900 sm:text-5xl md:text-6xl"
            >
              <span class="block text-indigo-600 xl:inline">Break down</span>
              <span class="block xl:inline">
                the bars of ignorance and illiteracy.</span
              >
            </h1>
            <p
              class="mt-3 text-base text-gray-500 sm:mx-auto sm:mt-5 sm:max-w-xl sm:text-lg md:mt-5 md:text-xl lg:mx-0"
            >
              Project Gutenberg’s bookshelves are hand-curated collections of
              eBooks that have similar topics.
            </p>
            <div class="mt-10 sm:mt-12">
              <div class="sm:mx-auto sm:flex sm:max-w-xl lg:mx-0">
                <div class="min-w-0 flex-1">
                  <label for="book" class="sr-only">Enter a book</label>
                  <input
                    id="book"
                    v-model="searchText"
                    type="text"
                    name="book"
                    placeholder="Tape something..."
                    class="block w-full rounded-md border border-gray-300 px-4 py-3 text-base text-gray-900 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-700"
                  />
                  <!-- @keyup.enter="submit()" -->
                </div>
                <div class="mt-3 sm:ml-3 sm:mt-0">
                  <router-link
                    class="flex w-full items-center justify-center rounded-md border border-transparent bg-indigo-600 px-8 py-3 text-base font-medium text-white hover:bg-indigo-700"
                    :to="{
                      name: 'Search',
                      query: { q: searchText }
                    }"
                  >
                    Search
                  </router-link>
                </div>
              </div>
            </div>
            <div
              class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start"
            >
              <div class="rounded-md">
                <router-link
                  class="flex w-full items-center justify-center rounded-md border border-transparent bg-indigo-100 px-8 py-3 text-base font-medium text-indigo-700 hover:bg-indigo-200"
                  to="/languages"
                >
                  Find books by language
                </router-link>
              </div>
            </div>
            <div
              class="mt-5 flex flex-col items-center justify-center sm:items-start sm:justify-start"
            >
              <a
                href="https://github.com/willdow/gutenbook"
                class="text-base text-gray-500 hover:text-indigo-900"
              >
                App repository
              </a>
              <a
                href="https://www.gutenberg.org/"
                class="text-base text-gray-500 hover:text-indigo-900"
              >
                The Gutenberg project
              </a>
            </div>
          </div>
        </main>
      </div>
    </div>
    <div class="lg:absolute lg:inset-y-0 lg:right-0 lg:top-28 lg:w-1/2">
      <img
        class="h-full w-full object-cover"
        src="/img/book.jpg"
        alt="Image de couverture"
      />
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    searchText: ""
  }),
  methods: {
    // submit() {
    //   return this.$router.push({
    //     name: "Search",
    //     params: { q: this.searchText}
    //   });
    // }
  }
};
</script>
