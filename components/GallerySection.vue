<template>
  <section class="relative w-full bg-surface">
    <div class="pt-24 md:pt-32">
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
        
        <!-- Animated Text Labels -->
        <div class="absolute inset-0 pointer-events-none">
          <!-- Label 1: SALON Z KOMINKIEM -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 1"
              class="absolute top-[20%] left-[25%]"
            >
              <div class="relative primary-gradient-bg text-white px-8 py-4 rounded-xl shadow-2xl">
                <!-- Multi-segment dotted line: right then down -->
                <svg class="absolute left-full top-1/2 -translate-y-1/2" width="80" height="60">
                  <circle cx="2" cy="30" r="2" fill="white" opacity="0.6"/>
                  <line x1="4" y1="30" x2="50" y2="30" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <line x1="50" y1="30" x2="50" y2="50" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <circle cx="50" cy="50" r="3" fill="white" opacity="0.8"/>
                </svg>
                <span class="font-bold text-base md:text-lg uppercase tracking-[0.3em]">Salon z Kominkiem</span>
              </div>
            </div>
          </transition>
          
          <!-- Label 2: STREFA RELAKSU -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 2"
              class="absolute top-[25%] right-[20%]"
            >
              <div class="relative primary-gradient-bg text-white px-8 py-4 rounded-xl shadow-2xl">
                <!-- Multi-segment dotted line: left then up -->
                <svg class="absolute right-full top-1/2 -translate-y-1/2" width="90" height="70">
                  <circle cx="88" cy="35" r="2" fill="white" opacity="0.6"/>
                  <line x1="86" y1="35" x2="40" y2="35" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <line x1="40" y1="35" x2="40" y2="10" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <circle cx="40" cy="10" r="3" fill="white" opacity="0.8"/>
                </svg>
                <span class="font-bold text-base md:text-lg uppercase tracking-[0.3em]">Strefa Relaksu</span>
              </div>
            </div>
          </transition>
          
          <!-- Label 3: PRZESTRZEŃ DLA RODZINY -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 3"
              class="absolute top-[35%] left-[30%]"
            >
              <div class="relative primary-gradient-bg text-white px-8 py-4 rounded-xl shadow-2xl">
                <!-- Multi-segment dotted line: right then up -->
                <svg class="absolute left-full top-1/2 -translate-y-1/2" width="75" height="65">
                  <circle cx="2" cy="32" r="2" fill="white" opacity="0.6"/>
                  <line x1="4" y1="32" x2="45" y2="32" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <line x1="45" y1="32" x2="45" y2="5" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <circle cx="45" cy="5" r="3" fill="white" opacity="0.8"/>
                </svg>
                <span class="font-bold text-base md:text-lg uppercase tracking-[0.3em]">Przestrzeń dla Rodziny</span>
              </div>
            </div>
          </transition>
          
          <!-- Label 4: WIDOK NA OGRÓD -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 4"
              class="absolute bottom-[40%] right-[25%]"
            >
              <div class="relative primary-gradient-bg text-white px-8 py-4 rounded-xl shadow-2xl">
                <!-- Multi-segment dotted line: down then right -->
                <svg class="absolute top-full left-1/2 -translate-x-1/2" width="70" height="60">
                  <circle cx="35" cy="2" r="2" fill="white" opacity="0.6"/>
                  <line x1="35" y1="4" x2="35" y2="30" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <line x1="35" y1="30" x2="60" y2="30" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <circle cx="60" cy="30" r="3" fill="white" opacity="0.8"/>
                </svg>
                <span class="font-bold text-base md:text-lg uppercase tracking-[0.3em]">Widok na Ogród</span>
              </div>
            </div>
          </transition>
          
          <!-- Label 5: KOMFORTOWE WNĘTRZE -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 5"
              class="absolute top-[45%] left-[18%]"
            >
              <div class="relative primary-gradient-bg text-white px-8 py-4 rounded-xl shadow-2xl">
                <!-- Multi-segment dotted line: left then down -->
                <svg class="absolute right-full top-1/2 -translate-y-1/2" width="80" height="70">
                  <circle cx="78" cy="35" r="2" fill="white" opacity="0.6"/>
                  <line x1="76" y1="35" x2="30" y2="35" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <line x1="30" y1="35" x2="30" y2="60" stroke="white" stroke-width="2" stroke-dasharray="4,4" opacity="0.6"/>
                  <circle cx="30" cy="60" r="3" fill="white" opacity="0.8"/>
                </svg>
                <span class="font-bold text-base md:text-lg uppercase tracking-[0.3em]">Komfortowe Wnętrze</span>
              </div>
            </div>
          </transition>
          
          <!-- Button at end: ROZPOCZNIJ -->
          <transition name="label-fade">
            <div 
              v-if="currentLabel === 6"
              class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 pointer-events-auto"
            >
              <a 
                href="/kreator"
                class="primary-gradient-bg text-white py-6 px-12 rounded-2xl font-label text-lg font-bold tracking-[0.3em] uppercase shadow-2xl shadow-primary/50 hover:scale-110 hover:shadow-3xl transition-all inline-flex items-center gap-3"
              >
                <span>Rozpocznij interaktywną podróż</span>
                <span class="material-symbols-outlined text-2xl">arrow_forward</span>
              </a>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

const videoRef = ref<HTMLVideoElement | null>(null)
const sectionRef = ref<HTMLElement | null>(null)
const currentLabel = ref<number | null>(null)

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
    
    // Update label based on scroll progress
    if (progress < 0.15) {
      currentLabel.value = null // No label at start
    } else if (progress < 0.3) {
      currentLabel.value = 1 // SALON Z KOMINKIEM
    } else if (progress < 0.45) {
      currentLabel.value = 2 // STREFA RELAKSU
    } else if (progress < 0.6) {
      currentLabel.value = 3 // PRZESTRZEŃ DLA RODZINY
    } else if (progress < 0.75) {
      currentLabel.value = 4 // WIDOK NA OGRÓD
    } else if (progress < 0.9) {
      currentLabel.value = 5 // KOMFORTOWE WNĘTRZE
    } else {
      currentLabel.value = 6 // Button at end
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

<style scoped>
.label-fade-enter-active,
.label-fade-leave-active {
  transition: all 0.5s ease;
}

.label-fade-enter-from {
  opacity: 0;
  transform: scale(0.9) translateY(10px);
}

.label-fade-leave-to {
  opacity: 0;
  transform: scale(0.9) translateY(-10px);
}
</style>
