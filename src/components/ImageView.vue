<script setup>
import { imageList } from '@/constants/CONSTANTS'
import question from '@/assets/question.png'
import { computed, ref, onMounted } from 'vue'
import { shuffleArray } from '@/util/Util'

const width = '100'
const height = '100'
const timeout = '2000'

let randomizedData = ref([])
let currentShowingCount = 0

onMounted(() => {
  let imagesLength = imageList.length

  for (let i = 0; i < imagesLength; i++) {
    randomizedData.value.push({ id: i, src: question })
    randomizedData.value.push({ id: i, src: question })
  }

  shuffleArray(randomizedData.value)
})

const handleImageClick = (e, imgData) => {
  if (currentShowingCount >= 2) return
  let { src: originalSrc } = e.target
  e.target.src = imageList[imgData.id]

  console.log('currentShowingCount :: ', currentShowingCount)
  currentShowingCount++
  console.log('currentShowingCount after:: ', currentShowingCount)

  setTimeout(() => {
    e.target.src = originalSrc
    currentShowingCount--
  }, timeout)
}
</script>

<template>
  <section class="image-gallery">
    <div :key="idx" v-for="(imageData, idx) in randomizedData" class="image-container">
      <img
        @click="(e) => handleImageClick(e, imageData)"
        :id="idx"
        :src="imageData.src"
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
