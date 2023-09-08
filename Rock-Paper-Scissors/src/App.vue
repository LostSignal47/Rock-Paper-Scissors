<script setup>
import { ref } from 'vue'

// กำหนดรูปภาพเริ่มต้น
const imgUrl = ref(new URL('./assets/r-p-g.png', import.meta.url).href)

const rd = Math.floor(Math.random() * 3) + 1

// เปลี่ยนรูปภาพเป็น ค้อน
imgUrl.value = new URL('./assets/r.png', import.meta.url).href

</script>

<template>
  <img :src="imgUrl" />

</template>

