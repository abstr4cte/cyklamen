<template>
  <section ref="sectionRef" class="relative w-full h-[300vh] bg-background">
    <div class="sticky top-0 w-full h-screen overflow-hidden">
      <!-- Muted and playsinline are required for seamless video manipulation and mobile support -->
      <video
        ref="videoRef"
        class="w-full h-full object-cover"
        muted
        playsinline
        preload="auto"
      >
        <source :src="videoPath" type="video/mp4" />
      </video>
      <!-- Płynne przejścia dla tła nad i pod sekcją wideo -->
      <div class="absolute top-0 left-0 w-full h-48 bg-gradient-to-b from-background via-background/80 to-transparent pointer-events-none z-10"></div>
      <div class="absolute bottom-0 left-0 w-full h-48 bg-gradient-to-t from-background via-background/80 to-transparent pointer-events-none z-10"></div>

      <div class="absolute inset-0 bg-black/40 flex items-center justify-center pointer-events-none z-20">
        <div class="relative w-full text-center flex flex-col items-center justify-center">
          <!-- Cienka linia biegnąca przez środek pod spodem -->
          <div class="absolute top-1/2 left-0 w-full h-[1px] bg-primary/40 -translate-y-[20%] shadow-[0_0_15px_rgba(233,179,255,0.7)] mix-blend-screen"></div>
          
          <h2 class="relative z-10 text-3xl sm:text-4xl md:text-6xl lg:text-[5rem] font-headline font-bold text-white tracking-[0.1em] sm:tracking-[0.15em] leading-tight drop-shadow-[0_0_25px_rgba(200,99,251,0.7)] px-4">
            PRZYSZŁOŚĆ JEST CYFROWA
          </h2>
          <!-- Grubsza różowa/czerwona kreska pod tekstem -->
          <div class="w-16 h-1 mt-4 sm:mt-6 bg-tertiary-container rounded-full shadow-[0_0_15px_rgba(255,81,103,0.9)] z-10 relative"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import videoPath from '~/assets/video/video-banner-smooth.mp4'

const sectionRef = ref<HTMLElement | null>(null)
const videoRef = ref<HTMLVideoElement | null>(null)

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
