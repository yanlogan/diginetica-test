<script setup>
import Logo from "./Logo.vue";
import Search from "./Search.vue";
</script>

<template>
  <header class="header">
    <Logo />
    <a class="header__catalog" href="#">Каталог</a>
    <Search />
    <nav class="header__nav">
      <ul>
        <li><a href="#">Информация о компании</a></li>
        <li><a href="#">Контакты</a></li>
        <li><a href="#">Полезные ссылки</a></li>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss">
.header {
  display: flex;
  align-items: stretch;
  padding: calc($gap-header / 2) 0;
  font-family: "Inter", sans-serif;
  font-size: $font-size-normal;
}
.header__catalog {
  display: flex;
  align-items: center;
  margin-left: $gap-header-small;
  padding: $gap-header-small $gap-header;
  font-weight: 500;
  border: 1px solid $color-border;
  border-radius: $gap-header-small;

  &:hover {
    color: $color-font-main;
    border-color: $color-border-hover;
  }
}
.header__nav {
  display: flex;
  align-items: center;

  ul {
    @include list(r, 20px);
    a:not(:hover) {
      color: #393939;
    }
  }
}
</style>
