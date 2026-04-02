<template>
  <section class="relative w-full bg-surface">
    <div class="py-24 md:py-32">
      <div class="max-w-7xl mx-auto px-8 relative">
        <div class="absolute -top-16 left-8 z-0">
          <span class="font-headline text-[8rem] md:text-[12rem] font-extrabold text-primary/5 select-none leading-none">
            Wnętrze
          </span>
        </div>
        
        <div class="relative z-10 text-center mb-16">
          <h2 class="font-headline text-3xl md:text-4xl font-bold tracking-tight text-on-surface">
            Odkryj Swoją Przestrzeń
          </h2>
          <div class="w-20 h-1 bg-[#D44E98] mx-auto mt-4 rounded-full"></div>
        </div>
      </div>
    </div>
    
    <div ref="sectionRef" class="relative w-full" style="height: 300vh;">
      <div class="w-full h-screen sticky top-0">
        <video 
          ref="videoRef"
          class="w-full h-full object-cover" 
          muted 
          playsinline
          preload="auto"
        >
          <source src="/assets/layout/paralax_optimized.mp4" type="video/mp4" />
        </video>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

const videoRef = ref<HTMLVideoElement | null>(null)
const sectionRef = ref<HTMLElement | null>(null)

let rafId = 0
let targetTime = 0

const animate = () => {
  if (sectionRef.value && videoRef.value && videoRef.value.duration) {
    const rect = sectionRef.value.getBoundingClientRect()
    const scrollDistance = rect.height - window.innerHeight
    
    // Calculate progress between 0 and 1
    let progress = -rect.top / scrollDistance
    progress = Math.max(0, Math.min(1, progress))
    
    targetTime = progress * videoRef.value.duration
    
    const diff = targetTime - videoRef.value.currentTime
    // Use lerp for smoother video scrubbing
    if (Math.abs(diff) > 0.01) {
      // Increased lerp factor to 0.3 for a more responsive, snappier feel
      videoRef.value.currentTime += diff * 0.3
    }
  }
  rafId = requestAnimationFrame(animate)
}

onMounted(() => {
  if (videoRef.value) {
    videoRef.value.addEventListener('loadedmetadata', () => {
      videoRef.value!.currentTime = 0
    })
    // Also try to preload the first frame actively
    videoRef.value.load()
  }
  rafId = requestAnimationFrame(animate)
})

onBeforeUnmount(() => {
  cancelAnimationFrame(rafId)
})
</script>
