<template>
  <div class="mt-8">
    <BookDetail :book="book" />
  </div>
</template>
<script>
import BookDetail from "../components/molecules/BookDetail.vue";
export default {
  components: {
    BookDetail
  },
  data() {
    return {
      id: this.$route.params.id
    };
  },
  computed: {
    book() {
      return this.$store.getters.book;
    }
  },
  created() {
    // watch the path of the route to fetch the data again
    this.$watch(
      () => this.$route.params.id,
      () => {
        this.fetchBook(this.id);
      },
      // fetch the data when the view is created and the data is
      // already being observed
      { immediate: true }
    );
  },
  mounted() {
    this.fetchBook(this.id);
  },
  methods: {
    async fetchBook() {
      try {
        await this.$store.dispatch("fetchBook", this.id);
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>
