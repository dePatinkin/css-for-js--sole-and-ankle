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

const onSale = typeof props.salePrice === 'number';
const newRelease = isNewShoe(props.releaseDate);
</script>

<template>
  <a class="shoe-card" :href="`/shoes/${slug}`">
    <article :class="`shoe-${variant}`">
      <div class="image-container">
        <img :src="imageSrc" :alt="name" />
      </div>
      <div class="row">
        <h3>{{ name }}</h3>
        <span :class="'price' + (onSale ? ' on-sale' : '')">{{ formatPrice(price) }}</span>
      </div>
      <div class="row">
        <span class="colors">{{ pluralize("Color", numOfColors) }}</span>
        <span v-if="salePrice" class="sale-price">
          {{ formatPrice(salePrice) }}
        </span>
      </div>
      <div v-if="onSale" class="notice on-sale">
        <span>Sale</span>
      </div>
      <div v-else-if="newRelease" class="notice new-release">
        <span>Just Released!</span>
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
    position: relative;
  }

  img {
    /* scale to container */
    width: 100%; // width: 340px;
    // max-height: 312px;
    border-radius: 16px 16px 4px 4px;
  }

  h3 {
    font-weight: $weight-medium;
  }

  .row {
    display: flex;
  }

  .price,
  .sale-price {
    margin-inline-start: auto;
  }

  .price.on-sale {
    text-decoration: line-through;
    color: $color-gray-700;
  }

  .colors {
    color: $color-gray-700;
  }

  .sale-price {
    color: $color-primary;
    font-weight: $weight-medium;
  }

  .notice {
    position: absolute;
    top: 12px;
    right: -4px;
    border-radius: 2px;
    font-size: 0.875rem;
    font-weight: $weight-xmedium;
    color: $color-white;
    padding: 0.5rem 0.8rem;

    &.on-sale {
      background-color: $color-primary;
    }

    &.new-release {
      background-color: $color-secondary;
    }
  }
}
</style>
