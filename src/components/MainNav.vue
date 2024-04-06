<script setup>
import { LINKS } from "../settings/data";
import IconSearch from "~icons/feather/search";
import IconShoppingBag from "~icons/feather/shopping-bag";
import IconMenu from "~icons/feather/menu";

const current = "/" + (window.location.pathname.slice(1) || "sale");
const links = LINKS;
</script>

<template>
  <div class="main-header">
    <div class="logo">
      <a href="/">
        <h1>Sole&amp;Ankle</h1>
      </a>
    </div>
    <nav>
      <a v-for="{ path, text } in links" :key="path" :href="path" :class="{ current: current === path }">
        {{ text }}
      </a>
    </nav>
    <div class="icons">
      <a href="#" class="search-icon">
        <IconSearch />
      </a>
      <a href="/cart" class="graphics-wrapper">
        <IconShoppingBag />
      </a>
      <a href="#" class="graphics-wrapper">
        <IconMenu />
      </a>
      <div class="search">
        <label>
          <input type="text" placeholder="Search..." aria-label="Search" />
        </label>
      </div>
    </div>
    <div class="spacer"></div>
  </div>
</template>

<style scoped lang="scss">
@import "../settings/variables";

.main-header {
  display: flex;
  position: relative;
  align-items: center;
  padding: 1.25rem 2rem;
  border-bottom: 1px solid $color-gray-300;

  a {
    color: inherit;
  }

  .logo,
  .spacer {
    flex: 1;
  }

  .logo {
    //flex: 1;

    a {
      color: inherit;
    }

    h1 {
      font-size: 1.5rem;
      font-weight: $weight-bold;
    }
  }

  nav {
    //flex: 4;
    padding-inline: 1.5rem;
    // position: relative;
    // margin: 0;

    // @media screen and (min-width: 1150px) {
    //   inset: 0;
    //   padding-inline: 10.75rem;
    //   position: absolute;
    //   margin: auto;
    //   width: fit-content;
    //   height: min-content;
    // }

    &>a {
      text-transform: uppercase;
      text-decoration: none;
      padding-inline: 1.5rem;
      font-size: 1.125rem;

      &.current {
        color: $color-secondary;
      }

      &::after {
        /* &zwnj; https://www.compart.com/en/unicode/search?q=space#characters */
        content: '\200B';
      }
    }
  }

  .icons {
    display: none;
  }

  @media (max-width: $breakpoint-md) {
    nav {
      display: none;
    }

    justify-content: space-between;
    align-items: baseline;

    .spacer {
      display: none;
    }

    .icons {
      align-self: center;
      display: grid;
      grid-template-areas: 'bag search menu';
      grid-template-columns: repeat(3, 1.5rem);
      gap: clamp(0.4rem, 6vw - 1rem, rem(34px));
      line-height: 0;
      position: relative;

      .search {
        //display: none;
        position: absolute;
        bottom: -2rem;
        opacity: 0;
        transition: opacity 0.5s ease;
      }

      .search-icon:focus~.search {
        display: block;
        opacity: 1;
      }

      svg {
        width: 1.5rem;
        height: 1.5rem;
        line-height: 0;
      }

      :nth-child(1) {
        grid-area: search;
      }

      :nth-child(2) {
        grid-area: bag;
      }

      :nth-child(3) {
        grid-area: menu;
      }
    }
  }
}
</style>
