<template>
  <Header />
  <Slider />
  <Posts v-if="posts.length" :posts="posts" :users="users" />
  <PostsSkeleton v-else />
  <Footer />
</template>

<script>
import Header from "@/components/blocks/Header.vue";
import Slider from "@/components/blocks/Slider.vue";
import Posts from "@/components/blocks/Posts.vue";
import Footer from "@/components/blocks/Footer.vue";
import PostsSkeleton from "@/components/blocks/PostsSkeleton.vue";

export default {
  name: "App",
  components: {
    Header,
    Slider,
    Posts,
    Footer,
    PostsSkeleton,
  },
  data() {
    return {
      posts: [],
      users: [],
    };
  },

  getRandomDate(date1, date2) {
    function getRandomArbitrary(min, max) {
      return Math.random() * (max - min) + min;
    }
    date1 = new Date(date1).getTime();
    date2 = new Date(date2).getTime();
    if (date1 > date2) {
      return new Date(getRandomArbitrary(date2, date1)).toLocaleDateString(
        "en-US",
        { day: "2-digit", month: "2-digit", year: "2-digit" }
      );
    } else {
      return new Date(getRandomArbitrary(date1, date2)).toLocaleDateString(
        "en-US",
        { day: "2-digit", month: "2-digit", year: "2-digit" }
      );
    }
  },
  addresses: ["posts", "users"],
  created() {
    // timeout для наглядности
    setTimeout(() => {
      let requests = this.$options.addresses.map((adress) =>
        fetch(`https://jsonplaceholder.typicode.com/${adress}`)
      );

      Promise.all(requests)
        .then((responses) => Promise.all(responses.map((r) => r.json())))
        .then(([posts, users]) => {
          function setUserName(post) {
            let user = users.find((el) => el.id === post.userId);
            return user ? user.name : "Автор не известен";
          }

          this.posts = posts.map((post) => {
            return {
              ...post,
              userName: setUserName(post),
              date: this.$options.getRandomDate(
                "08.08.2008",
                new Date().toLocaleDateString()
              ),
            };
          });
          this.users = users;
        });
    }, 1000);
  },
};
</script>

<style></style>
