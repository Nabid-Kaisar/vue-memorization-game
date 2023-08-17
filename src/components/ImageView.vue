<script setup>
import { imageList } from '@/constants/CONSTANTS'

const width = '100'
const height = '100'
</script>

<template id="app">
  <div>
    <img
      v-for="(img, idx) in imageList"
      :src="img"
      :key="idx"
      :width="width"
      :height="height"
      alt="humanPortrait"
    />
  </div>
</template>
