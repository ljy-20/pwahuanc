<script setup>
import { ref } from 'vue'

const imageUrl = ref('https://picsum.photos/id/1/200/300')

const refreshImage = () => {
  const randomId = Math.floor(Math.random() * 1000)
  imageUrl.value = `https://picsum.photos/id/${randomId}/200/300`
}
</script>

<template>
  <div>
    <h1>PWA 图片缓存示例</h1>
    <img :src="imageUrl" alt="Random Image" style="width: 200px; height: 300px;" />
    <p>
      <button @click="refreshImage">刷新图片</button>
    </p>
    <p>请尝试刷新页面或离线访问，观察图片是否被缓存。</p>
  </div>
</template>

<style scoped>
img {
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
