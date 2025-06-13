<template>
  <div class="marquee-wrapper" ref="wrapper">
    <div
      class="marquee-content"
      :style="contentStyle"
      ref="content"
    >
      <span class="marquee-text" v-for="n in 2" :key="n">{{ name }}</span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const props = defineProps({
  name: {
    type: String,
    default: '这是滚动的名字',
  },
  speed: {
    type: Number,
    default: 80, // px per second
  },
})

const wrapper = ref(null)
const content = ref(null)

const contentWidth = ref(0)
const duration = ref(0)

const contentStyle = computed(() => ({
  animationDuration: `${duration.value}s`,
}))

onMounted(() => {
  // 获取内容宽度
  contentWidth.value = content.value.offsetWidth / 2
  duration.value = contentWidth.value / props.speed
})
</script>

<style scoped>
.marquee-wrapper {
  overflow: hidden;
  white-space: nowrap;
  width: 100%;
  position: relative;
  height: 30px;
}

.marquee-content {
  display: inline-block;
  white-space: nowrap;
  animation: scroll linear infinite;
}

.marquee-text {
  display: inline-block;
  padding-right: 60px; /* 间距决定首尾连接距离 */
  font-weight: bold;
  font-size: 18px;
}

/* 滚动动画 */
@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>
