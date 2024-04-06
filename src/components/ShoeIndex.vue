<script setup>
import { shallowRef, watch } from "vue";
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
];

const sortSelected = shallowRef(sortOptions[0].value);

const sortShoes = () => {
  console.log("sort executed")
  if (sortSelected.value === "price")
    SHOES.sort((a, b) => (a.salePrice || a.price) - (b.salePrice || b.price));
  else if (sortSelected.value === "newest")
    SHOES.sort((a, b) => b.releaseDate - a.releaseDate);
};
sortShoes();

watch(sortSelected, (newv, oldv) => {
  sortShoes();
});
</script>

<template>
  <div class="shoe-index">
    <main>
      <header>
        <section class="breadcrumbs">
          <nav>
            <a :href="breadcrumb1?.path">{{ breadcrumb1?.text }}</a>
            <a :href="breadcrumb2?.path">{{ breadcrumb2?.text }}</a>
          </nav>
        </section>
        <h2>{{ title }}</h2>
        <label class="sortSelection"><span>Sort</span>
          <div class="custom-select-wrapper">
            <select v-model="sortSelected">
              <option v-for="{ text, value } in sortOptions" :value="value">
                {{ text }}
              </option>
            </select>
          </div>
        </label>
      </header>
      <div class="shoes-container">
        <div class="shoe-wrapper" v-for="shoe in SHOES" :key="shoe.slug">
          <ShoeCard v-bind="shoe" />
        </div>
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
  align-items: baseline;
  padding-block: 4rem 2.5rem; //64px 40px;
  padding-inline: 2rem 2.75rem; //32px 28px;

  main {
    display: flex;
    flex-direction: column;
    //flex-direction: row;
    //flex-wrap: wrap;
    gap: 2rem;
    flex: 1;

    .shoes-container {
      display: flex;
      flex-wrap: wrap;
      gap: 2rem;
      // float: inline-start;
      // width: 100%;

      @supports (display: grid) {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
      }

      >.shoe-wrapper {
        flex: 1 0 340px;
      }
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;

      @media screen and (max-width: $breakpoint-md) {
        display: grid;
        grid-template-areas: 'breadcrumbs none' 'title sort';
      }

      h2 {
        font-size: 1.5rem;
        line-height: 1.5rem;
        //float: inline-start;
        grid-area: title;
      }

      .breadcrumbs {
        display: none;
        grid-area: breadcrumbs;

        @media screen and (max-width: $breakpoint-md) {
          display: revert;
        }
      }

      .sortSelection {
        //float: inline-end;
        // display: flex;
        // align-items: baseline;
        grid-area: sort;

        @media screen and (max-width: $breakpoint-sm) {
          display: none;
        }

        >span {
          padding-inline: 1rem;
        }
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
    flex-basis: 15.5rem; //min-width: 15.5rem; //11.875rem;
    padding-inline-end: 2rem;
    text-wrap: nowrap;

    @media screen and (max-width: $breakpoint-md) {
      display: none;
    }
  }

  .breadcrumbs {
    margin-block-end: 2.25rem;
    min-height: 45.6px;
    justify-self: center;

    @media screen and (max-width: $breakpoint-md) {
      margin-block-end: 0;
      min-height: revert;
    }

    @media screen and (max-width: $breakpoint-sm) {
      margin-block-end: 0.5rem;
    }

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
</style>
