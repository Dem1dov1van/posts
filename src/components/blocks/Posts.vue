<template>
  <section class="posts">
    <div class="posts__top-filter">
      <div class="posts__select">
        <a-select
          :value="value"
          mode="multiple"
          placeholder="Выберите автора"
          :options="
            users.map((user) => ({
              value: user.name,
              id: user.id,
            }))
          "
          @change="handleChange"
        >
        </a-select>
      </div>

      <div class="posts__date-picker">
        <DatePickerRange @changeDate="handleChangeDate" />
      </div>
    </div>
    <div v-if="filteredPosts.length" class="posts__wrapper">
      <Post v-for="post in sortPosts(filteredPosts)" :key="post.id" :post="post" />
    </div>
    <div v-else class="posts__no-found">
      <p>Упс, по вашему запросу ничего не найдено</p>
      <img src="../../assets/img/no-found.jpg" alt="no-found">
    </div>
  </section>
</template>

<script>
import Post from "@/components/Post.vue";
import DatePickerRange from "@/components/DatePickerRange.vue";
export default {
  props: {
    posts: Array,
    users: Array,
  },
  data() {
    return {
      selectedAuthors: [],
      startDate: "",
      endDate: "",
    };
  },
  components: {
    Post,
    DatePickerRange,
  },
  methods: {
    handleChange(a, selectedArr) {
      this.selectedAuthors = selectedArr;
    },
    handleChangeDate([start, end]) {
      this.startDate = start;
      this.endDate = end;
    },
    sortPosts(arr){
      return arr.sort((a, b)=> Date.parse( b.date) - Date.parse( a.date))
    }
  },
  computed: {
    filteredPosts() {
      if (!this.selectedAuthors.length && !this.startDate && !this.endDate) {
        return this.posts;
      }
      let filtered;
      if (!this.selectedAuthors.length) {
        filtered = this.posts.filter(
          (post) =>
            Date.parse(post.date) > Date.parse(this.startDate) &&
            Date.parse(post.date) < Date.parse(this.endDate)
        );
        return filtered;
      }
      if (!this.startDate && !this.endDate) {
        filtered = this.posts.filter((post) =>
          this.selectedAuthors.some((author) => author.id === post.userId)
        );
        return filtered;
      }
      return this.posts.filter(
        (post) =>
          this.selectedAuthors.some((author) => author.id === post.userId) &&
          Date.parse(post.date) > Date.parse(this.startDate) &&
          Date.parse(post.date) < Date.parse(this.endDate)
      );
    },
  },
};
</script>
