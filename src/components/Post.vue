<template>
  <div class="posts__post-card post-card">
    <div class="post-card__top">
      <h3 class="post-card__title">{{ post.title }}</h3>
    </div>
    <div class="post-card__body">
      <p class="post-card__paragraph">
        {{ post.body }}
      </p>
      <div class="post-card__info">
        <span class="post-card__badge-text badge-text badge-text--fill">
          {{ post.userName }}
        </span>
        <span class="post-card__badge-text badge-text badge-text--outline">
          {{ getAdaptiveDate(post.date) }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: Object,
  },
  methods: {
    getAdaptiveDate(date) {
      return new Date(date).toLocaleDateString("ru-RU", {
        day: "numeric",
        month: "long",
        year: "numeric",
      });
    },
  },
};
</script>
