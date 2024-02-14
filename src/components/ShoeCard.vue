<script setup>
import { formatPrice, pluralize, isNewShoe } from "../settings/utils";

const props = defineProps({
  slug: String,
  name: String,
  imageSrc: String,
  price: Number,
  salePrice: Number,
  releaseDate: Date,
  numOfColors: Number,
});
</script>

<template>
  <a class="shoe-card" :href="`/shoes/${slug}`">
    <article :class="`shoe-${variant}`">
      <div class="image-container">
        <img :src="imageSrc" :alt="name" />
      </div>
      <div class="infos-container">
        <h3>{{ name }}</h3>
        <span class="price">{{ formatPrice(price) }}</span>
        <span class="color">{{ pluralize("Color", numOfColors) }}</span>
        <span v-if="salePrice" class="sale-price">
          {{ formatPrice(salePrice) }}
        </span>
      </div>
      <div class="notice">
        <div v-if="typeof salePrice === 'number'" class="on-sale">
          <span>Sale</span>
        </div>
        <div v-else-if="isNewShoe(releaseDate)" class="new-release">
          <span>Just Released!</span>
        </div>
      </div>
    </article>
  </a>
</template>

<style scoped lang="scss">
@import "../settings/variables";

.shoe-card {
  article {
    display: flex;
    flex-direction: column;
  }

  img {
    width: 100%; // width: 340px;
    // max-height: 312px;
    border-radius: 16px 16px 4px 4px;
  }
}
</style>
