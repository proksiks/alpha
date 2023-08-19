<template>
  <Header />
  <Head title="Новости" image="./images/head-bg.jpg" />
  <main class="main">
    <div class="container">
      <ul class="posts">
        <li class="post" v-for="post in sliceArray" :key="post.code">
          <Article :post="post" />
        </li>
      </ul>
      <div class="load-more" v-if="showToggleLoadButton">
        <button class="button" @click="loadMoreProducts">Загрузить ещё</button>
      </div>
    </div>
  </main>
  <Footer />
</template>

<script setup>
  import { ref, computed, onMounted, onBeforeUnmount } from "vue";

  import Header from "@/components/Header.vue";
  import Head from "@/components/Head.vue";
  import Article from "@/components/Article.vue";
  import Footer from "@/components/Footer.vue";

  const URL = "https://flems.github.io/test/api/news";
  const posts = ref({});
  const postsToShow = ref(9);

  async function getApiData() {
    try {
      const response = await fetch(URL);
      const data = await response.json();
      posts.value = data;
    } catch (e) {
      console.error(e);
    }
  }

  getApiData();

  const loadMoreProducts = () => {
    if (postsToShow.value > posts.value.items.length) {
      return;
    } else {
      postsToShow.value = postsToShow.value + 9;
    }
  };

  const sliceArray = computed(() => {
    return posts.value.items?.slice(0, postsToShow.value);
  });

  const showToggleLoadButton = computed(() => {
    return postsToShow.value <= sliceArray.value?.length;
  });

  function checkPostsLength() {
    if (window.innerWidth <= 1024) {
      postsToShow.value = 8;
    } else postsToShow.value = 9;
  }

  onMounted(() => {
    checkPostsLength();
    window.addEventListener("resize", checkPostsLength);
  });
</script>

<style scoped>
  .posts {
    list-style: none;
    padding: 0;
    margin: 0;
    margin-top: 64px;
    margin-bottom: 72px;

    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 64px 48px;
  }
  @media (max-width: 1024px) {
    .posts {
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
    }
  }
  @media (max-width: 768px) {
    .posts {
      grid-template-columns: 1fr;
    }
  }
  .load-more {
    margin-bottom: 72px;
    display: flex;
    justify-content: center;
  }
  .button {
    cursor: pointer;
    color: #002dbf;
    font-size: 20px;
    font-weight: 600;
    line-height: 1.2;
    letter-spacing: -0.2px;
    padding: 16px 32px;
    border: 1px solid #002dbf;
    background-color: transparent;
    border-radius: 8px;
    transition: background-color 0.15s ease;
  }
  .button:hover {
    background-color: rgba(0, 45, 191, 0.1);
  }
  .button:active {
    background-color: rgba(0, 45, 191, 0.2);
  }
</style>
