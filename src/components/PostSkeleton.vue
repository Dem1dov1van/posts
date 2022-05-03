<template>
  <div class="posts__post-card post-card post-card--skeleton">
    <div class="post-card__top">
        <a-skeleton :active="true" :paragraph="{ rows: 0 }"  />
    </div>
    <div class="post-card__body">
        <!-- <a-skeleton-paragraph :active="active"  /> -->
        <a-skeleton :active="true" :title="false" :paragraph="{ rows: 4, width:[200, 250, 220, 250,] }"  />
      <div class="post-card__info">
        <a-space>
          <a-skeleton-button
            :active="true"
            style="width: 105px"
            :size="'small'"
            :block="true"
            :shape="'round'"
          />
          <a-skeleton-button
            :active="true"
            style="width: 105px"
            :size="'small'"
            :block="true"
            :shape="'round'"
          />
        </a-space>
      </div>
    </div>
  </div>
</template>
