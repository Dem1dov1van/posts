<template>
  <section class="posts">
      <div class="posts__top-filter">
      <div class="posts__select">
           <a-skeleton-input style="width: 100%; min-width: 305px" :active="true" :size="'default'" />
      </div>
      <div class="posts__date-picker">
         <a-skeleton-input style="width: 100%; min-width: 305px" :active="true" :size="'default'" />
      </div>
    </div>
    <div class="posts__wrapper">
      <PostSkeleton v-for="post in 9" :key="post" />
    </div>
  </section>
</template>

<script>
import PostSkeleton from "@/components/PostSkeleton.vue";

export default {
  components: {
    PostSkeleton,
  },
};
</script>
