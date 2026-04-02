<template>
  <div class="bg-surface min-h-screen">
    <TheNavigation />
    
    <div class="pt-20 pb-4">
      <div class="container mx-auto px-4 h-[calc(100vh-6rem)]">
        <!-- Page Title -->
        <h1 class="font-headline text-xl md:text-2xl font-extrabold text-on-surface mb-3">
          Wybierz swój dom w Cyklamenach
        </h1>
        
        <div class="grid grid-cols-1 gap-3 h-[calc(100%-3.5rem)]">
          <!-- House Stage - Full Width -->
          <div class="w-full h-full">
            <div class="bg-white rounded-2xl overflow-hidden shadow-sm border border-surface-variant/20 h-full flex flex-col">
              <div class="px-6 pt-3 pb-2">
                <div class="text-xs font-label tracking-widest text-secondary uppercase">
                  STAGE
                </div>
              </div>
              
              <!-- House Image with Interactive SVG -->
              <div class="relative flex items-center justify-center flex-1 overflow-hidden">
                <img 
                  :src="currentScene === 1 ? '/assets/scenes/scena1.png' : '/assets/scenes/scena2.png'"
                  alt="Dom w Cyklamenach"
                  class="max-w-full max-h-full object-contain"
                />
                
                <!-- SVG Overlay for Scene 1 -->
                <svg 
                  v-if="currentScene === 1"
                  viewBox="0 0 2752 1536"
                  class="absolute top-0 left-0 w-full h-full"
                  style="pointer-events: none;"
                >
                  <polygon
                    id="polygon-1"
                    points="585,813 593,1196 1070,1396 1345,1325 1497,1370 1678,1316 1677,1300 2023,1207 2047,1213 2153,1186 2153,1175 2153,1175 2140,1171 2141,1077 2149,1082 2149,1082 2152,1079 2130,1064 2133,844 2133,833 2147,832 2115,807 2100,795 2256,790 2030,612 2030,612 2032,606 2032,606 2035,607 2037,595 1940,463 1849,473 1591,439 1592,398 1594,399 1594,399 1595,390 1576,388 1575,380 1575,380 1572,375 1567,373 1560,374 1559,379 1558,386 1558,389 1531,394 1531,399 1522,399 1523,380 1509,377 1509,377 1508,366 1494,365 1492,371 1492,375 1490,378 1449,383 1450,412 688,322 472,798 480,802 482,817"
                    :fill="hoveredArea === 1 ? '#D44E98' : '#c9a84c'"
                    :fill-opacity="hoveredArea === 1 ? '0.3' : '0.15'"
                    stroke="#c9a84c"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 1"
                    @mouseleave="hoveredArea = null"
                    @click="goToScene(2)"
                  />
                </svg>
                
                <!-- Info Tooltip for Scene 1 -->
                <div v-if="currentScene === 1">
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 1"
                      class="absolute left-1/2 top-[35%] -translate-x-1/2 bg-white/70 backdrop-blur-md p-5 rounded-xl shadow-xl border-2 border-primary z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-xl font-bold text-on-surface mb-2 text-center uppercase">
                        Dom w Cyklamenach
                      </h3>
                      <p class="text-center text-secondary text-sm max-w-xs">
                        Kliknij, aby poznać dostępne segmenty
                      </p>
                    </div>
                  </transition>
                </div>
                
                <!-- SVG Overlay for Scene 2 -->
                <svg 
                  v-if="currentScene === 2"
                  viewBox="0 0 2752 1536"
                  class="absolute top-0 left-0 w-full h-full"
                  style="pointer-events: none;"
                >
                  <polygon
                    id="polygon-left"
                    points="1395,1213 1394,393 1367,393 1366,364 1330,365 1330,365 1330,392 747,394 577,767 577,767 575,782 583,782 581,794 694,795 702,1177 864,1184 864,1184 889,1192 889,1192 887,1203 902,1204 898,1208 898,1222 1111,1219 1117,1210"
                    :fill="hoveredArea === 2 ? '#D44E98' : '#c9a84c'"
                    :fill-opacity="hoveredArea === 2 ? '0.3' : '0.15'"
                    stroke="#c9a84c"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 2"
                    @mouseleave="hoveredArea = null"
                    @click="selectSegment('left')"
                  />
                  
                  <polygon
                    id="polygon-right"
                    points="1397,1212 1395,393 1417,393 1417,364 1453,364 1453,393 2034,391 2210,760 2210,776 2202,782 2196,792 2095,793 2091,1175 1877,1174 1877,1193 1889,1206 1890,1218 1679,1218 1672,1209 1475,1209"
                    :fill="hoveredArea === 3 ? '#ff0000' : '#ff0000'"
                    :fill-opacity="hoveredArea === 3 ? '0.4' : '0.2'"
                    stroke="#ff0000"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-not-allowed transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 3"
                    @mouseleave="hoveredArea = null"
                  />
                </svg>
                
                <!-- Info Tooltips for Scene 2 -->
                <div v-if="currentScene === 2">
                  <!-- Left Segment Tooltip -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 2"
                      class="absolute left-[15%] top-[30%] bg-white/70 backdrop-blur-md p-4 rounded-xl shadow-xl border-2 border-primary z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-lg font-bold text-on-surface mb-3 uppercase">
                        Segment Lewy
                      </h3>
                      <div class="space-y-1.5 text-sm font-body">
                        <div class="flex gap-2">
                          <span class="text-on-surface font-semibold">POWIERZCHNIA:</span>
                          <span class="text-on-surface">121 m²</span>
                        </div>
                        <div class="flex gap-2">
                          <span class="text-on-surface font-semibold">DZIAŁKA:</span>
                          <span class="text-on-surface">310 m²</span>
                        </div>
                        <div class="flex gap-2 items-center">
                          <span class="text-on-surface font-semibold">STATUS:</span>
                          <span class="text-green-600 font-bold">WOLNY</span>
                        </div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Right Segment Tooltip -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 3"
                      class="absolute right-[15%] top-[30%] bg-white/70 backdrop-blur-md p-4 rounded-xl shadow-xl border-2 border-red-500 z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-lg font-bold text-on-surface mb-3 uppercase">
                        Segment Prawy
                      </h3>
                      <div class="space-y-1.5 text-sm font-body">
                        <div class="flex gap-2">
                          <span class="text-on-surface font-semibold">POWIERZCHNIA:</span>
                          <span class="text-on-surface">121 m²</span>
                        </div>
                        <div class="flex gap-2">
                          <span class="text-on-surface font-semibold">DZIAŁKA:</span>
                          <span class="text-on-surface">305 m²</span>
                        </div>
                        <div class="flex gap-2 items-center">
                          <span class="text-on-surface font-semibold">STATUS:</span>
                          <span class="text-red-600 font-bold">REZERWACJA</span>
                        </div>
                      </div>
                    </div>
                  </transition>
                </div>
              </div>
              
              <!-- Bottom Controls -->
              <div class="px-6 py-3">
                <div class="flex items-center justify-center gap-3 text-secondary">
                  <button 
                    @click="goToScene(1)" 
                    class="p-1.5 hover:bg-surface-container-low rounded-lg transition-colors"
                    :class="{ 'bg-surface-container-low': currentScene === 1 }"
                  >
                    <span class="material-symbols-outlined text-xl">filter_1</span>
                  </button>
                  <div class="flex items-center gap-2">
                    <button 
                      @click="goToScene(1)"
                      class="w-6 h-0.5 rounded-full transition-colors"
                      :class="currentScene === 1 ? 'bg-primary' : 'bg-outline-variant/30'"
                    ></button>
                    <button 
                      @click="goToScene(2)"
                      class="w-6 h-0.5 rounded-full transition-colors"
                      :class="currentScene === 2 ? 'bg-primary' : 'bg-outline-variant/30'"
                    ></button>
                  </div>
                  <button 
                    @click="goToScene(2)" 
                    class="p-1.5 hover:bg-surface-container-low rounded-lg transition-colors"
                    :class="{ 'bg-surface-container-low': currentScene === 2 }"
                  >
                    <span class="material-symbols-outlined text-xl">filter_2</span>
                  </button>
                </div>
                
                <!-- PDF Download Section -->
                <div class="mt-3 text-center">
                  <button class="primary-gradient-bg text-on-primary py-2.5 px-6 rounded-lg font-label text-xs font-bold tracking-[0.2em] uppercase shadow-md shadow-primary/30 hover:scale-105 transition-transform">
                    ZAREZERWUJ TERMIN PREZENTACJI
                  </button>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Right Side - Dynamic Detail Panel -->
          <div class="hidden lg:col-span-4">
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-surface-variant/20 sticky top-24">
              <div class="text-xs font-label tracking-widest text-secondary mb-6 uppercase">
                DYNAMIC DETAIL PANEL
              </div>
              
              <h2 class="font-headline text-2xl font-extrabold text-on-surface mb-2">
                <template v-if="currentScene === 1">
                  Twój nowy dom<br/>w Cyklamenach
                </template>
                <template v-else-if="selectedSegment === 'left'">
                  Segment Lewy
                </template>
                <template v-else-if="selectedSegment === 'right'">
                  Segment Prawy
                </template>
                <template v-else>
                  Wybierz segment
                </template>
              </h2>
              <p class="text-secondary text-sm mb-6 leading-relaxed">
                <template v-if="currentScene === 1">
                  Kliknij w zaznaczony obszar, aby poznać rozkład pomieszczeń, szczegółowe wymiary i wizualizacje.
                </template>
                <template v-else-if="selectedSegment">
                  <span class="block mb-2"><strong>Powierzchnia:</strong> 121 m²</span>
                  <span class="block mb-2"><strong>Działka:</strong> {{ selectedSegment === 'left' ? '310 m²' : '305 m²' }}</span>
                  <span class="block"><strong>Status:</strong> <span :class="selectedSegment === 'left' ? 'text-green-600' : 'text-orange-600'">{{ selectedSegment === 'left' ? 'WOLNY' : 'REZERWACJA' }}</span></span>
                </template>
                <template v-else>
                  Kliknij w lewy lub prawy segment, aby zobaczyć szczegóły.
                </template>
              </p>
              
              <!-- Floor Plan Toggle -->
              <div class="space-y-3 mb-6">
                <button 
                  class="w-full flex items-center gap-3 p-3 rounded-lg transition-colors"
                  :class="activeView === 'plot' ? 'bg-primary/10 border-2 border-primary' : 'bg-surface-container-low border-2 border-transparent hover:border-outline-variant/30'"
                  @click="activeView = 'plot'"
                >
                  <div class="w-6 h-6 rounded-full border-2 flex items-center justify-center"
                       :class="activeView === 'plot' ? 'border-primary' : 'border-outline-variant'">
                    <div v-if="activeView === 'plot'" class="w-3 h-3 rounded-full bg-primary"></div>
                  </div>
                  <span class="font-label text-sm font-semibold tracking-wider" :class="activeView === 'plot' ? 'text-primary' : 'text-secondary'">
                    RZUT DZIAŁKI
                  </span>
                </button>
                
                <button 
                  class="w-full flex items-center gap-3 p-3 rounded-lg transition-colors"
                  :class="activeView === 'ground' ? 'bg-primary/10 border-2 border-primary' : 'bg-surface-container-low border-2 border-transparent hover:border-outline-variant/30'"
                  @click="activeView = 'ground'"
                >
                  <div class="w-6 h-6 rounded-full border-2 flex items-center justify-center"
                       :class="activeView === 'ground' ? 'border-primary' : 'border-outline-variant'">
                    <div v-if="activeView === 'ground'" class="w-3 h-3 rounded-full bg-primary"></div>
                  </div>
                  <span class="font-label text-sm font-semibold tracking-wider" :class="activeView === 'ground' ? 'text-primary' : 'text-secondary'">
                    PARTER
                  </span>
                </button>
                
                <button 
                  class="w-full flex items-center gap-3 p-3 rounded-lg transition-colors"
                  :class="activeView === 'first' ? 'bg-primary/10 border-2 border-primary' : 'bg-surface-container-low border-2 border-transparent hover:border-outline-variant/30'"
                  @click="activeView = 'first'"
                >
                  <div class="w-6 h-6 rounded-full border-2 flex items-center justify-center"
                       :class="activeView === 'first' ? 'border-primary' : 'border-outline-variant'">
                    <div v-if="activeView === 'first'" class="w-3 h-3 rounded-full bg-primary"></div>
                  </div>
                  <span class="font-label text-sm font-semibold tracking-wider" :class="activeView === 'first' ? 'text-primary' : 'text-secondary'">
                    PIĘTRO
                  </span>
                </button>
              </div>
              
              <!-- Floor Plans Grid -->
              <div class="grid grid-cols-2 gap-3 mb-6">
                <div class="bg-surface-container-low rounded-lg p-3 text-center">
                  <div class="aspect-square bg-pink-100 rounded-lg mb-2 flex items-center justify-center">
                    <span class="text-4xl text-primary/30 material-symbols-outlined">home</span>
                  </div>
                  <p class="text-xs font-label font-bold tracking-wider text-on-surface">PARTER</p>
                </div>
                <div class="bg-surface-container-low rounded-lg p-3 text-center">
                  <div class="aspect-square bg-pink-100 rounded-lg mb-2 flex items-center justify-center">
                    <span class="text-4xl text-primary/30 material-symbols-outlined">stairs</span>
                  </div>
                  <p class="text-xs font-label font-bold tracking-wider text-on-surface">PIĘTRO</p>
                </div>
              </div>
              
              <!-- Large Floor Plan -->
              <div class="bg-pink-50 rounded-xl p-6 mb-6 aspect-square flex items-center justify-center border-2 border-primary/20">
                <div class="text-center">
                  <span class="text-6xl text-primary/20 material-symbols-outlined mb-4 block">home_work</span>
                  <p class="text-sm font-label tracking-wider text-secondary uppercase">SVG</p>
                </div>
              </div>
              
              <!-- Room Details -->
              <div class="bg-surface-container-low rounded-xl p-5 mb-6">
                <h3 class="font-headline text-lg font-bold text-on-surface mb-3">
                  ### Salon z jadalnią
                </h3>
                <p class="text-primary font-bold text-xl mb-4">
                  Powierzchnia: 34,2 m²
                </p>
                <ul class="space-y-2 text-sm text-secondary">
                  <li class="flex items-start gap-2">
                    <span class="text-primary mt-0.5">*</span>
                    <span>Jasne przeszklenia tarasowe</span>
                  </li>
                  <li class="flex items-start gap-2">
                    <span class="text-primary mt-0.5">*</span>
                    <span>Wyjście południowo-zachodnie</span>
                  </li>
                  <li class="flex items-start gap-2">
                    <span class="text-primary mt-0.5">*</span>
                    <span>Przylega do kominka</span>
                  </li>
                </ul>
              </div>
              
              <!-- Interior Visualization Button -->
              <button class="w-full flex items-center justify-center gap-3 bg-on-surface text-white py-4 px-6 rounded-xl font-label text-xs font-bold tracking-widest uppercase hover:bg-on-surface/90 transition-colors">
                <span class="material-symbols-outlined text-xl">photo_camera</span>
                ZOBACZ WIZUALIZACJĘ WNĘTRZA
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const currentScene = ref<1 | 2>(1)
const hoveredArea = ref<number | null>(null)
const selectedSegment = ref<'left' | 'right' | null>(null)
const activeView = ref<'plot' | 'ground' | 'first'>('ground')

const goToScene = (sceneNumber: 1 | 2) => {
  currentScene.value = sceneNumber
}

const selectSegment = (segment: 'left' | 'right') => {
  selectedSegment.value = segment
}
</script>
