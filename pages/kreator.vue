<template>
  <div class="bg-gradient-to-br from-surface to-surface-variant/30 min-h-screen overflow-hidden">
    <TheNavigation />
    
    <div class="pt-24 pb-6 h-screen flex flex-col">
      <div class="container mx-auto px-4 flex-1 flex flex-col min-h-0 max-w-6xl">
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
            <div class="grid grid-cols-1 gap-4 flex-1 min-h-0">
              <!-- House Stage - Full Width -->
              <div class="w-full h-full min-h-0">
                <div class="bg-white/50 backdrop-blur-sm rounded-2xl overflow-hidden shadow-inner border border-surface-variant/10 h-full flex flex-col min-h-0 relative">
              <div class="px-6 pt-3 pb-2">
                <div class="text-xs font-label tracking-widest text-secondary uppercase">
                  STAGE
                </div>
              </div>
              
              <!-- House Image with Interactive SVG -->
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
                        <span class="font-bold tracking-wide text-xs">ZOBACZ RZUT TECHNICZNY (2D)</span>
                      </button>
                    </div>
                  </div>
                </div>
                
                <!-- Regular image (always present to maintain layout) -->
                <img
                  :src="currentScene === 1 ? '/assets/scenes/scena1.png' : currentScene === 2 ? '/assets/scenes/scena2.png' : currentScene === 3 ? '/assets/scenes/scena3.png' : '/assets/scenes/scena4.png'"
                  alt="Dom w Cyklamenach"
                  class="max-w-full max-h-full object-contain"
                />
                
                <!-- Video overlay (appears on top when playing) -->
                <transition name="fade">
                  <video
                    v-if="isVideoPlaying"
                    ref="videoPlayer"
                    class="absolute inset-0 w-full h-full object-contain"
                    style="will-change: opacity;"
                    @ended="onVideoEnd"
                    autoplay
                    muted
                  >
                    <source :src="currentVideoSrc" type="video/mp4" />
                  </video>
                </transition>
                
                <!-- SVG Overlay for Scene 1 -->
                <svg 
                  v-if="currentScene === 1 && !isVideoPlaying"
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
                <div v-if="currentScene === 1 && !isVideoPlaying">
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
                  v-if="currentScene === 2 && !isVideoPlaying"
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
                    @click="playVideoForSegment('left')"
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
                
                <!-- SVG Overlay for Scene 3 -->
                <svg 
                  v-if="currentScene === 3 && !isVideoPlaying"
                  viewBox="0 0 2754 1536"
                  class="absolute top-0 left-0 w-full h-full"
                  style="pointer-events: none;"
                >
                  <polygon
                    id="mieszkanie-a2"
                    points="859,626 865,893 560,893 558,630"
                    :fill="hoveredArea === 4 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 4 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 4"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a2')"
                  />
                  
                  <polygon
                    id="mieszkanie-a3"
                    points="948,1240 561,1240 563,910 857,910 946,988"
                    :fill="hoveredArea === 5 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 5 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 5"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a3')"
                  />
                  
                  <polygon
                    id="mieszkanie-a4"
                    points="1235,991 1235,1242 965,1244 966,995"
                    :fill="hoveredArea === 8 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 8 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 8"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a4')"
                  />
                  
                  <polygon
                    id="mieszkanie-a1"
                    points="994,321 996,614 560,615 565,327"
                    :fill="hoveredArea === 7 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 7 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 7"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a1')"
                  />
                  
                  <polygon
                    id="mieszkanie-a5"
                    points="1395,995 1253,993 1257,1244 1401,1244"
                    :fill="hoveredArea === 6 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 6 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 6"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a5')"
                  />
                  
                  <polygon
                    id="mieszkanie-a6"
                    points="1419,294 1010,294 1010,610 1037,612 1126,741 1410,741"
                    :fill="hoveredArea === 9 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 9 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 9"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a6')"
                  />
                  
                  <polygon
                    id="mieszkanie-a7"
                    points="1166,759 1170,975 963,977 879,904 879,630 1035,632 1119,763"
                    :fill="hoveredArea === 10 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 10 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 10"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a7')"
                  />
                  
                  <polygon
                    id="mieszkanie-a8"
                    points="1415,149 1417,241 983,243 983,149"
                    :fill="hoveredArea === 12 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 12 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 12"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a8')"
                  />
                  
                  <polygon
                    id="mieszkanie-a9"
                    points="1397,757 1401,966 1174,964 1170,757"
                    :fill="hoveredArea === 11 ? '#D44E98' : '#e879f9'"
                    :fill-opacity="hoveredArea === 11 ? '0.3' : '0.15'"
                    stroke="#e879f9"
                    stroke-width="3"
                    stroke-linejoin="round"
                    class="cursor-pointer transition-all"
                    style="pointer-events: auto;"
                    @mouseenter="hoveredArea = 11"
                    @mouseleave="hoveredArea = null"
                    @click="selectApartment('a9')"
                  />
                </svg>
                
                <!-- Info Tooltips for Scene 2 -->
                <div v-if="currentScene === 2 && !isVideoPlaying">
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
                
                <!-- Info Tooltips for Scene 3 -->
                <div v-if="currentScene === 3 && !isVideoPlaying">
                  <!-- Pokój dzienny -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 4"
                      class="absolute left-[18%] top-[52%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Łazienka
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">8.5 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Wanna</div>
                        <div>• Prysznic</div>
                        <div>• Okno</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Salon z jadalnią -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 5"
                      class="absolute left-[20%] top-[72%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Schody
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">4.5 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Żelbetowe</div>
                        <div>• Bezpieczne</div>
                        <div>• Wykończone wg projektu</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Łazienka -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 6"
                      class="absolute left-[44%] top-[72%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Garderoba
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">4.8 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Szafy wnękowe</div>
                        <div>• Lustro</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Przedpokój -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 7"
                      class="absolute left-[20%] top-[32%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Pokój 1
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">5.2 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Okno</div>
                        <div>• Idealne na gabinet</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Garderoba -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 8"
                      class="absolute left-[35%] top-[72%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Pokój 3
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">3.5 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Pokój dziecięcy</div>
                        <div>• Regały</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Sypialnia -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 9"
                      class="absolute left-[40%] top-[35%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Sypialnia
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">10.5 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Drzwi balkonowe</div>
                        <div>• Złącze do klimatyzacji</div>
                        <div>• Skosy od wys. 140cm</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Kuchnia -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 10"
                      class="absolute left-[30%] top-[58%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Przedpokój
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">6.8 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Szafa wnękowa</div>
                        <div>• Domofon</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Pokój 2 -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 11"
                      class="absolute left-[45%] top-[58%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Schody
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">3.2 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Wygodny bieg</div>
                        <div>• Możliwość podświetlenia</div>
                      </div>
                    </div>
                  </transition>
                  
                  <!-- Balkon -->
                  <transition name="fade">
                    <div 
                      v-if="hoveredArea === 12"
                      class="absolute left-[38%] top-[12%] bg-white/70 backdrop-blur-md p-2 rounded-xl shadow-xl border-2 border-[#e879f9] z-10"
                      style="pointer-events: none;"
                    >
                      <h3 class="font-headline text-sm font-bold text-on-surface mb-1 uppercase">
                        Balkon
                      </h3>
                      <div class="text-xs font-body text-on-surface mb-1">2.3 m²</div>
                      <div class="text-xs font-body text-secondary leading-tight space-y-0.5">
                        <div>• Ekspozycja południowa</div>
                      </div>
                    </div>
                  </transition>
                </div>
                
                <!-- Technical Plan Overlay - Scene 4 -->
                <transition name="plan-fade">
                  <div 
                    v-if="currentScene === 4"
                    class="absolute inset-0 bg-black/40 backdrop-blur-sm flex items-center justify-center z-30"
                    @click="goToScene(3)"
                  >
                    <button 
                      @click="goToScene(3)"
                      class="absolute top-6 right-6 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 backdrop-blur-md flex items-center justify-center transition-colors z-40"
                    >
                      <span class="material-symbols-outlined text-white text-2xl">close</span>
                    </button>
                    <div class="max-w-5xl max-h-[90vh]" @click.stop>
                      <img 
                        src="/assets/scenes/rzut.png" 
                        alt="Rzut techniczny"
                        class="w-full h-full object-contain"
                      />
                    </div>
                  </div>
                </transition>
              </div>
              
              <!-- Bottom Controls -->
              <div class="px-6 py-2">
                <div class="flex items-center justify-center gap-3 text-secondary text-sm">
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
                    <button 
                      @click="goToScene(3)"
                      class="w-6 h-0.5 rounded-full transition-colors"
                      :class="currentScene === 3 ? 'bg-primary' : 'bg-outline-variant/30'"
                    ></button>
                    <button 
                      @click="goToScene(4)"
                      class="w-6 h-0.5 rounded-full transition-colors"
                      :class="currentScene === 4 ? 'bg-primary' : 'bg-outline-variant/30'"
                    ></button>
                  </div>
                  <button 
                    @click="goToScene(2)" 
                    class="p-1.5 hover:bg-surface-container-low rounded-lg transition-colors"
                    :class="{ 'bg-surface-container-low': currentScene === 2 }"
                  >
                    <span class="material-symbols-outlined text-xl">filter_2</span>
                  </button>
                  <button 
                    @click="goToScene(3)" 
                    class="p-1.5 hover:bg-surface-container-low rounded-lg transition-colors"
                    :class="{ 'bg-surface-container-low': currentScene === 3 }"
                  >
                    <span class="material-symbols-outlined text-xl">filter_3</span>
                  </button>
                  <button 
                    @click="goToScene(4)" 
                    class="p-1.5 hover:bg-surface-container-low rounded-lg transition-colors"
                    :class="{ 'bg-surface-container-low': currentScene === 4 }"
                  >
                    <span class="material-symbols-outlined text-xl">filter_4</span>
                  </button>
                </div>
                
                <!-- PDF Download Section -->
                <div class="mt-2 text-center">
                  <button class="primary-gradient-bg text-on-primary py-2 px-6 rounded-lg font-label text-[10px] font-bold tracking-[0.2em] uppercase shadow-md shadow-primary/30 hover:scale-105 transition-transform">
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
</div>
</div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const currentScene = ref<1 | 2 | 3 | 4>(1)
const hoveredArea = ref<number | null>(null)
const selectedSegment = ref<'left' | 'right' | null>(null)
const activeView = ref<'plot' | 'ground' | 'first'>('ground')
const isVideoPlaying = ref(false)
const videoPlayer = ref<HTMLVideoElement | null>(null)
const currentVideoSrc = ref('/assets/scenes/film1.mp4')

// Preload images to avoid flickers
import { onMounted } from 'vue'
onMounted(() => {
  ['scena1.png', 'scena2.png', 'scena3.png', 'scena4.png'].forEach(img => {
    const i = new Image()
    i.src = `/assets/scenes/${img}`
  })
})

const goToScene = (sceneNumber: 1 | 2 | 3 | 4) => {
  if (sceneNumber === 2 && currentScene.value === 1) {
    // Play video before transitioning to scene 2
    currentVideoSrc.value = '/assets/scenes/film1.mp4'
    isVideoPlaying.value = true
    currentScene.value = 2 // Update background immediately while video covers it
  } else {
    currentScene.value = sceneNumber
  }
}

const playVideoForSegment = (segment: 'left' | 'right') => {
  if (segment === 'left') {
    // Play film2 before showing segment details (stage 3)
    currentVideoSrc.value = '/assets/scenes/film2.mp4'
    isVideoPlaying.value = true
    currentScene.value = 3 // Update stage immediately
  }
}

const playTechnicalPlan = () => {
  // Play film3 for technical plan (stage 4)
  currentVideoSrc.value = '/assets/scenes/film3.mp4'
  isVideoPlaying.value = true
  currentScene.value = 4 // Update background immediately
}

const onVideoEnd = () => {
  // Video finished, just hide it. backgroundScene is already updated.
  isVideoPlaying.value = false
}

const selectSegment = (segment: 'left' | 'right') => {
  selectedSegment.value = segment
}

const selectApartment = (apartment: string) => {
  console.log('Selected apartment:', apartment)
  // TODO: Add apartment selection logic
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
  backface-visibility: hidden;
  transform: translateZ(0);
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.plan-fade-enter-active {
  transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
  backface-visibility: hidden;
}
.plan-fade-leave-active {
  transition: all 0.4s ease;
  backface-visibility: hidden;
}
.plan-fade-enter-from {
  opacity: 0;
  transform: scale(0.8) translateZ(0);
}
.plan-fade-leave-to {
  opacity: 0;
  transform: scale(0.95) translateZ(0);
}
</style>
