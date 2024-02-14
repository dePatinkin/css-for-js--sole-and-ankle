<script setup>
import SuperHeader from "./components/SuperHeader.vue";
import MainNav from "./components/MainNav.vue";
import ShoeIndex from "./components/ShoeIndex.vue";
</script>

<template>
  <SuperHeader />
  <MainNav />
  <ShoeIndex />
</template>

//
<style scoped lang="scss">
@import "./settings/variables";

// #app {
//   z-index: 0;
// }

::v-deep(a, p, span, h1, h2, h3, h4, h5, h6) {
  color: $color-gray-900;
}

::v-deep(a) {
  text-decoration: none;
}

::v-deep(.graphics-wrapper) {
  line-height: 0;
}
</style>
