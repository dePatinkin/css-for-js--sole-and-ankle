<script setup>
import { shallowRef } from "vue";
import IconChevronDown from "~icons/feather/chevron-down";
import IconChevronUp from "~icons/feather/chevron-up";
import ShoeSidebar from "./ShoeSidebar.vue";
import ShoeCard from "./ShoeCard.vue";
import { LINKS, SHOES } from "../settings/data";

const title = shallowRef("All");
const current1 = "/" + (window.location.pathname.slice(1) || "sale");
const breadcrumb1 = LINKS.find((i) => i.path === current1);
const breadcrumb2 = shallowRef({ text: "All", path: "/" });
const onTitleChanged = (e) => {
  title.value = e?.text;
  breadcrumb2.value = e;
};

const sortOptions = [
  { text: "Newest Releases", value: "newest" },
  { text: "Price", value: "price" },
  { text: "xxx", value: "xxx" },
];
const sortSelected = shallowRef(null); //shallowRef(sortOptions[0].value);
</script>

<template>
  <div class="shoe-index">
    <main>
      <header>
        <h2>{{ title }}</h2>
        <label class="sortSelection"><span>Sort</span>
          <div class="custom-select-wrapper">
            <select>
              <option v-for="{ text, value } in sortOptions" value="value">
                {{ text }}
              </option>
            </select>
          </div>
        </label>
      </header>
      <div class="shoes-container">
        <ShoeCard v-for="shoe in SHOES" v-bind="shoe" />
      </div>
    </main>
    <aside>
      <section class="breadcrumbs">
        <nav>
          <a :href="breadcrumb1?.path">{{ breadcrumb1?.text }}</a>
          <a :href="breadcrumb2?.path">{{ breadcrumb2?.text }}</a>
        </nav>
      </section>
      <ShoeSidebar @currentChanged="onTitleChanged" />
    </aside>
  </div>
</template>

<style scoped lang="scss">
@import "../settings/variables";

.shoe-index {
  display: flex;
  flex-direction: row-reverse;
  justify-content: flex-end;
  padding-block: 4rem 2.5rem; //64px 40px;
  padding-inline: 2rem 2.75rem; //32px 28px;

  main {
    // display: flex;
    // flex-direction: row;
    // flex-wrap: wrap;
    // gap: 2rem;

    .shoes-container {
      // display: flex;
      // flex-wrap: wrap;
      // gap: 2rem;
      float: inline-start;
      width: 100%;
    }

    header {
      h2 {
        font-size: 1.5rem;
        line-height: 1.5rem;
        float: inline-start;
      }

      .sortSelection {
        float: inline-end;
      }

      label>span {
        padding-inline: 1rem;
      }
    }

    .custom-select-wrapper {
      display: inline;
      //position: relative;

      select {
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
      }

      select::-ms-expand {
        display: none;
      }

      /* Icon */
      select {
        background: transparent;
        background-image: url("data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cGF0aCBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIGQ9Im02IDlsNiA2bDYtNiIvPjwvc3ZnPg==");
        background-size: 1.5rem;
        background-repeat: no-repeat;
        background-position-x: 94%;
        background-position-y: 0.72rem;
      }

      select {
        font-size: 1rem;
        font-weight: $weight-medium;
        padding: 0.7rem 1rem;
        width: 11.875rem;
        border: 0;
        border-radius: 8px;
        color: inherit;
        background-color: $color-gray-100;
      }
    }
  }

  aside {
    display: flex;
    flex-direction: column;
    min-width: 15.5rem; //11.875rem;
    padding-inline-end: 2rem;

    .breadcrumbs {
      margin-block-end: 2.25rem;
      min-height: 45.6px;
      justify-self: center;

      nav {
        display: flex;
        font-size: 0.875rem;
      }

      a {
        color: $color-gray-500;

        &:hover {
          color: $color-gray-900;
        }

        &:not(:last-of-type)::after {
          content: "/";
          margin-inline: 0.5rem;
          color: $color-gray-300;
        }
      }
    }
  }
}
</style>
