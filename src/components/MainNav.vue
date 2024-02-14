<script setup>
import { LINKS } from "../settings/data";

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
}
</style>
