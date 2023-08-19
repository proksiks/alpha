<template>
  <div class="hero" :style="{ backgroundImage: `url(${image})` }">
    <div class="container">
      <div class="hero__title">{{ title }}</div>
    </div>
  </div>
</template>

<script setup>
  const props = defineProps({
    title: {
      type: String,
    },
    image: {
      type: String,
    },
  });
</script>

<style scoped>
  .hero {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 50px 0;
    min-height: 320px;

    background-repeat: no-repeat;
    background-size: cover;
    background-position: bottom right;
  }
  @media (max-width: 1280px) {
    .hero {
      background-position: center;
    }
  }
  @media (max-width: 480px) {
    .hero {
      min-height: 160px;
    }
  }
  .hero__title {
    font-size: 40px;
    font-weight: 700;
    line-height: 1.2;
    letter-spacing: -0.01em;
  }
</style>
