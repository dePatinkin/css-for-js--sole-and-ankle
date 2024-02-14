<script setup>
import { shallowRef, watch } from "vue";

const links = [
  { text: "All", path: "" },
  { text: "Lifestyle", path: "#lifestyle" },
  { text: "Jordan", path: "#jordan" },
  { text: "Running", path: "#running" },
  { text: "Basketball", path: "#basketball" },
  { text: "Training & Gym", path: "#training" },
  { text: "Football", path: "#football" },
  { text: "Skateboarding", path: "#skateboarding" },
  { text: "American Football", path: "#us-football" },
  { text: "Baseball", path: "#baseball" },
  { text: "Golf", path: "#golf" },
  { text: "Tennis", path: "#tennis" },
  { text: "Athletics", path: "#athletics" },
  { text: "Walking", path: "#walking" },
];

const currentPath = shallowRef(window.location.hash);
window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const emit = defineEmits(["currentChanged"]);
watch(currentPath, () => {
  emit(
    "currentChanged",
    links.find((i) => i.path === currentPath.value) || links[0],
  );
});
</script>

<template>
  <section class="filters">
    <!-- <p>currentPath: {{ currentPath }}</p> -->
    <a v-for="{ text, path } in links" :key="path" :href="path" :class="path === currentPath ? 'current' : ''">{{ text
    }}</a>
  </section>
</template>

<style scoped lang="scss">
@import "../settings/variables";

.filters {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  line-height: 2rem;
  font-weight: $weight-medium;

  a {
    line-height: inherit;
  }

  a.current {
    color: $color-primary;
  }
}
</style>
