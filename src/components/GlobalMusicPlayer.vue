<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { useMusicStore } from '@/stores/music'
const aplayerRef = ref<HTMLElement>()
const musicStore = useMusicStore()
let lrcTimer: number | null = null
onMounted(() => {
  if (aplayerRef.value) {
    musicStore.initPlayer(aplayerRef.value)
    lrcTimer = window.setInterval(musicStore.updateLrc, 500)
  }
})
onUnmounted(() => {
  if (lrcTimer) clearInterval(lrcTimer)
  lrcTimer = null
})
</script>
<template>
  <div style="display:none"><div id="aplayer" ref="aplayerRef"></div></div>
</template> 