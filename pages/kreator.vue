<template>
  <div class="bg-gradient-to-br from-surface to-surface-variant/30 min-h-screen overflow-hidden">
    <TheNavigation />
    
    <div class="pt-24 pb-6 h-screen flex flex-col">
      <div class="w-full px-4 md:px-8 flex-1 flex flex-col min-h-0">
        <div class="bg-white/70 backdrop-blur-xl rounded-[2.5rem] shadow-[0_20px_50px_rgba(0,0,0,0.08)] border border-white/40 flex-1 flex flex-col min-h-0 overflow-hidden relative">
          <!-- Background decorative elements -->
          <div class="absolute -top-24 -right-24 w-64 h-64 bg-primary/5 rounded-full blur-3xl pointer-events-none"></div>
          <div class="absolute -bottom-24 -left-24 w-64 h-64 bg-secondary/5 rounded-full blur-3xl pointer-events-none"></div>

          <!-- Wizard Header -->
          <div class="px-8 pt-6 pb-4 border-b border-surface-variant/10 flex items-center justify-between bg-white/30">
            <h1 class="font-headline text-xl md:text-2xl font-bold text-on-surface tracking-tight">
              Konfigurator Domu w <span class="text-primary">Cyklamenach</span>
            </h1>
            <div class="flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-primary animate-pulse"></span>
              <span class="text-[10px] font-label font-bold tracking-widest text-primary uppercase">Tryb Interaktywny</span>
            </div>
          </div>
          
          <div class="flex-1 flex flex-col min-h-0 p-4 md:p-6">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 flex-1 min-h-0">
              <!-- House Stage -->
              <!-- House Stage Container (Scrollable on small screens) -->
              <div class="lg:col-span-9 h-full min-h-0 overflow-x-auto overflow-y-hidden custom-scrollbar">
                <div class="bg-white/50 backdrop-blur-sm rounded-2xl overflow-hidden shadow-inner border border-surface-variant/10 h-full min-h-[500px] min-w-[1000px] xl:min-w-0 relative aspect-[2754/1536]">
                  <!-- Instructional Hint for Horizontal Scroll -->
                  <div class="absolute bottom-4 left-1/2 -translate-x-1/2 z-50 lg:hidden pointer-events-none">
                    <div class="bg-black/60 backdrop-blur-md text-white text-[10px] font-bold tracking-widest px-4 py-2 rounded-full uppercase flex items-center gap-2">
                       <span class="material-symbols-outlined text-sm">swipe_left</span>
                       Przesuń, aby zobaczyć cały dom
                    </div>
                  </div>

                  <div class="px-6 pt-3 pb-2 absolute top-0 left-0 z-20">
                    <div class="text-xs font-label tracking-widest text-secondary uppercase">
                      STAGE: {{ currentScene === 1 ? 'WIDOK ZEWNĘTRZNY' : currentScene === 2 ? 'WYBÓR SEGMENTU' : currentScene === 3 ? 'RZUT KONDYGNACJI' : 'RZUT TECHNICZNY' }}
                    </div>
                  </div>
                  
                  <!-- House Image with Interactive Overlays -->
                  <div class="relative flex items-center justify-center flex-1 overflow-hidden">
                    <!-- Floor Legend - Top Right -->
                    <div v-if="currentScene === 3 && !isVideoPlaying" class="absolute top-6 right-6 bg-white/95 backdrop-blur-md rounded-xl shadow-xl border-2 border-surface-variant/40 p-4 z-20">
                      <div class="space-y-3 text-sm font-label">
                        <div class="flex items-center gap-3">
                          <div class="w-7 h-7 rounded border-2 border-on-surface flex items-center justify-center text-sm font-bold">1</div>
                          <span class="font-bold tracking-wider text-base">PARTER</span>
                        </div>
                        <div class="flex items-center gap-3">
                          <div class="w-7 h-7 rounded border-2 border-primary bg-primary/10 flex items-center justify-center text-sm font-bold text-primary">2</div>
                          <span class="font-bold tracking-wider text-base text-primary">PODDASZE</span>
                        </div>
                        <div class="pt-3 border-t border-surface-variant/40">
                          <button 
                            @click="playTechnicalPlan"
                            class="flex items-center gap-2 text-on-surface hover:text-primary transition-colors"
                          >
                            <span class="material-symbols-outlined text-lg">edit_square</span>
                            <span class="font-bold tracking-wide text-[10px]">ZOBACZ RZUT TECHNICZNY (2D)</span>
                          </button>
                        </div>
                      </div>
                    </div>
                    
                    <!-- Regular image (always present to maintain layout) -->
                    <img
                      :src="backgroundScene === 1 ? '/assets/scenes/scena1.png' : backgroundScene === 2 ? '/assets/scenes/scena2.png' : backgroundScene === 3 ? '/assets/scenes/scena3.png' : '/assets/scenes/scena4.png'"
                      alt="Dom w Cyklamenach"
                      class="max-w-full max-h-full object-contain"
                    />
                    
                    <!-- Video overlay (appears on top when playing) -->
                    <transition name="fade">
                      <video
                        v-if="isVideoPlaying"
                        ref="videoPlayer"
                        class="absolute inset-0 w-full h-full object-contain"
                        @ended="onVideoEnd"
                        @playing="onVideoPlaying"
                        autoplay
                        muted
                      >
                        <source :src="currentVideoSrc" type="video/mp4" />
                      </video>
                    </transition>
                    
                    <!-- Interactive Hotspot for Scene 1 -->
                    <transition name="fade">
                      <div 
                        v-if="currentScene === 1 && !isVideoPlaying && isHotspotVisible"
                        class="absolute left-[48%] top-[65%] z-20"
                      >
                        <div class="relative group">
                          <div class="absolute -inset-4 bg-primary/40 rounded-full animate-ping opacity-75"></div>
                          <div class="absolute -inset-8 bg-primary/20 rounded-full animate-pulse opacity-50"></div>
                          <button 
                            @click="goToScene(2)"
                            @mouseenter="hoveredArea = 1"
                            @mouseleave="hoveredArea = null"
                            class="relative w-10 h-10 bg-primary rounded-full border-4 border-white shadow-xl flex items-center justify-center transition-transform hover:scale-110 active:scale-95"
                          >
                            <span class="material-symbols-outlined text-white text-xl">ads_click</span>
                          </button>

                          <transition name="tooltip-slide">
                            <div v-if="hoveredArea === 1" class="absolute bottom-full left-1/2 -translate-x-1/2 mb-6 w-48 bg-white/95 backdrop-blur-md p-4 rounded-2xl shadow-2xl border border-primary/20 pointer-events-none">
                              <div class="text-[10px] font-bold text-primary tracking-widest uppercase mb-1">INTERAKCJA</div>
                              <div class="text-[13px] font-bold text-on-surface leading-tight">Kliknij, aby poznać wnętrze domu</div>
                              <div class="absolute top-full left-1/2 -translate-x-1/2 w-3 h-3 bg-white rotate-45 border-r border-b border-primary/20 -translate-y-1.5"></div>
                            </div>
                          </transition>
                        </div>
                      </div>
                    </transition>

                    <!-- Interactive Floating Hotspots for Scene 2 -->
                    <div v-if="currentScene === 2 && !isVideoPlaying" class="absolute inset-0 pointer-events-none">
                      <div class="absolute left-[30%] top-[45%] pointer-events-auto group translate-x-[-50%] translate-y-[-50%]" @mouseenter="hoveredArea = 2" @mouseleave="hoveredArea = null">
                        <div @click="playVideoForSegment('left')" class="relative flex flex-col items-center">
                          <div class="bg-white/90 backdrop-blur-xl rounded-full p-1.5 shadow-2xl border border-white/50 transition-all duration-500 ease-out group-hover:rounded-[2rem] group-hover:p-6 group-hover:w-64 cursor-pointer overflow-hidden max-w-[140px] group-hover:max-w-[300px] border-primary/20">
                            <div class="flex items-center gap-2 px-2 py-1">
                              <span class="w-2.5 h-2.5 rounded-full bg-green-500 shadow-[0_0_10px_rgba(34,197,94,0.5)] animate-pulse shrink-0"></span>
                              <span class="text-[10px] font-bold tracking-widest uppercase text-green-700 whitespace-nowrap">Segment Lewy</span>
                            </div>
                            <div class="h-0 opacity-0 group-hover:h-auto group-hover:opacity-100 transition-all duration-500 overflow-hidden">
                              <div class="pt-4 pb-2">
                                 <div class="flex justify-around mb-4">
                                    <div class="text-center">
                                      <div class="text-[10px] text-secondary font-bold uppercase tracking-wider mb-0.5">Powierzchnia</div>
                                      <div class="text-on-surface font-bold">121 m²</div>
                                    </div>
                                    <div class="w-[1px] bg-outline-variant/30"></div>
                                    <div class="text-center">
                                      <div class="text-[10px] text-secondary font-bold uppercase tracking-wider mb-0.5">Działka</div>
                                      <div class="text-on-surface font-bold">310 m²</div>
                                    </div>
                                 </div>
                                 <button class="w-full primary-gradient-bg text-white py-2.5 rounded-xl font-label text-[10px] font-bold tracking-widest uppercase shadow-lg shadow-primary/20 flex items-center justify-center gap-2">
                                    Odkryj wnętrze <span class="material-symbols-outlined text-base">arrow_forward</span>
                                 </button>
                              </div>
                            </div>
                          </div>
                          <div class="w-[2px] h-12 bg-gradient-to-b from-primary/40 to-transparent group-hover:h-8 transition-all duration-500"></div>
                        </div>
                      </div>
                      <div class="absolute left-[70%] top-[45%] pointer-events-auto group translate-x-[-50%] translate-y-[-50%]" @mouseenter="hoveredArea = 3" @mouseleave="hoveredArea = null">
                        <div class="relative flex flex-col items-center">
                          <div class="bg-white/80 backdrop-blur-xl rounded-full p-1.5 shadow-xl border border-white/40 border-orange-500/20">
                            <div class="flex items-center gap-2 px-2 py-1">
                              <span class="w-2.5 h-2.5 rounded-full bg-orange-500 shrink-0"></span>
                              <span class="text-[10px] font-bold tracking-widest uppercase text-orange-700 whitespace-nowrap">S. Prawy - Rezerwacja</span>
                            </div>
                          </div>
                          <div class="w-[2px] h-12 bg-gradient-to-b from-orange-400/40 to-transparent"></div>
                        </div>
                      </div>
                    </div>

                    <!-- Interactive Scene 3 (Floor Plan) -->
                    <div v-if="currentScene === 3 && !isVideoPlaying" class="absolute inset-0">
                      <svg viewBox="0 0 2754 1536" class="absolute inset-0 w-full h-full pointer-events-none">
                        <polygon v-for="room in roomBadges" :key="'poly-'+room.id" :points="room.points" fill="transparent" class="cursor-pointer pointer-events-auto" @mouseenter="hoveredArea = room.id" @mouseleave="hoveredArea = null" @click="selectApartment(room.key)" />
                      </svg>
                      <div class="absolute inset-0 pointer-events-none">
                        <div v-for="room in roomBadges" :key="'badge-'+room.id" 
                             class="absolute transition-all duration-500 ease-out translate-x-[-50%] translate-y-[-50%]" 
                             :style="{ left: room.x, top: room.y }">
                          
                          <!-- Room Hotspot / Badge Container -->
                          <div 
                            class="relative flex items-center justify-center bg-white/90 backdrop-blur-md rounded-full shadow-xl border-2 transition-all duration-500 overflow-hidden" 
                            :class="hoveredArea === room.id ? 'px-4 py-1.5 border-primary max-w-[200px] h-auto rounded-xl -translate-y-2' : 'w-4 h-4 border-surface-variant/40 max-w-[16px] h-4'"
                          >
                            <!-- Pulsating Dot (Visible in idle state) -->
                            <div v-if="hoveredArea !== room.id" class="w-2 h-2 rounded-full bg-primary animate-pulse"></div>

                            <!-- Expanded Content (Visible on hover) -->
                            <div 
                              class="flex flex-col items-center transition-all duration-500 whitespace-nowrap"
                              :class="hoveredArea === room.id ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4 h-0'"
                            >
                               <span class="text-[8px] font-bold tracking-[0.2em] text-primary uppercase mb-0.5">{{ room.name }}</span>
                               <span class="text-[11px] font-extrabold text-on-surface">{{ room.area }}</span>
                            </div>

                            <!-- Active Glow -->
                            <div v-if="hoveredArea === room.id" class="absolute inset-0 bg-primary/5 rounded-xl animate-pulse -z-10 overflow-hidden"></div>
                          </div>
                          
                          <!-- Connector Dot Pulse (Always under the hotspot) -->
                          <div v-if="hoveredArea !== room.id" class="absolute inset-0 w-8 h-8 -translate-x-[25%] -translate-y-[25%] bg-primary/20 rounded-full animate-ping pointer-events-none"></div>
                        </div>
                      </div>
                    </div>

                    <!-- Scene 4 (Technical Plan) -->
                    <transition name="plan-fade">
                      <div v-if="currentScene === 4" class="absolute inset-0 bg-black/40 backdrop-blur-sm flex items-center justify-center z-30" @click="goToScene(3)">
                        <button @click="goToScene(3)" class="absolute top-6 right-6 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 backdrop-blur-md flex items-center justify-center transition-colors z-40">
                          <span class="material-symbols-outlined text-white text-2xl">close</span>
                        </button>
                        <div class="max-w-5xl max-h-[90vh]" @click.stop>
                          <img src="/assets/scenes/rzut.png" alt="Rzut techniczny" class="w-full h-full object-contain" />
                        </div>
                      </div>
                    </transition>
                  </div>
                  
                  <!-- Bottom Pagination -->
                  <div class="px-6 py-2 border-t border-surface-variant/5 bg-surface-container-low/30 mt-auto">
                    <div class="flex items-center justify-center gap-6 text-secondary text-sm">
                      <button @click="goToScene(1)" class="flex flex-col items-center gap-1 group">
                        <span class="w-8 h-1 rounded-full transition-colors" :class="currentScene === 1 ? 'bg-primary' : 'bg-outline-variant/30 group-hover:bg-outline-variant/50'"></span>
                        <span class="text-[9px] font-bold tracking-tighter" :class="currentScene === 1 ? 'text-primary' : 'text-secondary/60'">START</span>
                      </button>
                      <button @click="goToScene(2)" class="flex flex-col items-center gap-1 group">
                        <span class="w-8 h-1 rounded-full transition-colors" :class="currentScene === 2 ? 'bg-primary' : 'bg-outline-variant/30 group-hover:bg-outline-variant/50'"></span>
                        <span class="text-[9px] font-bold tracking-tighter" :class="currentScene === 2 ? 'text-primary' : 'text-secondary/60'">WYBÓR</span>
                      </button>
                      <button @click="goToScene(3)" class="flex flex-col items-center gap-1 group">
                        <span class="w-8 h-1 rounded-full transition-colors" :class="currentScene === 3 ? 'bg-primary' : 'bg-outline-variant/30 group-hover:bg-outline-variant/50'"></span>
                        <span class="text-[9px] font-bold tracking-tighter" :class="currentScene === 3 ? 'text-primary' : 'text-secondary/60'">RZUT</span>
                      </button>
                      <button @click="goToScene(4)" class="flex flex-col items-center gap-1 group">
                        <span class="w-8 h-1 rounded-full transition-colors" :class="currentScene === 4 ? 'bg-primary' : 'bg-outline-variant/30 group-hover:bg-outline-variant/50'"></span>
                        <span class="text-[9px] font-bold tracking-tighter" :class="currentScene === 4 ? 'text-primary' : 'text-secondary/60'">TECHNICZNY</span>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Right Detail Panel -->
              <div class="lg:col-span-3 flex flex-col min-h-0">
                <div class="bg-white rounded-3xl p-8 shadow-sm border border-surface-variant/20 flex-1 flex flex-col min-h-0 overflow-y-auto">
                  <div class="text-[10px] font-label font-bold tracking-[0.2em] text-secondary mb-8 uppercase flex items-center gap-2">
                    <span class="w-4 h-[1px] bg-secondary/30"></span>
                    Szczegóły Wyboru
                  </div>
                  
                  <h2 class="font-headline text-2xl font-extrabold text-on-surface mb-4 leading-tight">
                    <template v-if="currentScene === 1">Twój nowy dom<br/>w Cyklamenach</template>
                    <template v-else-if="selectedRoom">{{ selectedRoom.name }}</template>
                    <template v-else-if="selectedSegment === 'left'">Segment Lewy</template>
                    <template v-else-if="selectedSegment === 'right'">Segment Prawy</template>
                    <template v-else>Rozpocznij Podróż</template>
                  </h2>
                  
                  <p class="text-secondary text-[13px] mb-8 leading-relaxed">
                    <template v-if="currentScene === 1">Kliknij w pulsujący przycisk na budynku, aby przejść do wyboru segmentu i rzutu pomieszczeń.</template>
                    <template v-else-if="selectedRoom">Przestronne i funkcjonalne pomieszczenie o powierzchni {{ selectedRoom.area }}. Idealnie doświetlone i gotowe do własnej aranżacji zgodnie z Twoimi potrzebami.</template>
                    <template v-else-if="selectedSegment">Znakomicie zaprojektowany segment o powierzchni 121 m² z przestronnym ogrodem. Idealny dla rodziny szukającej komfortu.</template>
                    <template v-else>Wciśnij ikonę interakcji na grafice, aby odkryć szczegóły kondygnacji i poszczególnych pokoi.</template>
                  </p>
                  
                  <!-- Dynamic Room Features -->
                  <div v-if="selectedRoom" class="space-y-6 mb-8 animate-fade-in">
                    <div class="bg-primary/5 rounded-2xl p-6 border border-primary/10">
                       <div class="text-[11px] font-bold text-primary tracking-widest uppercase mb-4">Charakterystyka</div>
                       <ul class="space-y-3">
                         <li v-for="feat in selectedRoom.features" :key="feat" class="flex items-center gap-3 text-[13px] text-on-surface/80">
                           <span class="w-1.5 h-1.5 rounded-full bg-primary/40"></span>
                           {{ feat }}
                         </li>
                       </ul>
                    </div>
                  </div>

                  <!-- CTAs -->
                  <div class="mt-auto pt-6 space-y-4">
                    <button class="w-full primary-gradient-bg text-on-primary py-4 px-6 rounded-2xl font-label text-xs font-bold tracking-widest uppercase shadow-xl shadow-primary/20 hover:scale-[1.02] transition-transform">
                      KONTAKT Z AGENTEM
                    </button>
                    <button @click="playTechnicalPlan" class="w-full flex items-center justify-center gap-3 bg-on-surface text-white py-4 px-6 rounded-2xl font-label text-xs font-bold tracking-widest uppercase hover:bg-on-surface/90 transition-colors">
                      <span class="material-symbols-outlined text-xl">photo_camera</span>
                      WIDOK 3D / RZUT PDF
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch, computed } from 'vue'

const currentScene = ref<1 | 2 | 3 | 4>(1)
const backgroundScene = ref<1 | 2 | 3 | 4>(1)
const hoveredArea = ref<number | null>(null)
const selectedSegment = ref<'left' | 'right' | null>(null)
const selectedRoomId = ref<string | null>(null)
const activeView = ref<'plot' | 'ground' | 'first'>('ground')
const isVideoPlaying = ref(false)
const videoPlayer = ref<HTMLVideoElement | null>(null)
const currentVideoSrc = ref('/assets/scenes/film1.mp4')
const targetSceneAfterVideo = ref<1 | 2 | 3 | 4>(1)
const isHotspotVisible = ref(false)

const roomBadges = [
  { id: 4, name: 'Łazienka', area: '8.5 m²', x: '21%', y: '52%', key: 'bathroom', points: '859,626 865,893 560,893 558,630', features: ['Wanna i prysznic', 'Ogrzewanie podłogowe', 'Wykończenie premium'] },
  { id: 5, name: 'Schody', area: '4.5 m²', x: '23%', y: '73%', key: 'stairs', points: '948,1240 561,1240 563,910 857,910 946,988', features: ['Wygodny bieg', 'Miejsce na schowek', 'Oświetlenie LED'] },
  { id: 6, name: 'Garderoba', area: '4.8 m²', x: '47%', y: '73%', key: 'wardrobe', points: '1395,995 1253,993 1257,1244 1401,1244', features: ['Systemy półkowe', 'Wentylacja', 'Duże lustro'] },
  { id: 7, name: 'Pokój 1', area: '5.2 m²', x: '23%', y: '32%', key: 'room1', points: '994,321 996,614 560,615 565,327', features: ['Duże okno', 'Cicha okolica', 'Internet światłowodowy'] },
  { id: 8, name: 'Pokój 3', area: '3.5 m²', x: '38%', y: '73%', key: 'room3', points: '1235,991 1235,1242 965,1244 966,995', features: ['Pokój dziecięcy', 'Jasne barwy', 'Gniazdka USB'] },
  { id: 9, name: 'Sypialnia', area: '10.5 m²', x: '45%', y: '35%', key: 'bedroom', points: '1419,294 1010,294 1010,610 1037,612 1126,741 1410,741', features: ['Wyjście na balkon', 'Klimatyzacja', 'Strop akustyczny'] },
  { id: 10, name: 'Przedpokój', area: '6.8 m²', x: '33%', y: '58%', key: 'hallway', points: '1166,759 1170,975 963,977 879,904 879,630 1035,632 1119,763', features: ['Domofon', 'Wnęka na szafę', 'Gres polerowany'] },
  { id: 11, name: 'Schody 2', area: '3.2 m²', x: '48%', y: '58%', key: 'stairs2', points: '1397,757 1401,966 1174,964 1170,757', features: ['Komunikacja pionowa', 'Wykończenie dębowe'] },
  { id: 12, name: 'Balkon', area: '2.3 m²', x: '41%', y: '12%', key: 'balcony', points: '1415,149 1417,241 983,243 983,149', features: ['Szklana balustrada', 'Widok na ogród'] },
]

const selectedRoom = computed(() => roomBadges.find(r => r.key === selectedRoomId.value))

onMounted(() => {
  ['scena1.png', 'scena2.png', 'scena3.png', 'scena4.png'].forEach(img => {
    const i = new Image()
    i.src = `/assets/scenes/${img}`
  })
  setTimeout(() => isHotspotVisible.value = true, 1500)
})

watch(currentScene, (newVal) => {
  if (newVal === 1) {
    isHotspotVisible.value = false
    setTimeout(() => { if (currentScene.value === 1) isHotspotVisible.value = true }, 1500)
  }
})

const goToScene = (sceneNumber: 1 | 2 | 3 | 4) => {
  if (sceneNumber === 2 && currentScene.value === 1) {
    targetSceneAfterVideo.value = 2
    currentVideoSrc.value = '/assets/scenes/film1.mp4'
    isVideoPlaying.value = true
  } else {
    currentScene.value = sceneNumber
    backgroundScene.value = sceneNumber
  }
}

const playVideoForSegment = (segment: 'left' | 'right') => {
  if (segment === 'left') {
    targetSceneAfterVideo.value = 3
    currentVideoSrc.value = '/assets/scenes/film2.mp4'
    isVideoPlaying.value = true
  }
}

const playTechnicalPlan = () => {
    targetSceneAfterVideo.value = 4
    currentVideoSrc.value = '/assets/scenes/film3.mp4'
    isVideoPlaying.value = true
}

const onVideoPlaying = () => {
  backgroundScene.value = targetSceneAfterVideo.value
}

const onVideoEnd = () => {
  currentScene.value = targetSceneAfterVideo.value
  isVideoPlaying.value = false
}

const selectApartment = (roomKey: string) => {
  selectedRoomId.value = roomKey
}

const selectSegment = (segment: 'left' | 'right') => {
  selectedSegment.value = segment
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active { transition: opacity 0.3s ease; transform: translateZ(0); }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.plan-fade-enter-active { transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1); }
.plan-fade-leave-active { transition: all 0.4s ease; }
.plan-fade-enter-from { opacity: 0; transform: scale(0.8); }
.plan-fade-leave-to { opacity: 0; transform: scale(0.95); }

.tooltip-slide-enter-active, .tooltip-slide-leave-active { transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1); }
.tooltip-slide-enter-from { opacity: 0; transform: translate(-50%, 10px) scale(0.9); }
.tooltip-slide-leave-to { opacity: 0; transform: translate(-50%, 5px) scale(0.95); }

@keyframes ping {
  0% { transform: scale(1); opacity: 0.75; }
  75%, 100% { transform: scale(2.5); opacity: 0; }
}

.animate-pulse { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
@keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: .5; } }

.animate-fade-in { animation: fadeIn 0.5s ease-out forwards; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
</style>
