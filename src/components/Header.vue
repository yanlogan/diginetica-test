<script setup>
import Logo from "./Logo.vue";
import Search from "./Search.vue";
import { useMedia } from "../composables/useMedia";

const isMobile = useMedia("(max-width: 968px)");
</script>

<template>
  <header class="header">
    <Logo />
    <button type="button" id="header-catalog" class="header__catalog">
      Каталог
    </button>
    <Search
      id="header-search"
      :show-search-btn="true"
      :placeholder="isMobile ? '' : 'Поиск по 100 000 товаров'"
      :isHeader="true"
      classes="header__search"
    />
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

  @include laptop {
    padding: calc($gap-header / 2) 28px;
  }

  @include mobile {
    padding: 0;
    padding-top: 8px;
  }
}
.header .logo {
  @include mobile {
    display: none;
  }
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

  @include mobile {
    display: none;
  }
}
.header__search {
  margin: 0 $gap-header;
  padding: 4px 4px 4px 16px;
  border-radius: 10px;

  .search__input {
    font-size: $font-size-big;
    line-height: 150%;
  }

  @include mobile {
    margin: 0;
    padding: 0;
  }
}
.header__nav {
  display: flex;
  align-items: center;
  white-space: nowrap;

  ul {
    @include list(r, 20px);
    a:not(:hover) {
      color: #393939;
    }
  }

  @include tablet {
    display: none;
  }
}
</style>
