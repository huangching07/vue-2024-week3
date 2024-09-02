<script setup>
import { defineProps, defineEmits } from 'vue'
defineProps(['data'])
const emits = defineEmits(['addToCart'])
</script>
<template>
  <div class="list-group">
    <a
      href="#"
      class="list-group-item list-group-item-action"
      v-for="item in data"
      :key="item.id"
      @click="emits('addToCart', item.id)"
    >
      <div class="d-flex w-100 justify-content-between">
        <h5 class="mb-1">{{ item.name }}</h5>
        <small>${{ item.price }}</small>
      </div>
      <p class="mb-1">{{ item.description }}</p>
    </a>
  </div>
</template>
<style scoped></style>
