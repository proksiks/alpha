<template>
  <footer class="footer">
    <div class="container">
      <div class="footer__info">
        <img src="/images/logo.svg" alt="Логотип компании Alpha" class="footer__logo" />
        <time class="footer__date" :datetime="date"> © alpha, {{ date }} </time>
      </div>
    </div>
  </footer>
</template>

<script setup>
  import { computed } from "vue";

  const date = computed(() => {
    return new Date().getFullYear();
  });
</script>

<style scoped>
  .footer {
    padding: 64px 0;
    background-color: var(--main-bg);
  }
  .footer__date {
    display: block;
    
    color: #81899d;
    font-size: 16px;
    font-weight: 400;
    line-height: 1.4;
  }
</style>
