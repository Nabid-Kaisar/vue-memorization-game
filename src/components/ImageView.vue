<script setup>
import { imageList } from '@/constants/CONSTANTS'
import question from '@/assets/question.png'
import { ref } from 'vue'

const width = '100'
const height = '100'
const timeout = '2000'
const imagesCollection = ref(
  Array.from(Array(imageList.length).fill(), (_, i) => {
    return { id: i, src: question }
  })
)

const handleImageClick = (e, imgData) => {
  let { src: originalSrc } = e.target
  e.target.src = imageList[imgData.id]

  setTimeout(() => {
    e.target.src = originalSrc
  }, timeout)
}
</script>

<template>
  <section class="image-gallery">
    <div :key="idx" v-for="(imgData, idx) in imagesCollection" class="image-container">
      <img
        @click="(e) => handleImageClick(e, imgData)"
        :id="idx"
        :src="imgData.src"
        :width="width"
        :height="height"
        alt="humanPortrait"
      />
    </div>
  </section>
</template>

<style scoped>
.image-gallery {
  display: flex;
  flex-wrap: wrap;
}

.image-container {
  margin: 0.2rem;
}
</style>
