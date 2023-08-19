<template>
  <article class="article" v-if="post">
    <div class="article__cover" v-if="post.image">
      <img class="article__img" :src="post.image" :alt="post.name" />
    </div>
    <time class="article__date" :datetime="formatedDate.fullDate.toISOString()">
      <div class="article__date-day">
        {{ formatedDay }}
      </div>
      <div class="article__date-content">
        <div class="article__date-month">{{ formatedDate.month }}</div>
        <div class="article__date-year">{{ formatedDate.year }}</div>
      </div>
    </time>
    <h3 class="article__title" v-if="post.name">{{ post.name }}</h3>
    <p class="article__descr" v-if="post.previewText">{{ post.previewText }}</p>
    <div class="article__footer">
      <div class="article__type">Новости</div>
    </div>
  </article>
</template>

<script setup>
  import { defineProps, computed } from "vue";

  const monthNames = [
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December",
  ];

  const props = defineProps({
    post: {
      type: Object,
      required: true,
    },
  });

  const formatedDay = computed(() => {
    return formatedDate.value.day < 10 ? `0${formatedDate.value.day}` : formatedDate.value.day;
  });

  const formatedDate = computed(() => {
    const date = new Date(props.post.date * 1000);
    const year = date.getFullYear();
    const day = date.getDay() + 1;
    const month = monthNames[date.getMonth()];

    return { fullDate: date, month, year, day };
  });
</script>

<style scoped>
  .article {
    display: flex;
    flex-direction: column;

    height: 100%;

    border-radius: 16px;
    border: 1px solid var(--border-blue-color);
  }
  .article__cover {
    position: relative;

    padding-bottom: 48%;
    margin: -1px;
  }
  .article__img {
    position: absolute;
    inset: 0;

    max-width: 100%;
    width: 100%;
    height: 100%;
    object-fit: cover;

    border-radius: 14px 14px 0 0;
  }
  .article__date {
    display: flex;

    margin-top: var(--inner-indent);
    padding-left: var(--inner-indent);
    padding-right: var(--inner-indent);
    margin-bottom: 16px;
  }
  @media (max-width: 1024px) {
    .article__date {
      margin-top: var(--inner-small-indent);
      padding-left: var(--inner-small-indent);
      padding-right: var(--inner-small-indent);
    }
  }
  .article__date-day {
    color: var(--text-gray-color);
    font-size: 36px;
    line-height: 1;

    margin-right: 4px;
  }
  .article__date-content {
    color: var(--text-gray-color);
    font-size: 15px;
    font-weight: 700;
    line-height: 1.1;
    letter-spacing: -0.15px;
  }
  .article__title {
    margin: 0;

    color: var(--text-blue-color);
    font-size: 22px;
    line-height: 1.2;

    padding-left: var(--inner-indent);
    padding-right: var(--inner-indent);
    margin-bottom: 16px;
  }
  @media (max-width: 1024px) {
    .article__title {
      font-size: 18px;
      padding-left: var(--inner-small-indent);
      padding-right: var(--inner-small-indent);
    }
  }
  @media (max-width: 480px) {
    .article__title {
      font-size: 16px;
    }
  }
  .article__descr {
    margin: 0;

    color: var(--text-dark-color);
    font-size: 20px;
    line-height: 1.3;
    letter-spacing: -0.2px;

    padding-left: var(--inner-indent);
    padding-right: var(--inner-indent);
    margin-bottom: 40px;
  }
  @media (max-width: 1024px) {
    .article__descr {
      font-size: 16px;
      padding-left: var(--inner-small-indent);
      padding-right: var(--inner-small-indent);
    }
  }
  @media (max-width: 480px) {
    .article__descr {
      font-size: 14px;
    }
  }
  .article__footer {
    margin-top: auto;
    margin-bottom: var(--inner-indent);
    margin-left: var(--inner-indent);
    margin-right: var(--inner-indent);
  }
  @media (max-width: 1024px) {
    .article__footer {
      margin-bottom: var(--inner-small-indent);
      margin-left: var(--inner-small-indent);
      margin-right: var(--inner-small-indent);
    }
  }
  .article__type {
    display: inline-block;
    border-radius: 40px;
    background: var(--main-bg);
    padding: 4px 16px;

    color: var(--text-dark-blue-color);
    font-size: 14px;
    line-height: 1.4;
  }
  .article__type:not(:last-child) {
    margin-right: 4px;
  }
</style>
