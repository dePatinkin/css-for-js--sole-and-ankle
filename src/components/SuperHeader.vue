<script setup>
import IconSearch from "~icons/feather/search";
import IconShoppingBag from "~icons/feather/shopping-bag";
</script>

<template>
  <div class="super-header">
    <span class="marketing-message">Free shipping on domestic orders over $75!</span>
    <menu>
      <span class="search">
        <label>
          <IconSearch />
          <input type="text" placeholder="Search..."></input>
        </label>
      </span>
      <a href="/help">Help</a>
      <a href="/cart" class="graphics-wrapper">
        <IconShoppingBag />
      </a>
    </menu>
  </div>
</template>

<style scoped lang="scss">
@import "../settings/variables";

.super-header {
  display: flex;
  justify-content: space-between;
  font-size: 0.875rem;
  color: $color-white;
  background-color: $color-gray-900;
  display: flex;
  align-items: center;
  padding: 0.75rem 2rem; //0.75rem 32px;

  svg,
  p,
  a,
  span {
    color: inherit;
  }

  menu {
    display: flex;
    justify-content: flex-end;
    gap: 1.5rem;
    align-items: center;

    a {
      text-decoration: none;
    }

    svg {
      width: 1.5rem;
      height: 1.5rem;
    }

    .search {

      svg {
        width: 1rem;
        height: 1rem;
        position: absolute;
        top: 0.4rem;
        left: 0rem;
      }

      label {
        position: relative;
        display: inline-block;
        border-bottom: 1px solid $color-gray-300;
        height: 100%;
        //width: 11rem;
        padding: 0.25rem 0;
      }

      input {
        border: none;
        //border-bottom: 1px solid $color-gray-300;
        color: inherit;
        background: transparent; //background-color: inherit;
        //font-size: 0.875rem;
        margin-inline: 0.5rem;
        padding: 0 0 0 1rem;
        outline-offset: .65rem;

        &::placeholder {
          color: $color-gray-500;
        }
      }
    }
  }
}
</style>
