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
  height: $gap-header * 2;
  padding: 0 $gap-header;
  font-family: "Inter", sans-serif;
  line-height: normal;
}

.logo__img {
  margin-right: $gap-header-small;
}
</style>
