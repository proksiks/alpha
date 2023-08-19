<template>
  <header class="header">
    <div class="container">
      <img src="/images/logo.svg" alt="Логотип компании Alpha" class="header__logo" />
    </div>
  </header>
</template>

<style scoped>
  .header {
    box-shadow: 0px 8px 16px 0px #00000014;
    background-color: white;
    padding: 40px 0;
  }
  @media (max-width: 480px) {
    .header {
      padding: 12px 0;
    }
  }
  .header__logo {
    display: block;
    max-width: 100%;
  }
  @media (max-width: 480px) {
    .header__logo {
      max-width: 92px;
      width: 100%;
    }
  }
</style>
