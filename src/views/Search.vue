<template>
  <div class="mt-8">
    <div class="flex flex-row-reverse">
      <button
        type="button"
        class="px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
        @click="isRegexSearch = !isRegexSearch"
      >
        {{ isRegexSearch ? "Switch Simple Search" : "Switch Advanced Search" }}
      </button>
    </div>
    <div v-if="!isRegexSearch">
      <div class="pt-4">
        <div
          class="py-5 border-t border-b sm:grid sm:grid-cols-4 sm:items-start sm:gap-4 sm:border-gray-200"
        >
          <label for="book" class="block text-sm font-medium text-gray-700">
            Find your book
          </label>
          <div class="sm:col-span-2">
            <div>
              <input
                id="book"
                v-model="searchText"
                type="text"
                name="book"
                autocomplete="given-name"
                class="block w-full border-gray-300 rounded-md shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
              />
              <!-- @keyup.enter="submit()" -->
            </div>
            <p id="book-description" class="mt-2 text-sm text-gray-500">
              example : alice adventure
            </p>
          </div>
          <router-link
            class="inline-flex justify-center px-4 py-2 ml-3 text-sm font-medium text-white bg-indigo-600 border border-transparent rounded-md shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 sm:col-span-1 sm:w-16"
            :to="{
              query: { q: searchText }
            }"
          >
            Search
          </router-link>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="pt-4">
        <div
          class="py-5 border-t border-b sm:grid sm:grid-cols-4 sm:items-start sm:gap-4 sm:border-gray-200"
        >
          <label for="book" class="block text-sm font-medium text-gray-700">
            Using regular expression
          </label>
          <div class="sm:col-span-2">
            <div>
              <input
                id="book"
                v-model="searchText"
                type="text"
                name="book"
                class="block w-full border-gray-300 rounded-md shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
              />
              <!-- @keyup.enter="submit()" -->
            </div>
            <p id="book-description" class="mt-2 text-sm text-gray-500">
              example : [alice*] please don't forget to add brackets []
            </p>
          </div>
          <router-link
            class="inline-flex justify-center px-4 py-2 ml-3 text-sm font-medium text-white bg-indigo-600 border border-transparent rounded-md shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 sm:col-span-1 sm:w-16"
            :to="{
              query: { q: searchText, page: 1 }
            }"
          >
            Search
          </router-link>
        </div>
      </div>
    </div>
    <div v-if="word" class="my-4 text-sm font-medium text-gray-700">
      Results for {{ word }} :
    </div>
    <div v-if="books.results">
      <BookList :books="books.results" />
      <!-- <Pagination
        :books="books"
        :page="page"
        :page-name="`search?q=${word}`"
      /> -->
    </div>
  </div>
</template>
<script>
import BookList from "../components/molecules/BookList.vue";
// import Pagination from "../components/molecules/Pagination.vue";

export default {
  components: {
    BookList
    // Pagination
  },
  data: () => ({
    isRegexSearch: false,
    searchText: ""
  }),
  computed: {
    books() {
      return this.$store.state.books;
    },
    word() {
      return this.$route.query.q;
    }
  },
  mounted() {
    this.fetchSearch();
  },
  created() {
    // watch the params of the route to fetch the data again
    this.$watch(
      () => this.$route.params,
      () => {
        this.fetchSearch();
      },
      // fetch the data when the view is created and the data is
      // already being observed
      { immediate: true }
    );
  },
  methods: {
    async fetchSearch() {
      try {
        await this.$store.dispatch("fetchSearch", {
          word: this.word
        });
      } catch (error) {
        console.log(error);
      }
    }
    // submit() {
    //   return this.$router.push({
    //     name: "Search",
    //     params: { q: this.searchText}
    //   });
    // }
  }
};
</script>
