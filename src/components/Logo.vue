<script setup></script>

<template>
  <a class="logo" href="/">
    <img src="../assets/images/logo.svg" alt="Лого" class="logo__img" />
    <span class="logo__text">Логотип</span>
  </a>
</template>

<style lang="scss">
.logo {
  display: flex;
  align-items: center;
  height: 48px;
  padding: 0 24px;
  font-family: "Inter", sans-serif;
  line-height: normal;
}

.logo__img {
  margin-right: 8px;
}
</style>
